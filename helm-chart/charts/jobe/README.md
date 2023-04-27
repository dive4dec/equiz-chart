# Jobeinabox helm chart


## Deploy the chart as stonealone app

Change the `jobeImage` value in `values.yaml` for configuring your own image name

Then, create a new namespace
```
kubectl create namespace my_namespace
```
Install a new helm release
```
sudo helm install release1 --debug . --values values.yaml --namespace=my_namespace
```

## Using the chart as subchart

Modify the following field in the root `values.yaml` to use your jobeinabox image
```
jobe:
  jobeImage: <you image name>
```

## Testing the chart
After deploying the chart, enter the pod, and run
```
python3 testsubmit.py
```
The output should be all "OK" except the pylint related items.

<br>

Access the following URL from other pods in the same node, using tool like curl
 ```
jobe/index.php/restapi/languages
 ```
The output should be a set of lanugages the jobeinabox supports.















