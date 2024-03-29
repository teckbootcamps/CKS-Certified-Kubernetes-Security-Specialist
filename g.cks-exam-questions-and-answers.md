
# CKS EXAM QUESTION 

## Enable Audit logs 

Enable Audit logs for the Kubernetes API server of your cluster.
There is an existing configuration file stored in your master node at /etc/kubernetes/audit/policy.yaml.
Add a policy to the configuration so that audit logs contain metadata for all resources. Additionally, it should log the request body for configmap resources.
Change the configuration of the Kube API Server to enable audit logging using the policy configuration created above. Write logs to the path /var/log/audit/audit.log.

<details><summary>Show Answer</summary>
<p>

The first part of the task is to configure the audit policy so that audit logs will contain metadata of all requests and request body of requests to config. We can accomplish this using this policy configuration:

STEP 1 : Kubernetes audit log configuration file ######

``` yaml
 /etc/kubernetes/audit/policy.yaml
# Log all requests at the Metadata level.
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
- level: Metadata
# Log configmap and secret changes in all other namespaces at the Metadata level.
- level: Request
  resources:
  - group: ""
    resources: ["configmaps"]

```
STEP 2 : Configure Kube API server for audit logs ######

#The second step of the task is to configure the Pod for the Kubernetes API server. You can change the API server’s configuration by editing its manifest. Usually, it is stored at /etc/kubernetes/manifests/kube-api-server.yaml on the master nodes.

We need to:

 +Configure the log path
 +Configure the path to the audit policy configuration file
 +Mount the audit policy to the Kube API server
 +Mount the logs directory

First, add the following additional arguments:

``` bash
--audit-policy-file=/etc/kubernetes/audit/policy.yaml
--audit-log-path=/var/log/audit/audit.log

```

Then add volumes to the pod description:

``` yaml
  volumes:
  - hostPath:
      path: /var/log/audit
      type: DirectoryOrCreate
    name: audit-logs
  - hostPath:
      path: /etc/kubernetes/audit/policy.yaml
      type: File

# Next, add the volumeMounts and apply the new configuration:

    volumeMounts:
    - mountPath: /var/log/audit
      name: audit-logs
      readOnly: false
    - mountPath: /etc/kubernetes/audit/policy.yaml
      name: audit-policy
      readonly: true
 ```     
      
You can check that logs are written by running the following on your node:

``` bash
cat /var/log/audit/audit.log
``` 

</p>
</details>

## Create a pod and attach a secret to it as a volume :

<details><summary>Show Answer</summary>
<p>

``` bash
kubectl create secret generic cks-exam-secret2 -n teckbootcamps-dev \
--from-literal=client-id=cks-username2 \
--from-literal=client-secret='Secret2022:)'
```

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: teckbootcamps-pod
  namespace: teckbootcamps-dev
spec:
  containers:
  - name: teckbootcamps-container
    image: nginx
    volumeMounts:
    - name: my-secret-volume
      mountPath: "/etc/secret/2022"
      readOnly: true
  volumes:
  - name: my-secret-volume
    secret:
      secretName: cks-exam-secret2
```

``` bash
k exec teckbootcamps-pod -n teckbootcamps-dev -- cat /etc/secret/2022/client-id
k exec teckbootcamps-pod  -n teckbootcamps-dev -- cat /etc/secret/2022/client-secret
```

</p>
</details>



