# Kubernetes Pod Creation and Troubleshooting Guide
This repository showcases the tasks completed using Kubernetes to create, modify, and troubleshoot pods.

## Task 1: Create an NGINX Pod Using Imperative Command
Run the following command to create an nginx pod using the nginx image:

``` kubectl run nginx --image=nginx ```

## Task 2: Generate and Modify YAML
1.Extract the YAML from the created nginx pod:
 
 ``` kubectl get pod nginx -o yaml > nginx-pod.yaml ```

2.Modify the pod name in the YAML file to nginx-new:

 ``` apiVersion: v1
kind: Pod
metadata:
  name: nginx-new
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```
3.Apply the new YAML to create the modified pod:
``` kubectl apply -f nginx-pod.yaml ```

 ## Task 3: Troubleshoot YAML Errors

  ### Original YAML:
 ```  apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - image: rediss
    name: redis
```

 ### Errors Encountered:
 error validating "<your-yaml-file>.yaml": error validating data: missing required field "containers" in PodSpec

### Fix:
 1.Correct the image name and indentation issues:

  ``` apiVersion: v1
kind: Pod
metadata:
  labels:
    app: test
  name: redis
spec:
  containers:
  - name: redis
    image: redis
 ```

 2.Apply the corrected YAML:
 ``` kubectl apply -f redis-pod.yaml ```

 ## Commands Used During Troubleshooting
 - Describe Pod: Get detailed information about the pod and error messages:
 ``` kubectl describe pod redis ```

 - Delete Pod: Delete a pod if needed for recreating:
 ``` kubectl delete pod redis ```