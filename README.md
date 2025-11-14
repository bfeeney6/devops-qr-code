# devops-qr-code

This project is an adaptation and extension of the original QR Code Generator by
Rishab Kumar
.

I expanded the original local-only application into a fully cloud-hosted deployment running on AWS EKS, using Infrastructure as Code (Terraform) and Kubernetes for orchestration and networking.

🚀 Cloud Adaptation Summary

This version of the project includes:

Amazon EKS cluster provisioned via Terraform

Managed Node Group running application workloads

Docker images pushed to Docker Hub:

Frontend: bfeeney6/devops-qr-frontend:latest

API: bfeeney/devops-qr-code-api:latest

Kubernetes Deployments for frontend and API

Kubernetes Services:

LoadBalancer Service to expose the frontend publicly

ClusterIP Service for internal API communication

GitHub Actions CI/CD pipeline that automatically builds and pushes images to Docker Hub when Dockerfiles change

This adapts the base application into a cloud-native deployment suitable for learning DevOps, Kubernetes, and infrastructure automation.
## Application

Front-End

Next.js web UI that allows users to input URLs for QR code generation.

API

FastAPI backend that:

Accepts URL submissions

Generates QR codes

Uploads them to an AWS S3 bucket

## Running locally

### API

The API code exists in the `api` directory. You can run the API server locally:

- Clone this repo
- Make sure you are in the `api` directory
- Create a virtualenv by typing in the following command: `python -m venv .venv`
- Install the required packages: `pip install -r requirements.txt`
- Create a `.env` file, and add you AWS Access and Secret key, check  `.env.example`
- Also, change the BUCKET_NAME to your S3 bucket name in `main.py`
- Run the API server: `uvicorn main:app --reload`
- Your API Server should be running on port `http://localhost:8000`

### Front-end

The front-end code exits in the `front-end-nextjs` directory. You can run the front-end server locally:

- Clone this repo
- Make sure you are in the `front-end-nextjs` directory
- Install the dependencies: `npm install`
- Run the NextJS Server: `npm run dev`
- Your Front-end Server should be running on `http://localhost:3000`

☁️ AWS Deployment Overview
🟩 Infrastructure (Terraform)

Terraform provisions:

VPC

Public & private subnets

Amazon EKS Cluster

Managed Node Group

IAM roles, networking, and cluster configuration

🟦 Kubernetes Configuration

After the cluster is created, Kubernetes manages:

Frontend Deployment & Service

Runs the Next.js image from Docker Hub

Exposes publicly through a LoadBalancer Service

API Deployment & Service

Runs the FastAPI image from Docker Hub

Exposed internally using a ClusterIP Service

Accessible to frontend Pods only

🔄 CI/CD (GitHub Actions)

This project includes GitHub Actions that:

Detect changes to Dockerfiles

Automatically build new Docker images

Push them to Docker Hub

Ensuring EKS deployments always pull the latest images


## License

[MIT](./LICENSE)
