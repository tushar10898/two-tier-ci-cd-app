# Two-Tier Dockerized Flask and MySQL App on Amazon EC2 with GitHub Integration

<img width="960" alt="two-tier app" src="https://github.com/tushar10898/two-tier-app/assets/165803170/bc39dcd4-a397-4bd8-85d1-e8ce797d0324">


## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Components](#components)
4. [Setup](#setup)
    - [GitHub Repository Setup](#github-repository-setup)
    - [Create Amazon EC2 Instance](#create-amazon-ec2-instance)
5. [Steps Involved](#steps-involved)
    - [Clone GitHub Repository to EC2 Instance](#clone-github-repository-to-ec2-instance)
    - [Manual Deployment Option 1: Dockerfile and Building Docker Images](#manual-deployment-option-1-dockerfile-and-building-docker-images)
    - [Manual Deployment Option 2: Docker Compose](#manual-deployment-option-2-docker-compose)
    - [Accessing the Application](#accessing-the-application)
6. [Maintenance](#maintenance)
7. [Conclusion](#conclusion)

---

## Introduction

This project demonstrates the setup and deployment of a two-tier Dockerized application using Flask for the frontend and MySQL for the backend on Amazon EC2. The application is containerized using Docker for easy deployment and scalability, while GitHub is used as the code repository for version control and collaboration.

## Prerequisites

Before you begin, ensure you have the following:

- An Amazon Web Services (AWS) account
- Basic knowledge of AWS EC2, Docker, Flask, MySQL, and Git
- A GitHub repository for your project

## Components

1. **Flask**: A lightweight web framework for Python used to develop the frontend of the application.
2. **MySQL**: An open-source relational database management system used for storing and managing application data.
3. **Docker**: A platform for developing, shipping, and running applications inside containers.
4. **Amazon EC2**: A web service that provides resizable compute capacity in the cloud.
5. **GitHub**: A web-based Git repository hosting service for version control and collaboration.

## Setup

1. **GitHub Repository Setup**
   - Create a new GitHub repository for your project.
   - Upload the necessary files for your Flask application to the repository. Ensure that the repository includes the following files and folders:
     - `app.py`: The main Flask application file.
     - `message.sql`: SQL file containing the SQL commands to create the required table(s) for the application. Ensure it includes the SQL command to create the `message` table.
     - `requirements.txt`: File listing all Python dependencies required for the Flask application.
     - `templates`: Folder containing the HTML templates and static files for the application. This folder should include at least an `index.html` file for the app template.
   
2. **Create Amazon EC2 Instance**
   - Log in to your AWS Management Console and navigate to the EC2 dashboard.
   - Launch a new EC2 instance by clicking on "Launch Instance".
   - Choose an appropriate Amazon Machine Image (AMI), such as Amazon Linux or Ubuntu Server.
   - Select an instance type based on your requirements.
   - Configure instance details such as network settings, security groups, and key pairs.
   - Review and launch the instance.
   - Once the instance is running, note down the public IP address or domain name associated with it for future SSH access.

## Steps Involved

1. **Clone GitHub Repository to EC2 Instance**
   - Clone your GitHub repository to the EC2 instance using the following command:
     ```
     git clone https://github.com/your-username/your-repository.git
     ```
   - This will clone all the necessary files and folders from your GitHub repository to your EC2 instance, including `app.py`, `message.sql`, `requirements.txt`, and `templates`.

2. **Docker file and Building Docker Images**
   - Create a Dockerfile for your Flask application to define its environment and dependencies.
   - Build Docker images for both your Flask application and MySQL database using the following commands:
     ```
     docker build -t flask-app -f Dockerfile .
     docker pull mysql:latest
     ```

3. **Docker Compose**
   - **Why Docker Compose?** Docker Compose is used to define and run multi-container Docker applications. It simplifies the process of defining and managing the interaction between different services.
   - **Installation:** To install Docker Compose on an EC2 instance running Ubuntu, you can use the following commands:
     ```
     sudo apt update
     sudo apt install -y docker-compose
     ```
   - **Docker Compose File Creation:** Create a `docker-compose.yml` file in your project directory to define the services, networks, and volumes for your application.
   
   - **Starting Docker Compose:** Once you have your `docker-compose.yml` file ready, navigate to the directory containing the file and execute the following command to start the Docker Compose services:
     ```
     docker-compose up -d
     ```
     The `-d` flag runs the containers in detached mode, meaning they run in the background. To view logs and follow the output of the containers, omit the `-d` flag.

   - **Stopping Docker Compose:** To stop the Docker Compose services, navigate to the directory containing the `docker-compose.yml` file and execute the following command:
     ```
     docker-compose down
     ```
     This command will stop and remove the containers, networks, and volumes defined in the `docker-compose.yml` file. Optionally, you can use the `-v` flag to also remove volumes associated with the containers.

## Accessing the Application

Once the containers are running, access your Flask application through the public IP address or domain name associated with your EC2 instance. Test the functionality of your application to ensure it is working correctly.

**Note:** If you encounter issues accessing the application, ensure that port 5000 is open in the security settings of your EC2 instance. You may need to add an inbound rule allowing traffic on port 5000 to ensure the Flask application can be accessed. 

## Maintenance

1. **Monitoring and Scaling**
   - Utilize AWS monitoring tools such as CloudWatch to monitor the performance and health of your EC2 instance and Docker containers. Scale your application horizontally by adding more EC2 instances behind a load balancer to handle increased traffic.
   
2. **Backup and Disaster Recovery**
   - Implement regular backups of your MySQL database using AWS Backup or automated scripts. Configure snapshots for your EC2 instance and ensure that critical data is backed up in case of hardware failure or other disasters.

3. **Version Control and Collaboration**
   - Continuously update and maintain your Dockerfile and `docker-compose.yml` file based on changes to your application requirements. After making any modifications, remember to push the updated files to your GitHub repository to keep track of changes and enable collaboration with other team members.

## Conclusion

By following this documentation, you can successfully create, deploy, and maintain a two-tier Dockerized application using Flask for the frontend and MySQL for the backend on Amazon EC2, with GitHub as the code repository. This setup provides scalability, flexibility, and reliability for your web application while streamlining the development and deployment processes through manual deployment on the EC2 instance.

