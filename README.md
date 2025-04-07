🚀 DevOps CI/CD Pipeline Project with Jenkins on AWS
This project demonstrates a complete DevOps CI/CD pipeline using Jenkins, Maven, and Docker, deployed on an AWS EC2 instance. It automates the process of building, testing, and deploying a sample Java application to ensure continuous delivery and integration.

**📌 Project Overview**
This project focuses on setting up a CI/CD pipeline that:

Automates code integration and builds using Jenkins

Builds the project with Maven

Creates and runs Docker containers for deployment

Runs on a cloud-based infrastructure (AWS EC2)

Deploys a sample Java web application to Tomcat

🧰 **Tech Stack**

AWS EC2

Jenkins

Java 17 & 8

Maven

Docker

Tomcat

Git

**🛠️ Setup & Configuration**
1. Launching EC2 Instance
Created an EC2 instance on AWS

Configured security group to allow SSH (22), HTTP (80), and Jenkins (8080)

**2. Installing Prerequisites**
bash
Copy
Edit
**# Java**
sudo yum update -y
sudo yum install java-17-amazon-corretto-devel -y
sudo yum install java-1.8.0-openjdk -y

**# Jenkins**
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
3. Installing Maven & Docker
bash
Copy
Edit
**# Maven**
sudo yum install maven -y
mvn -version

**# Docker**
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
🔧 Jenkins Configuration
Plugins Installed:
Maven Integration Plugin

Git Plugin

Docker Pipeline Plugin

Configurations:
Configured global tools (Java, Git, Maven)

Created a new Pipeline Project in Jenkins

📄** Jenkins Pipeline Script**
Created a Jenkins pipeline script to automate:
pipeline {
    agent any
    tools {
        maven 'Maven'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/Manikandanravi19/githubmani.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Docker Build and Push') {
            steps {
                script {
                    sh 'docker build -t myapp:latest .'
                    sh 'docker run -d -p 8081:8080 myapp:latest'
                }
            }
        }
    }
}


Code checkout from Git

Maven build

Docker image creation

Docker container deployment

📌 Before execution, no Docker images were running. Post pipeline run, the Docker container was successfully launched and validated.

**✅ Output & Validation**
Jenkins job executed successfully

Docker image created and container launched

Application accessed via the public IP and Tomcat port

**🎯 Conclusion**
This project showcases the seamless integration of Jenkins, Maven, and Docker in automating software delivery. 
By leveraging AWS, we ensured scalability and real-world infrastructure simulation, making this a practical and production-ready DevOps solution.
