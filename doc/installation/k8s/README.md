# How to install Rockside Engine Kuberbetes

This tutorial shows you how to deploy a Rockside and a MySQL database using Minikube.
Both applications use PersistentVolumes and PersistentVolumeClaims to store data.

## Before you begin

You need to have a Kubernetes cluster, and the kubectl command-line tool must be configured to communicate with your cluster.
If you do not already have a cluster, you can create one by using Minikube.

You will need these files:

1) [db-secret.yaml](db-secret.yaml)

2) [rockside-config.yaml](rockside-config.yaml)

3) [engine-deployment.yaml](engine-deployment.yaml)

4) [scheduler-deployment.yaml](scheduler-deployment.yaml)

5) [front-deployment.yaml](front-deployment.yaml)


## Create Secrets

A Secret is an object that stores a piece of sensitive data like a password or key. The manifest files are already configured to use a Secret, but you have to create your own Secret.

### Mysql

In the db-secret.yaml file, add the base64 value of your host, password and username.

```
echo -n 'my-host' | base64
```

```
apiVersion: v1
kind: Secret
metadata:
  name: rockside-db
data:
  host: BASE_64_OF_HOST
  username: BASE_64_OF_USERNAME
  password: BASE_64_OF_PASSWORD
```

Then create your secret

```
kubectl apply -f db-secret.yaml
```

### Rockside Engine

#### Slave Token

Generate a random token

```
cat /dev/urandom | head -c 2048 | shasum | head -c 40; echo
```

You will need to replace `YOUR_TOKEN` with the token you want to use.

```
kubectl create secret generic rockside-slave-token --from-literal=token=YOUR_TOKEN
```

#### Application Key

Generate a random key

```
cat /dev/urandom | head -c 32 | base64
```

You will need to replace `YOUR_KEY` with the token you want to use.

```
kubectl create secret generic rockside-app-key --from-literal=key=base64:YOUR_KEY
```

### Rockside Front SSL Certificate

1) First generate dhparam file

```
openssl dhparam -out dhparam.pem 2048
```

... have a coffee .... or If you are hurry use the following command instead

```
openssl dhparam -dsaparam -out dhparam.pem 2048
```

2) Next, generate self signed certificate and private keys, if you have already certificate and keys, then Ignore this step.

```
openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out cert.pem
```

3) Finally, create secret with cerificate, private key and dhparam.

```
kubectl create secret generic rockside-front-certs-keys --from-file=./key.pem --from-file=./cert.pem --from-file=./dhparam.pem
```

### Private dockerhub registry

If you need to access images from a private registry, you have to create a secrect like this

```
kubectl create secret docker-registry private-docker-key --docker-username="DOCKER_USERNAME" --docker-password="DOCKER_PASSWORD" --docker-email="DOCKER_EMAIL" --docker-server="https://index.docker.io/v1/"
```

Then in your deployment, on spec of the template, add:

```
imagePullSecrets:
  - name: private-docker-key
```

## Create ConfigMap

Create a config to contains the configuration to will be shared between the different part deployment of rockside.

Edit the rockside-config.yaml file and add the url where your app will be available.

```
app_url: https://cloud.rockside.io
```
Then create your config map:

```
kubectl apply -f rockside-config.yaml
```

## Deploy Rockside Engine

1) Deploy Rockside Engine from the engine-deployment.yaml file:

```
kubectl create -f engine-deployment.yaml
```

2) Verify that a PersistentVolume got dynamically provisioned.

```
kubectl get pvc
```

The response should be like this:

```
NAME                      STATUS    VOLUME            CAPACITY   ACCESS MODES   STORAGECLASS   AGE
rockside-engine-pv-claim  Bound     pvc-ded5ff20...   10Gi       RWO            standard       66s
```

3) Verify that the Pod is running by running the following command:

```
kubectl get pods
```

The response should be like this:

```
NAME                     READY     STATUS       RESTARTS   AGE
engine-7bc8fcbb5-4622p   1/1       Running		0          66s
```

## Deploy Rockside Scheduler

1) Deploy Rockside Scheduler from the scheduler-deployment.yaml file:

```
kubectl create -f scheduler-deployment.yaml
```

2) Verify that the Pod is running by running the following command:

```
kubectl get pods
```

The response should be like this:

```
NAME                     READY     STATUS       RESTARTS   AGE
scheduler-7bc8fcbb5-4622p   1/1       Running		0          66s
```

## Deploy Rockside Front

1) Deploy Rockside Front from the front-deployment.yaml file:

```
kubectl create -f front-deployment.yaml
```

2) Verify that the Pod is running by running the following command:

```
kubectl get pods
```

The response should be like this:

```
NAME                     READY     STATUS       RESTARTS   AGE
front-7bc8fcbb5-4622p    1/1       Running		0          66s
```

## Configure SMTP server

Define for the engine container the following environment variables:

```
MAIL_HOST=
MAIL_PORT=
MAIL_ENCRYPTION=
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_FROM_ADDRESS=notification@rockside.io
MAIL_FROM_NAME=rockside
```







