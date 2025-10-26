# E-Commerce Product Assistant (LLMOps Project)

An AI-powered E-Commerce Product Assistant designed with LLMOps principles for scalable, production-grade deployment. This project integrates FastAPI, Streamlit, DataStax VectorDB, and AWS ECR/EKS to deliver seamless product search, recommendation, and workflow automation.

---

## Features

- LLM-Powered Search using agentic workflows with MCP servers for intelligent product discovery.  
- Dual Interface: FastAPI backend and Streamlit frontend.  
- Vector Search Integration with DataStax Vector Database for semantic retrieval.  
- Containerization & Deployment with Docker, AWS ECR, and EKS.  
- CI/CD Ready with GitHub Actions and environment secrets.

---

## Project Structure

```
prod_assistant/
│
├── router/
│   └── main.py
├── mcp_servers/
│   └── product_search_server.py
├── workflow/
│   └── agentic_workflow_with_mcp_websearch.py
├── streamlit_app.py
├── requirements.txt
├── pyproject.toml
├── Dockerfile
└── setup.py
```

---

## Setup Instructions

### Step 1: Environment Setup
```bash
uv --version
pip install uv
uv init ecomm-prod-assistant
uv venv env --python 3.10
.\env\Scripts\activate    # For Windows CMD
source env/Scripts/activate  # For Git Bash or Mac
```

### Step 2: Install Dependencies
```bash
uv pip install -r requirements.txt
```
or install as an editable package:
```bash
uv pip install -e .
```

---

## Running the Application

### Start MCP Server
```bash
python prod_assistant/mcp_servers/product_search_server.py
```

### Run Agentic Workflow
```bash
python prod_assistant/workflow/agentic_workflow_with_mcp_websearch.py
```

### Run FastAPI Backend
```bash
uvicorn prod_assistant.router.main:app --reload --port 8000
```
Access URL: http://127.0.0.1:8000

### Run Streamlit Frontend
```bash
streamlit run streamlit_app.py
```

---

## Docker Deployment

### Build Docker Image
```bash
docker build -t prod-assistant .
```

### Run Docker Container
```bash
docker run -d -p 8000:8000 --name product-assistant prod-assistant
```

Check and manage containers:
```bash
docker ps
docker stop <container_id>
docker rm <container_id>
docker images
docker rmi <image_id>
```

---

## AWS Deployment (ECR & EKS)

### Step 1: Install AWS CLI
Download and install AWS CLI:  
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### Step 2: Configure AWS
```bash
aws configure
aws eks update-kubeconfig --name product-assistant-cluster-latest --region us-west-1
kubectl get nodes
kubectl get svc -o wide
kubectl describe svc product-assistant-service
kubectl get pods -o wide
kubectl logs <pod_id>
```

### Step 3: GitHub Secrets
Set up the following secrets in your GitHub repository:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
ECR_REGISTRY
ECR_REPOSITORY
EKS_CLUSTER_NAME
GROQ_API_KEY
GOOGLE_API_KEY
ASTRA_DB_API_ENDPOINT
ASTRA_DB_APPLICATION_TOKEN
ASTRA_DB_KEYSPACE
```

---

## Vector DB and References

- DataStax Astra Vector Database:  
  https://accounts.datastax.com/session-service/v1/login

- Vector DB Comparison:  
  https://superlinked.com/vector-db-comparison

---

