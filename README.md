# Cloud-Based Web App Deployment on AWS
This project is a full-stack web application deployed on AWS cloud infrastructure. It includes user registration/login, CRUD operations for posts, and file/image uploads using AWS services like EC2, RDS, S3, and Elastic Beanstalk.


## 🛠️ Tech Stack
- Frontend: React
- Backend: Node.js + Express
- Database: Amazon RDS (MySQL)
- File Storage: Amazon S3
- Deployment:
  - Backend on EC2 
  - Frontend on Elastic Beanstalk

## 🚀 Deployment Guide
###🧩 1. Pre-requisites
- AWS account with Free Tier access
- AWS CLI installed and configured
- Node.js and npm installed locally
- React installed locally (for frontend development)
- Git for cloning the project

###☁️ 2. AWS Infrastructure Setup
🔹 VPC Configuration
- Created a custom VPC: Taijya-Abdullah-AppVPC with CIDR block 10.0.0.0/16.
- Added 4 subnets:
      - Public Subnets: us-east-1a and us-east-1b
      - Private Subnets: us-east-1a and us-east-1b
- Attached an Internet Gateway for public subnet access.
- Added 2 NAT Gateways for private subnets to access internet for updates.
- Configured 3 route tables: 1 public, 2 private.

🔹 Security Groups
- EC2 Security Group: Allowed inbound on ports 22 (SSH), 80 (HTTP), 443 (HTTPS), 5000 (App).
- RDS Security Group: Allowed port 3306 only from EC2’s security group.
- Elastic Beanstalk Security Group: Allowed HTTP/HTTPS access from anywhere.

🔹 IAM Roles
- Created an IAM role for EC2 instance to access S3 and RDS (attached during EC2 launch).
- Created an IAM role for Elastic Beanstalk environment to manage deployment resources.

🔹 Amazon RDS (MySQL)
- Deployed a single-AZ MySQL database in the private subnet.
- Used for storing user and post data.

🔹 Amazon S3
- Created an S3 bucket for user-uploaded files (images and PDFs).
- Attached bucket policy to allow access from the EC2 IAM role only.

###⚙️ 3. Backend Deployment (Node.js on EC2)
- Launched an EC2 instance in the public subnet with attached IAM role and security group
- Connected via SSH using a key pair
- Installed Node.js and dependencies
- Set environment variables for:
- RDS_HOSTNAME, RDS_USERNAME, RDS_PASSWORD, AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, S3_BUCKET_NAME, etc.
- Started the server using:
        node index.js

###🌐4. Frontend Deployment 
- Created an Elastic Beanstalk application and environment
- Selected custom VPC and public subnets for deployment
- Attached IAM role for Beanstalk
- Built the React app:
        npm run build
- Zipped the build folder and uploaded it through the Elastic Beanstalk dashboard

### 🔐5. Environment Variables
You need to set the following environment variables:
- `RDS_HOSTNAME`
- `RDS_USERNAME`
- `RDS_PASSWORD`
- `RDS_DATABASE`
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `S3_BUCKET_NAME`
- `JWT_SECRET`

  ## 🌍 Live Demo
- Frontend: http://tajiya-abdullah-webapp-env.eba-p3jetumx.us-east-1.elasticbeanstalk.com/
- Backend: [http://your-backend-ec2.amazonaws.com:5000](https://3.83.69.126/)


