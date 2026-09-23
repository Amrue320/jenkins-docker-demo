# Jenkins CI/CD Task - Short Report

## Objective

Set up Jenkins locally on Windows, connect Jenkins to a GitHub repository, create a Jenkinsfile-based pipeline, run automated tests, build a Docker image, and prepare the project for pushing the image to Docker Hub.

## Tools Used

- Jenkins
- GitHub
- Git for Windows
- Docker Desktop
- Python
- Pytest
- Docker Hub

## Pipeline Stages

### Checkout
Jenkins checks out the project source code from GitHub.

### Build
Jenkins installs the Python dependency and prepares the application.

### Test
Jenkins runs the automated pytest test.

### Package
Jenkins copies the application files into a package directory.

### Docker Build
Jenkins builds the Docker image from the Dockerfile.

### Docker Push
The pipeline can push the Docker image to Docker Hub after Jenkins credentials are configured.

## Environment Variables

The Jenkinsfile uses:

- IMAGE_NAME
- IMAGE_TAG
- DOCKER_REGISTRY

Docker Hub credentials should be stored in Jenkins Credentials rather than hard-coded in the Jenkinsfile.

## Blue-Green Deployment

Blue-Green deployment maintains two application environments. The current version runs in Blue while the new version is deployed and tested in Green. Traffic can then be switched to Green.

## Rolling Deployment

Rolling deployment updates application instances gradually rather than replacing every instance at once. This can reduce service interruption during an update.

## Required Screenshots

1. Jenkins pipeline/stage screenshot
2. Successful Jenkins build screenshot
3. Docker Hub image screenshot
4. GitHub repository screenshot if required by the instructor

## Conclusion

The project demonstrates a basic Jenkins CI/CD workflow from source-code checkout through testing and Docker image creation, with Docker Hub integration prepared through Jenkins credentials.
