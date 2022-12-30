# Equiz-chart
Helm chart for E-Quiz.

## Building and pushing custom images

Build the docker image from the "docker" folder
Build the Jobeinabox image from https://github.com/dive4dec/jobeinabox
Push the images to localhost or dockerhub

Exmaple of building the moodle image and push to localhost:
```
docker build --no-cache -t localhost:32000/bitnami_moodle_custom:test1 .
docker push localhost:32000/bitnami_moodle_custom:test1
```

## Setup a Moodle instance using Kubernetes

Go to helm-chart folder

Modify the following filed in the `helm_chart/values.yaml` to your own Moodle and Jobeinabox image name, domain name, URL.
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
Access it at your configured url, please note that the moodle instance may takes few minutes to initialize.

# Moodle configuration

After moodle is initialized, go to Site administration and perform the following configuration.

###LTI
Go to Plugins->Authentication->Manage authentication, Enable LTI
Go to Plugins->Enrolments->Manage enrol plugins, Enable Publish as LTI tool


###Jobeinabox
Go to Plugins->Question types->CodeRunner,
Modify the field Jobe server" to "jobe",
Modify the Jobe API-key to be blank.

Go to General->Security->HTTP security,
Modify the cURL blocked hosts list to be blank.

















