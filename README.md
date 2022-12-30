# equiz-chart
Helm chart for E-Quiz.


# Building and pushing custom images

Build the docker image from the "docker" folder
Build the jobeinabox image from https://github.com/dive4dec/jobeinabox
Push the images to localhost or dockerhub

Exmaple of building the moodle image and push to localhost:
```
docker build --no-cache -t localhost:32000/bitnami_moodle_custom:test1 .
docker push localhost:32000/bitnami_moodle_custom:test1
```

# Setup a Moodle instance using Kubernetes

Go to helm-chart folder

Create a new namespace
```
kubectl create namespace my_namespace
```
Modify the following filed in the `helm_chart/values.yaml` to your own image name, domain name, URL.
```
#Image
moodle.image.registry
moodle.image.repository
moodle.image.tag
#Domain Name and URL
moolde.image.websiteUrl
moodle.ingress.hostname
moodle.ingress.path
```









