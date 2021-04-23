# Solution

The application is a simple employee directory app with the below three components

  1. frontend (react)
  2. backend (spring boot)
  3. database (mysql)

## Task A

1. Two dockerfiles created for frontend (Dockerfile-frontend) and backend (Dockerfile-backend).
2. Build backend jar using maven.

    Prerequisite: maven and java installed in local`

    ```bash
    $ mvn clean install -DskipTests
    ```
3. Build and push docker images for backend and frontend into dockerhub

    ```bash
    $ docker login -u <dockerhub_username> -p <dockerhub_password>
    $ docker build -t <dockerhub_username>/frontend:latest -f Dockerfile-frontend .
    $ docker push <dockerhub_username>/frontend:latest
    $ docker build -t <dockerhub_username>/backend:latest -f Dockerfile-backend .
    $ docker push <dockerhub_username>/backend:latest
    ```

## Task B

1. Have used minikube for running kubernetes in local.
2. Have deployed 3 kubernetes manifests to deploy database (db-manifest.yaml), backend (backend-manifest.yaml) and frontend (frontend-manifest.yaml) into minikube.
3. db-manifest.yaml used mysql:5.7 public image to run the database.
4. backend-manifest.yaml and frontend-manifest.yaml uses backend and frontend images build and pushed to docker hub in Task A.
5. Start minikube
    Prerequisite: minikube and kubectl installed in local

    ```bash
    $ minikube start
    ```

6. Deploying kubernetes manifests

    ```bash
    $ kubectl create namespace app
    $ kubectl apply -f db-manifest.yaml -n app
    $ kubectl apply -f backend-manifest.yaml -n app
    $ kubectl apply -f frontend-manifest.yaml -n app
    ```
7. Test

    ```bash
    $ minikube tunnel
    ```

    Get the loadbalancer IP of the frontend service by running

    ```bash
    $ kubectl get svc -n app
    ```

    And then access the URL in the browser.
