[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

# ☸️  Certified Kubernetes Security Specialist (CKS) Study Guide - V1.31 (2024)

<p align="center">
  <img src="assets/cks.png" alt="CKS EXAM">
</p>

> This guide is part of our blog [Guide to Certified Kubernetes Security Specialist (CKS)  ](https://teckbootcamps.com/cks-exam-study-guide/).

## Hit the Star! :star:
> If you are using this repo for guidance, please hit the star. Thanks A lot !


The [Certified Kubernetes Security Specialist (CKS) certification](https://training.linuxfoundation.org/certification/certified-kubernetes-security-specialist/)  program provides assurance that a CKS has the skills, knowledge, and competence on a broad range of best practices for securing container-based applications and Kubernetes platforms during build, deployment and runtime. CKA certification is required to sit for this exam.

## CKS Exam details (v1.31  2024 ) 

| **CKA Exam Details**                     | **Information**                                                                                     |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Exam Type**                             | Performance Based NOT MCQ )                                    |
| **Exam Duration**                         | 2 hours                                                                                            |
| **Pass Percentage**                       | 66%  ( One Retake )                                                                                             |
| **CKS Exam Kubernetes Version**          | [Kubernetes v1.31](#cks-exam-syllabus-updated-kubernetes-131-2024)                                                                               |
| **CKS Validity**                         | 2 Years  |
| **Exam Cost**                            | $395 USD ([GET 30% OFF CKA Exam Coupon](https://github.com/teckbootcamps/linux-foundation-coupon?tab=readme-ov-file#-30-off-kubernetes-certification-coupon-ckad--cka--cks)) 💥INCREASE PRICE:  $434 in January 2025         |



## [30% OFF]  CKA Exam Coupon

Save 30% using Coupon code **TECK30** on all the Linux Foundation training and certification programs. This is a limited-time offer for this month. This offer is applicable for CKA, CKAD, CKS, KCNA, LFCS, PCA FINOPS, NodeJS, CHFA, and all the other certification, training, and BootCamp programs.

> Kubernetes CKS VOUCHER ($395 —> $276): [teckbootcamps-30%off/cks](https://teckbootcamps.com/go/cks-exam-2024/)


## CKS Exam Syllabus (Updated Kubernetes 1.31)

| **Topic**                           | **Concepts**                                                                                                                                                               | **Weightage** |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| [**1. Cluster Setup - 15%**](#1-cluster-setup-15)                   | - Use Network security policies to restrict cluster-level access<br>- Use CIS benchmark to review the security configuration of Kubernetes components (etcd, kubelet, kubedns, kubeapi)<br>- Properly set up Ingress with TLS<br>- Protect node metadata and endpoints<br>- Verify platform binaries before deploying | 15%          |
| [**2. Cluster Hardening - 15%**](#2-cluster-hardening-15)               | - Use Role-Based Access Controls to minimize exposure<br>- Exercise caution in using service accounts (e.g., disable defaults, minimize permissions on newly created ones)<br>- Restrict access to Kubernetes API<br>- Upgrade Kubernetes to avoid vulnerabilities | 15%          |
| [**3. System Hardening - 10%**](#3-system-hardening-10)                | - Minimize host OS footprint (reduce attack surface)<br>- Use least-privilege identity and access management<br>- Minimize external access to the network<br>- Appropriately use kernel hardening tools such as AppArmor, seccomp | 10%          |
| [**4. Minimize Microservice Vulnerabilities - 20%**](#4-minimize-microservice-vulnerabilities-20) | - Use appropriate pod security standards<br>- Manage Kubernetes secrets<br>- Understand and implement isolation techniques (multi-tenancy, sandboxed containers, etc.)<br>- Implement Pod-to-Pod encryption using Cilium | 20%          |
| [**5. Supply Chain Security - 20%**](#5-supply-chain-security-20)           | - Minimize base image footprint<br>- Understand your supply chain (e.g., SBOM, CI/CD, artifact repositories)<br>- Secure your supply chain (permitted registries, sign and validate artifacts, etc.)<br>- Perform static analysis of user workloads and container images (e.g., Kubesec, KubeLinter) | 20%          |
| [**6. Monitoring, Logging and Runtime Security - 20%**](#6-monitoring-logging-and-runtime-security-20) | - Perform behavioral analytics to detect malicious activities<br>- Detect threats within physical infrastructure, apps, networks, data, users, and workloads<br>- Investigate and identify phases of attack and bad actors within the environment<br>- Ensure immutability of containers at runtime<br>- Use Kubernetes audit logs to monitor access | 20%          |


# 1. Cluster Setup (15%)

This domain constitutes 15% of the CKS Exam. Below are the key topics explained with examples and best practices to secure your Kubernetes cluster.

### Use Network Security Policies to Restrict Cluster Level Access
> NetworkPolicies control communication between Pods and network endpoints, enforcing security rules.

#### Example:
> **Create a NetworkPolicy to Deny All Traffic Except from Specific Pods:**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: restrict-access
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: backend
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: frontend
    ports:
    - protocol: TCP
      port: 8080
```
```bash
kubectl apply -f networkpolicy.yaml
```

> **Verify NetworkPolicy:**
```bash
kubectl describe networkpolicy restrict-access
```

- [Learn more about NetworkPolicies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

### Use CIS Benchmark to Review the Security Configuration of Kubernetes Components
> The Center for Internet Security (CIS) benchmarks provide best practices for securing Kubernetes.

#### Example:
> **Run CIS Benchmark Tools:**
> - Use tools like [kube-bench](https://github.com/aquasecurity/kube-bench) to audit the security configurations.

```bash
kube-bench run --targets etcd,kubelet,kubeapi
```
**Manually Review Security Settings:**
- **Etcd:** Ensure encryption at rest and restricted access.
- **Kubelet:** Restrict anonymous access (`--anonymous-auth=false`).
- **API Server:** Enable RBAC and audit logging.

> - [Learn more about CIS Benchmarks](https://www.cisecurity.org/benchmark/kubernetes/)

### Properly Set Up Ingress with TLS
> Ingress with TLS secures HTTP communication to services.

#### Example:
> **Create a Secret for TLS:**
```bash
kubectl create secret tls tls-secret --cert=cert.crt --key=cert.key
```

> **Configure Ingress Resource with TLS:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: tls-example
spec:
  tls:
  - hosts:
    - example.com
    secretName: tls-secret
  rules:
  - host: example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```
```bash
kubectl apply -f ingress-tls.yaml
```
> **Test Ingress:**
```bash
curl -k https://example.com
```

> - [Learn more about TLS with Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)

### Protect Node Metadata and Endpoints
> Securing node metadata prevents unauthorized access to sensitive information.

#### Best Practices:
> - **Disable Metadata APIs for Pods:**
  Use `--enable-metadata-concealment` in cloud providers like GKE.
> - **Restrict Access to Node Endpoints:**
  Set firewall rules to limit access.

#### Example:
> **Block Metadata Access with iptables:**
```bash
iptables -A OUTPUT -d 169.254.169.254 -j DROP
```

> - [Learn more about protecting metadata](https://cloud.google.com/kubernetes-engine/docs/how-to/protecting-cluster-metadata)

### Verify Platform Binaries Before Deploying
> Ensuring the integrity of platform binaries mitigates risks of tampered software.

#### Best Practices:
> - Use package managers to verify binary checksums.
> - Always download binaries from official sources.

#### Example:
> **Verify Binary Checksum:**
```bash
curl -LO https://dl.k8s.io/release/v1.24.0/bin/linux/amd64/kubectl
curl -LO https://dl.k8s.io/release/v1.24.0/bin/linux/amd64/kubectl.sha256
sha256sum --check kubectl.sha256
```

> - [Learn more about binary verification](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#verify-kubectl-binary)

---

### Resources to Prepare
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
> - [CKS Exam Tips](https://kubernetes.io/docs/certifications/)


# 2. Cluster Hardening (15%)
> This domain constitutes 15% of the CKS Exam. Below are the key topics explained with examples and best practices to harden your Kubernetes cluster.

### Use Role-Based Access Controls (RBAC) to Minimize Exposure
> RBAC ensures that users and applications have only the permissions they need.

#### Example:
> **Create a Role with Minimal Permissions:**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
```
> **Create a RoleBinding to Assign the Role:**
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: default
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```
```bash
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
```

> - [Learn more about RBAC](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

### Exercise Caution in Using Service Accounts
> By default, service accounts may have more privileges than necessary. Disable or restrict these accounts to improve security.

#### Best Practices:
> - **Disable the Default Service Account:**
```bash
kubectl patch serviceaccount default -p '{"automountServiceAccountToken":false}'
```
- **Create a Service Account with Limited Permissions:**
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: limited-sa
  namespace: default
```
```bash
kubectl apply -f serviceaccount.yaml
```
> - **Associate the Service Account with a Role:**
> Refer to the RBAC example above to link this service account to minimal permissions.

> - [Learn more about Service Accounts](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)

### Restrict Access to Kubernetes API
> Limiting access to the Kubernetes API minimizes the risk of unauthorized actions.

#### Best Practices:
> - **Restrict API Server Access by IP Address:**
```bash
kubectl create clusterrolebinding restricted-access --clusterrole=view --user=<your-user>
```
- **Use Network Policies to Block API Access:**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: restrict-api-access
  namespace: kube-system
spec:
  podSelector:
    matchLabels:
      component: kube-apiserver
  ingress:
  - from:
    - ipBlock:
        cidr: 192.168.1.0/24
```
```bash
kubectl apply -f networkpolicy.yaml
```

> - [Learn more about securing API access](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/)

### Upgrade Kubernetes to Avoid Vulnerabilities
> Regularly upgrading Kubernetes ensures that you benefit from security patches and new features.

#### Best Practices:
> - **Check Current Version:**
```bash
kubectl version --short
```
> - **Plan and Execute an Upgrade:**
  1. Drain worker nodes:
     ```bash
     kubectl drain <node-name> --ignore-daemonsets
     ```
  2. Upgrade control plane components using your cluster manager (e.g., kubeadm, cloud provider tools).
  3. Upgrade worker nodes:
     ```bash
     kubectl uncordon <node-name>
     ```

> - [Learn more about upgrading Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/cluster-upgrade/)

---

### Resources to Prepare
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
> - [CKS Exam Tips](https://kubernetes.io/docs/certifications/)


# 3. System Hardening (10%)

> This domain constitutes 10% of the CKS Exam. Below are the key topics explained with examples and best practices to harden your system.

### Minimize Host OS Footprint (Reduce Attack Surface)
> A minimal host OS reduces the attack surface by limiting unnecessary services and applications.

#### Best Practices:
> - Use minimal OS distributions like **Container-Optimized OS**, **Flatcar**, or **Ubuntu Minimal**.
> - Remove unused software and disable unnecessary services.

#### Example:
> **Install a Minimal OS on a Node:**
```bash
# For Container-Optimized OS (GCP)
gcloud compute instances create <instance-name> --image-family=cos-stable --image-project=cos-cloud
```
> - [Learn more about Container-Optimized OS](https://cloud.google.com/container-optimized-os/docs)

### Use Least-Privilege Identity and Access Management
> Ensure that users and applications have only the permissions they need.

#### Example:
> **Restrict IAM Permissions for Cloud Resources:**
```bash
# GCP Example: Assign minimal roles to Kubernetes Engine
gcloud projects add-iam-policy-binding <project-id> --member=<user> --role=roles/container.viewer
```
> **Limit Privileges in Kubernetes:**
Use Role-Based Access Control (RBAC) as shown in the "Cluster Hardening" section to restrict permissions for users and service accounts.

> - [Learn more about IAM Best Practices](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

### Minimize External Access to the Network
> Restrict external access to nodes and Kubernetes resources to reduce exposure.

#### Best Practices:
> - Use firewall rules to limit external access.
> - Disable SSH access to nodes if possible.
> - Restrict access to specific IP ranges using network policies.

#### Example:
> **Create Firewall Rules to Restrict Access:**
```bash
# GCP Example: Block all ingress traffic except from trusted IP ranges
gcloud compute firewall-rules create restrict-access --direction=INGRESS --priority=1000 --action=DENY --rules=all --source-ranges=0.0.0.0/0
```
> **Apply Network Policies:**
> Refer to the "Cluster Hardening" section for examples of network policies to restrict access to Kubernetes resources.

> - [Learn more about securing networks](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

### Appropriately Use Kernel Hardening Tools (e.g., AppArmor, seccomp)
> Kernel hardening tools like **AppArmor** and **seccomp** restrict what system calls and resources a container can access.

#### Example:
> **Use seccomp to Restrict System Calls:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: seccomp-demo
  annotations:
    seccomp.security.alpha.kubernetes.io/pod: 'runtime/default'
spec:
  containers:
  - name: app-container
    image: busybox
    command: ["sh", "-c", "echo Hello Kubernetes! && sleep 3600"]
```
```bash
kubectl apply -f seccomp-demo.yaml
```

> **Apply AppArmor Profiles:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: apparmor-demo
  annotations:
    container.apparmor.security.beta.kubernetes.io/app-container: runtime/default
spec:
  containers:
  - name: app-container
    image: nginx
```
```bash
kubectl apply -f apparmor-demo.yaml
```

> - [Learn more about seccomp](https://kubernetes.io/docs/tutorials/clusters/seccomp/)
> - [Learn more about AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/)

---

### Resources to Prepare
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
> - [CKS Exam Tips](https://kubernetes.io/docs/certifications/)


# 4. Minimize Microservice Vulnerabilities (20%)
> This domain constitutes 20% of the CKS Exam. Below are the key topics explained with examples and best practices to minimize vulnerabilities in microservices.

### Use Appropriate Pod Security Standards
> Pod security standards (PSS) define best practices for securing Pods by restricting capabilities and enforcing security policies.

#### Example:
> **Apply a PodSecurity Admission Policy (restricted):**
```yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: restricted
spec:
  privileged: false
  runAsUser:
    rule: MustRunAsNonRoot
  seLinux:
    rule: RunAsAny
  supplementalGroups:
    rule: MustRunAs
    ranges:
    - min: 1
      max: 65535
  fsGroup:
    rule: MustRunAs
    ranges:
    - min: 1
      max: 65535
  volumes:
  - 'configMap'
  - 'emptyDir'
  - 'projected'
  - 'secret'
```
```bash
kubectl apply -f podsecuritypolicy.yaml
```
> - [Learn more about Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/)

### Manage Kubernetes Secrets
> Secrets store sensitive data like passwords, tokens, and keys, and should be managed securely.

#### Example:
> **Create and Consume a Secret:**
```bash
kubectl create secret generic db-credentials --from-literal=username=admin --from-literal=password=secret123
```
> **Use the Secret in a Pod:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-demo
spec:
  containers:
  - name: app-container
    image: nginx
    env:
    - name: DB_USERNAME
      valueFrom:
        secretKeyRef:
          name: db-credentials
          key: username
    - name: DB_PASSWORD
      valueFrom:
        secretKeyRef:
          name: db-credentials
          key: password
```
```bash
kubectl apply -f secret-demo.yaml
```
> - [Learn more about Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

### Understand and Implement Isolation Techniques (Multi-Tenancy, Sandboxed Containers, etc.)
> Isolation techniques help separate workloads for security and resource management.

#### Best Practices:
> - Use Kubernetes namespaces for multi-tenancy.
> - Implement sandboxed containers with gVisor or Kata Containers.

#### Example:
> **Create a Namespace for Isolation:**
```bash
kubectl create namespace team-a
```
**Apply Resource Quotas:**
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: team-a-quota
  namespace: team-a
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: "2Gi"
```
```bash
kubectl apply -f resource-quota.yaml
```

> - [Learn more about Namespace Isolation](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/)
> - [Learn more about gVisor](https://gvisor.dev/)
> - [Learn more about Kata Containers](https://katacontainers.io/)

### Implement Pod-to-Pod Encryption Using Cilium
> Cilium enables secure communication between Pods using eBPF-based networking and encryption.

#### Example:
> **Install Cilium:**
```bash
helm repo add cilium https://helm.cilium.io/
helm install cilium cilium/cilium --namespace kube-system --set encryption.enabled=true
```

> **Enable Pod-to-Pod Encryption:**
```bash
kubectl annotate namespace default io.cilium.encryption=true
```

> **Verify Encryption:**
```bash
kubectl exec -it <pod-name> -- curl https://<target-pod-ip>
```

> - [Learn more about Cilium](https://docs.cilium.io/en/stable/)

---

### Resources to Prepare
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
> - [CKS Exam Tips](https://kubernetes.io/docs/certifications/)


# 5. Supply Chain Security (20%)
> This domain constitutes 20% of the CKS Exam. Below are the key topics explained with examples and best practices to secure your Kubernetes supply chain.

### Minimize Base Image Footprint
> Using minimal base images reduces the attack surface by limiting unnecessary software and dependencies.

#### Best Practices:
> - Use minimal base images like `distroless` or `alpine`.
> - Avoid including unused libraries and tools in your images.

#### Example:
> **Create a Dockerfile with a Minimal Base Image:**
```Dockerfile
FROM gcr.io/distroless/base
COPY app /app
CMD ["/app"]
```
> **Build and Push the Image:**
```bash
docker build -t <registry>/minimal-app:latest .
docker push <registry>/minimal-app:latest
```
> - [Learn more about distroless images](https://github.com/GoogleContainerTools/distroless)

### Understand Your Supply Chain (e.g., SBOM, CI/CD, Artifact Repositories)
> Understanding your software supply chain involves tracking the sources and dependencies of your workloads.

#### Example:
> **Generate a Software Bill of Materials (SBOM):**
> Use `syft` to generate an SBOM for your container image:
```bash
syft <registry>/minimal-app:latest -o json > sbom.json
```
> **Integrate Dependency Scanning in CI/CD:**
> Use tools like `Trivy` or `Snyk` to scan dependencies during CI/CD builds.
```bash
trivy image <registry>/minimal-app:latest
```
> - [Learn more about SBOM](https://github.com/anchore/syft)
> - [Learn more about Trivy](https://github.com/aquasecurity/trivy)

### Secure Your Supply Chain (Permitted Registries, Sign and Validate Artifacts, etc.)
> Enforcing policies for registries and artifact validation ensures secure deployment of images.

#### Example:
> **Restrict to Permitted Registries:**
> Use Admission Controllers to enforce registry restrictions:
```yaml
apiVersion: admissionregistration.k8s.io/v1
kind: ValidatingWebhookConfiguration
metadata:
  name: registry-restriction
webhooks:
- name: validate.registries.k8s.io
  clientConfig:
    service:
      name: registry-validator
      namespace: kube-system
    caBundle: <base64-encoded-ca>
  rules:
  - operations: ["CREATE"]
    resources: ["pods"]
  failurePolicy: Fail
```
> **Sign and Validate Images:**
Use `cosign` to sign and verify images:
```bash
cosign sign --key cosign.key <registry>/minimal-app:latest
cosign verify <registry>/minimal-app:latest
```
> - [Learn more about Cosign](https://github.com/sigstore/cosign)

### Perform Static Analysis of User Workloads and Container Images
> Static analysis tools help detect misconfigurations and vulnerabilities in workloads and container images.

#### Example:
> **Use KubeSec for Policy Validation:**
```bash
kubesec scan pod.yaml
```
> **Use KubeLinter for Workload Analysis:**
```bash
kubelinter lint pod.yaml
```
> **Scan Container Images for Vulnerabilities:**
```bash
trivy image <registry>/minimal-app:latest
```
> - [Learn more about KubeSec](https://kubesec.io/)
> - [Learn more about KubeLinter](https://github.com/stackrox/kube-linter)

---

### Resources to Prepare
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
> - [CKS Exam Tips](https://kubernetes.io/docs/certifications/)


# 6. Monitoring, Logging, and Runtime Security (20%)
> This domain constitutes 20% of the CKS Exam. Below are the key topics explained with examples and best practices to enhance monitoring, logging, and runtime security in Kubernetes.

### Perform Behavioral Analytics to Detect Malicious Activities
> Behavioral analytics involves monitoring application and system behavior to detect anomalies that may indicate malicious activities.

#### Example:
> **Use Falco to Detect Anomalies:**
> Falco monitors runtime behavior in Kubernetes clusters.
```bash
helm repo add falcosecurity https://falcosecurity.github.io/charts
helm install falco falcosecurity/falco --namespace kube-system
```
> **Create a Falco Rule:**
```yaml
- rule: Write Below Binary Dir
  desc: Detect any process writing below /bin or /sbin
  condition: evt.type = "write" and fd.name startswith "/bin/"
  output: "Process writing below /bin or /sbin (user=%user.name command=%proc.cmdline)"
  priority: CRITICAL
```
> - [Learn more about Falco](https://falco.org/)

### Detect Threats Within Physical Infrastructure, Apps, Networks, Data, Users, and Workloads
> Threat detection ensures a comprehensive security posture across the Kubernetes environment.

#### Example:
> **Use Sysdig to Detect Threats:**
```bash
helm install sysdig sysdig/sysdig --set sysdig.accessKey=<YOUR-ACCESS-KEY>
```
> **Enable Runtime Threat Detection:**
> Monitor threats across the cluster by configuring Sysdig or similar tools for Kubernetes.
> - [Learn more about Sysdig](https://sysdig.com/)

### Investigate and Identify Phases of Attack and Bad Actors Within the Environment
> Understanding attack phases helps in identifying and mitigating threats effectively.

#### Example:
> **Use EFK (Elasticsearch, Fluentd, Kibana) Stack to Investigate Attacks:**
- Deploy EFK to aggregate and visualize logs.
```bash
helm install efk elasticsearch fluentd kibana --namespace monitoring
```
> - Analyze logs in Kibana to track suspicious activity.

> - [Learn more about Kubernetes Logging](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

### Ensure Immutability of Containers at Runtime
> Immutability ensures that containers remain unchanged during runtime, preventing unauthorized modifications.

#### Example:
> **Use Read-Only Root Filesystem:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: immutable-container
spec:
  containers:
  - name: app
    image: my-app:latest
    securityContext:
      readOnlyRootFilesystem: true
```
```bash
kubectl apply -f immutable-container.yaml
```
> **Use Tools to Enforce Immutability:**
> Enable runtime immutability with tools like Falco and Sysdig.

> - [Learn more about Immutability](https://kubernetes.io/docs/concepts/policy/security-context/)

### Use Kubernetes Audit Logs to Monitor Access
> Audit logs provide detailed records of cluster activities, helping to monitor and investigate access.

#### Example:
> **Enable Kubernetes Audit Logging:**
> Edit the `kube-apiserver` configuration to enable audit logging:
```yaml
--audit-log-path=/var/log/kubernetes/audit.log
--audit-policy-file=/etc/kubernetes/audit-policy.yaml
```
> **Create an Audit Policy:**
```yaml
apiVersion: audit.k8s.io/v1
kind: Policy
rules:
- level: Metadata
  resources:
  - group: ""
    resources: ["pods"]
```
> **View Audit Logs:**
```bash
kubectl logs -n kube-system kube-apiserver
```
> - [Learn more about Audit Logs](https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/)

---

### Resources to Prepare
> - [Kubernetes Documentation](https://kubernetes.io/docs/)
> - [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
> - [CKS Exam Tips](https://kubernetes.io/docs/certifications/)


# CKS Exam Questions And Answers

Practice a lot with Kubernetes:

- [CKS Exam Questions And Answers](g.cks-exam-questions-and-answers.md)


## Additional Resources
* 💬 [Kubernetes Slack Channel #certifications](https://kubernetes.slack.com/)<sup>Slack</sup>
* 📚 [Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>
* 📚 [Guide to Certified Kubernetes Security Specialist (CKS) ](https://teckbootcamps.com/cks-exam-study-guide/)<sup>Blog</sup>
* 🎞️ [Kubernetes CKS Full Course Theory + Practice + Browser Scenarios](https://www.youtube.com/watch?v=d9xfB5qaOfg)<sup>Video Course</sup>
* 🎞️ [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)<sup>Official Course</sup>
* 🎞️ [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)<sup>Video Course</sup>

## Practice
Practice a lot with Kubernetes:

- [CKS Simulator - killer.sh](https://killer.sh/cks)
- [Kubernetes the Hard Way by Kelsey Hightower](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [CKS Scenarios - killercoda.com](https://killercoda.com/killer-shell-cks)
- [Learning Playground - by Docker](https://labs.play-with-k8s.com/)



# 💬 Share To Your Network
If this repo has helped you in any way, feel free to share !
