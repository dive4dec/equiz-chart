# Equiz-chart
Helm chart for E-Quiz.

## Setup a E-quiz instance using Kubernetes

### Prerequisite
- Kubernetes
- Helm

### Build subchart dependencies
Equiz helm chart is based on Bitnami Moodle, before install the instance, Clone this repo into your machine and build subchart dependencies by running the following command in terminal:
```
helm dependency update
```

Modify the following field in the `values.yaml` to use your own domain name, URL, images, if applicable.
```
#Images
moodle.image.registry
moodle.image.repository
moodle.image.tag
Jobe.jobeImage

#Domain Name and URL
moolde.image.websiteUrl
moodle.ingress.hostname
moodle.ingress.path
```

Create a new namespace
```
kubectl create namespace my_namespace
```
Install a new helm release
```
sudo helm install release1 --debug . --values values.yaml --namespace=my_namespace
```
Access it at your configured url, please note that the E-quiz instance may takes few minutes to initialize.

The default Login information for admin:
```
admin-custom
admin123
```
## E-quiz moodle configuration

After E-quiz is initialized, go to Site administration and perform the following configuration.

### LTI
Go to Plugins->Authentication->Manage authentication, Enable LTI

Go to Plugins->Enrolments->Manage enrol plugins, Enable Publish as LTI tool


### Jobeinabox
Go to Plugins->Question types->CodeRunner,
Modify the field "Jobe server" to "jobe",
Modify the field "Jobe API-key" to be blank.

Go to General->Security->HTTP security,
Modify the field "cURL blocked hosts list" to be blank.

### Maxima
Go to Plugins->Question types->STACK
Modify the field "Maxima version" to the latest version (currently 5.44.0).

## Building and pushing the custom images (if you want to use customized images)

Build the docker image from the "docker" folder<br />

Build the Jobeinabox image from https://github.com/dive4dec/jobeinabox<br />

Push the images to localhost or dockerhub<br />

Example of building the moodle image and push to localhost:
```
docker build --no-cache -t localhost:32000/bitnami_moodle_custom:test1 .
docker push localhost:32000/bitnami_moodle_custom:test1
```

Example of building the moodle image and push to dockerhub:
```
docker build --no-cache -t <dockerhub account>/<dockerhub repo>:<tag> .
docker push <dockerhub account>/<dockerhub repo>:<tag>
```
















