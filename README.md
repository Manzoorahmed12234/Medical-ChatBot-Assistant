# ⚕️ Intelligent Medical Chatbot Agent: LLMs, LangChain, Pinecone, Flask, and AWS CI/CD

This repository provides the complete solution for developing and deploying a sophisticated **Medical Chatbot Agent**. Engineered to deliver reliable and contextualized medical information, this system integrates **Large Language Models (LLMs)** with the LangChain framework for powerful natural language understanding and response generation. Persistent, efficient knowledge retrieval is managed by **Pinecone**, and the application is exposed via a **Flask** web server.

The project features a **fully automated CI/CD pipeline** using GitHub Actions, Docker, and AWS services (ECR, EC2) for streamlined, production-ready deployment.

---

## ⚙️ Quick Start: Local Deployment

Get your Medical Agent running in minutes with these simple steps.

### **Prerequisites**

* Git
* Conda (Recommended)

### **Setup Guide**

1.  **Clone the Repository**

    ```bash
    git clone 
    ```

2.  **Environment Setup**

    ```bash
    conda create -n medibot python=3.10 -y
    conda activate medibot
    ```

3.  **Install Dependencies**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Configure API Keys**

    Create a file named `.env` in the root directory and securely add your **Pinecone** and **OpenAI** credentials:

    ```ini
    PINECONE_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    OPENAI_API_KEY = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    ```

5.  **Index Medical Knowledge**

    Prepare your knowledge base by generating embeddings and storing them in your Pinecone index:

    ```bash
    python store_index.py
    ```

6.  **Launch the Agent**

    Start the Flask web application:

    ```bash
    python app.py
    ```

7.  **Access:** Open your browser to the local host address shown in the terminal.

---

## 🛠️ Technology Stack Breakdown

| Component | Technology | Role in the System |
| :--- | :--- | :--- |
| **Agent Core** | **LLMs (GPT)** | The engine providing intelligent, human-like medical responses. |
| **Orchestration** | **LangChain** | Manages the complex chains and interactions between components. |
| **Knowledge Base** | **Pinecone** | Vector database for high-speed similarity search and retrieval-augmented generation (RAG). |
| **Web Server** | **Flask** | Lightweight server hosting the chatbot interface. |
| **Deployment** | **AWS (EC2, ECR)** | Cloud infrastructure for hosting and container management. |
| **Automation** | **GitHub Actions** | CI/CD pipeline ensuring continuous delivery. |

---

## 🚀 CI/CD Pipeline: Automated Deployment to AWS

This project includes a powerful workflow to automatically build, push, and deploy the application to AWS using Docker and GitHub Actions.

### 1. AWS IAM and ECR Configuration

* **IAM User:** Create a dedicated IAM user with the following required policies for GitHub Actions:
    * `AmazonEC2ContainerRegistryFullAccess`
    * `AmazonEC2FullAccess`
* **ECR Repo:** Create an ECR repository to host the Docker image. **Note its URI** (e.g., `315865595366.dkr.ecr.us-east-1.amazonaws.com/medicalbot`).
* **EC2 Host:** Launch an Ubuntu-based EC2 instance to run the application container.

### 2. EC2 Host Preparation

Install Docker and configure the EC2 machine for CI/CD:

```bash
# Install Docker
curl -fsSL [https://get.docker.com](https://get.docker.com) -o get-docker.sh
sudo sh get-docker.sh

# Add user to docker group
sudo usermod -aG docker ubuntu
newgrp docker
