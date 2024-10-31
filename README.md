# docker-containerization-and-orchestration

## This project guide how to containerize a simple static HTML and CSS web application using Docker and deploy it to a Kubernetes cluster using kind. 

## By following this guide, users will learn how to create a Dockerfile, build a Docker image, push it to Docker Hub, set up a Kubernetes cluster using kind, deploy the Docker image to the cluster, and expose the application using a Kubernetes service.

#### Create a new directory: "mkdir nomolosapp"

#### Change directory into the new directory: "cd nomolosapp"

#### Inside the directory, create an HTML file (index.html) and CSS file (style.css): "touch index.html style.css"

#### Initialize a Git repository in the project directory: "git init"

#### Add and commit the initial code to the Git repository: "git add . git commit -m "Initial commit"

#### Create a Dockerfile specifying Nginx as the base image:

Create a new file called `Dockerfile` and open it in a text editor. Add the following content to the file:

```
FROM nginx:latest
COPY index.html /usr/share/nginx/html
COPY style.css /usr/share/nginx/html
```

#### Log in to Docker Hub: "docker login"

#### Build and push the Docker image to Docker Hub:docker build -t your-dockerhub-nomoloshub/my-nginx-app .

#### Push the Docker image to Docker Hub: "docker push nomolos98/nginx:1.0.0"

#### Install kind (Kubernetes in Docker):

#### Create a kind cluster:"kind create cluster"

#### Create a Kubernetes deployment YAML file (deployment.yaml) specifying the image and desired replica count:
Create a new file called `deployment.yaml` and open it in a text editor. Add the following content to the file:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-nginx-app
  template:
    metadata:
      labels:
        app: my-nginx-app
    spec:
      containers:
      - name: my-nginx-app
        image: your-dockerhub-username/my-nginx-app
        ports:
        - containerPort: 80

#### Apply the deployment to the cluster: "kubectl apply -f deployment.yaml"

#### Create a Kubernetes service in a YAML file (service.yaml) specifying the type as ClusterIP:
Create a new file called `service.yaml` and open it in a text editor. Add the following content to the file:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nginx-service
spec:
  selector:
    app: my-nginx-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP

#### Port-forward to the service to access the application locally:"kubectl port-forward service/my-nginx-service 8080:80"

#### Open the browser and visit `http://localhost:8080` to view the simple frontend application.

