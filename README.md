
# Hosting a Dynamic Web App on AWS with Terraform, Docker, Amazon ECR, and ECS

## Project Overview
This project demonstrates the process of hosting a dynamic web application on AWS using a modular infrastructure as code approach. The setup includes containerizing the web app with Docker, storing the Docker image in Amazon ECR (Elastic Container Registry), and deploying the app on an ECS (Elastic Container Service) cluster, all managed through Terraform.

## Project Structure
terraform-ecs-webapp/ ├── modules/ │ ├── ecr/ # Terraform module for creating Amazon ECR repository │ ├── ecs/ # Terraform module for provisioning ECS resources ├── my-webapp/ # Application code and Dockerfile │ ├── app.js # Node.js app code (or similar if using another language) │ ├── Dockerfile # Dockerfile to containerize the application ├── main.tf # Main Terraform configuration to orchestrate modules └── README.md # Project documentation

markdown
Copy code

## Technologies Used
- **Terraform**: Infrastructure as Code to automate AWS resource creation
- **AWS**: Services including ECS, ECR, IAM, and VPC for application hosting and networking
- **Docker**: For containerizing the web application
- **Node.js (or your chosen framework)**: Web application framework for backend service
- **Git/GitHub**: Version control and code hosting

## Project Setup

### Prerequisites
- **Docker**: [Install Docker](https://docs.docker.com/get-docker/)
- **AWS CLI**: [Install AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) and configure with your credentials
- **Terraform**: [Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)

### Steps to Run the Project

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/terraform-ecs-webapp.git
   cd terraform-ecs-webapp
2. Dockerize the Web Application:

   Build the Docker image:

 
   cd my-webapp
   docker build -t my-webapp .
   Test the Docker container locally:


   docker run -p 3000:3000 my-webapp
   Access the app at http://localhost:3000 to ensure it’s working.

3. Deploy Infrastructure Using Terraform:

   Initialize Terraform in the project directory:



   terraform init
   Apply the Terraform configuration to provision the AWS infrastructure:



   terraform apply -auto-approve
   This will set up an ECS cluster, create an ECR repository, and deploy the Dockerized web app.

4. Push Docker Image to Amazon ECR:

   Authenticate Docker with ECR:

 

   aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin <account_id>.dkr.ecr.your-region.amazonaws.com
   Tag and push the Docker image:



   docker tag my-webapp:latest <account_id>.dkr.ecr.your-region.amazonaws.com/webapp-repo:latest
   docker push <account_id>.dkr.ecr.your-region.amazonaws.com/webapp-repo:latest

5. Access the Application:

   Once deployed, you can access the web application through the public IP or DNS of the ECS service.