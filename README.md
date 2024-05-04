## Federated Learning for Fine-Tuning ML Models

This repository explores the potential of federated learning (FL) in fine-tuning machine learning models while preserving data privacy.

**Federated Learning**

Federated learning allows collaborative training of a central model on distributed data residing on individual devices. Devices train the model locally and send updates (weight adjustments) to the central server for aggregation, improving the overall model without sharing raw data. 

**Frameworks Used**

* **Flower:** A user-friendly framework for building FL systems, focusing on computation movement rather than data sharing. We primarily use Flower due to its community support and broader library compatibility. 
* **OpenFL:** A Python framework for FL, designed for flexibility and ease of learning.

**Code Examples**

This repository includes code for various algorithms implemented using Flower and OpenFL:

* Linear Regression
* Logistic Regression
* Multi-Class Classification
* Fine-tuning:
    * GPT-2 Sequence Classifier Model
    * DistilBERT Sequence Classifier Model
    * juliensimon/reviews-sentiment-analysis Sequence Classifier Model (DistilBERT fine-tuned on generated_reviews_enth dataset)

**LLM Models Used**

1. **GPT-2:** A powerful transformer model for text generation and classification.
2. **DistilBERT:** A lightweight transformer model ideal for resource-constrained environments, effective for tasks like sentiment analysis.
3. **juliensimon/reviews-sentiment-analysis:** A DistilBERT model fine-tuned on the generated_reviews_enth dataset for sentiment classification (positive/negative reviews).

**Fine-Tuning on IMDB Dataset**

We fine-tuned all models on the IMDB dataset, containing 50,000 labeled movie reviews for sentiment analysis (positive/negative).

**Fine-Tuning Process**

1. **Data Preparation:** Gather and preprocess labeled data (cleaning text, tokenization, padding).
2. **Model Selection:** Choose a pre-trained LLM model based on task complexity and resource constraints.
3. **Model Loading:** Load the pre-trained LLM model using libraries like Hugging Face Transformers.
4. **Classification Head:** Add a new classification head on top of the pre-trained model to map the output to desired categories (e.g., positive/negative sentiment).
5. **Model Compilation:** Specify loss function (e.g., categorical cross-entropy), optimizer (e.g., Adam), and metrics (e.g., accuracy) for training evaluation.
6. **Model Training:** Train the model on the prepared data for a specified number of epochs and batch size.
7. **Monitoring and Evaluation:** Track training progress using metrics like loss and accuracy on a validation set to prevent overfitting.

**SSL Certification with Flower**

Flower allows using SSL certificates for secure communication. The general steps for certificate creation involve generating keys and certificates using OpenSSL commands and a configuration file specifying domain name, organization, etc.

* `openssl genrsa -out ca.key 4096`: This command generates a new private key (ca.key) with a size of 4096 bits for the Certificate Authority (CA).
* `openssl req -new -x509 -key ca.key -sha256 -subj "/C=DE/ST=HH/O=CA, Inc." -days 365 -out ca.crt`: This command creates a self-signed certificate (ca.crt) using the generated key (ca.key).
* `openssl genrsa -out server.key 4096`: Generate a new private key for the server
* `openssl req -new -key server.key -out server.csr -config ./certificate.conf`: Create a signing CSR
* `openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.pem -days 365 -sha256 -extfile ./certificate.conf -extensions req_ext`: Generate a certificate for the server


**Generating Server Key, CSR, and Certificate:**

You'll need a separate `certificate.conf` file for server-specific configurations.

**Note:** These commands are for demonstration purposes only. In a production environment, you'll likely use a more secure way to manage certificates.

**Remember to replace the placeholders with your own information.**

**Further Exploration**

This repository provides a foundation for exploring federated learning and fine-tuning LLM models. You can delve deeper into specific algorithms, experiment with different LLM models, or explore advanced federated learning techniques.
