Jenkins CI/CD Pipeline for Django App
Objective

Set up a Jenkins pipeline to automate the building, testing, Dockerizing, and deployment of a Django application.

Tools Used

Jenkins – CI/CD automation server

Docker – Containerization platform

Git/GitHub – Version control and source repository

Docker Compose – Multi-container application deployment

Repo Structure
django-notes-app/
├── api/                   # Django app API files
├── mynotes/               # Frontend React app (if any)
├── notesapp/              # Django project files
├── staticfiles/           # Django static files
├── Dockerfile             # Dockerfile for Django app
├── docker-compose.yml     # Docker Compose file for deployment
├── Jenkinsfile            # CI/CD pipeline definition
├── requirements.txt       # Python dependencies
├── README.md              # Project documentation
└── .gitignore             # Git ignore file

Pipeline Overview

The Jenkins pipeline consists of the following stages:

Checkout – Pulls code from the GitHub repository (master or main).

Build – Logs into Docker Hub, builds a Docker image of the application.

Test – Placeholder stage for running automated tests.

Push to Docker Hub – Pushes the Docker image to Docker Hub.

Deploy – Deploys the application using Docker Compose.

Prerequisites

Jenkins installed and running.

Docker installed on the Jenkins host.

Jenkins user added to the docker group (no sudo needed).

Docker Hub account with credentials stored in Jenkins (dockerhub credential ID).

GitHub repository with at least one commit on the branch you want to build (master or main).

Setup Instructions

Clone repository locally:

git clone https://github.com/negiminakshi/django-notes-app.git
cd django-notes-app


Ensure Docker is running and Jenkins user has permissions:

sudo usermod -aG docker jenkins
sudo systemctl restart jenkins


Configure Jenkins Pipeline:

Create a new pipeline job.

Set Pipeline script from SCM → Git → repo URL.

Branch: master (or main).

Credential: Jenkins Docker Hub credentials (dockerhub).

Push initial commit if needed:

git add .
git commit -m "Initial commit"
git push -u origin master


Run pipeline:

Click Build Now in Jenkins.

Verify stages execute successfully: Checkout → Build → Test → Push → Deploy.

Notes

Use --password-stdin in the pipeline for Docker login to keep credentials secure.

Ensure the branch in Jenkins matches the branch on GitHub.

Docker Compose will deploy containers in detached mode (-d).
