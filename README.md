# Jenkins Docker Demo

This project is designed for a local Jenkins + GitHub + Docker Desktop CI/CD assignment.

## Project files

- `app.py` - simple Python application
- `test_app.py` - automated pytest test
- `requirements.txt` - Python dependency
- `Dockerfile` - Docker image definition
- `Jenkinsfile` - Jenkins pipeline
- `.gitignore` - Git ignore rules

## Pipeline stages

1. Checkout
2. Build
3. Test
4. Package
5. Docker Build
6. Docker Push

## Run locally

```cmd
python -m pip install -r requirements.txt
python app.py
python -m pytest -v
docker build -t jenkins-docker-demo:latest .
docker run --rm jenkins-docker-demo:latest
```

## Jenkins setup notes

Create a Jenkins Pipeline job and connect it to this GitHub repository. Jenkins should use the `Jenkinsfile` from the repository.

For Docker Hub pushing, create a Jenkins username/password credential with ID:

`dockerhub-credentials`

Use a Docker Hub access token as the password rather than your normal Docker Hub password.

The Docker Push stage in this starter Jenkinsfile is intentionally left as a safe configuration placeholder. After adding your credential, uncomment the `withCredentials` block and update the job as needed.

## Deployment strategies

### Blue-Green Deployment

Blue is the currently running version and Green is the new version. The new version is deployed and tested separately, then traffic is switched from Blue to Green.

### Rolling Deployment

The application instances are updated gradually. Some instances continue serving the old version while others are updated, until all instances run the new version.
