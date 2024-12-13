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


# Additional Resources
* 💬 [Kubernetes Slack Channel #certifications](https://kubernetes.slack.com/)<sup>Slack</sup>
* 📚 [Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>
* 📚 [Guide to Certified Kubernetes Security Specialist (CKS) ](https://teckbootcamps.com/cks-exam-study-guide/)<sup>Blog</sup>
* 🎞️ [Kubernetes CKS Full Course Theory + Practice + Browser Scenarios](https://www.youtube.com/watch?v=d9xfB5qaOfg)<sup>Video Course</sup>
* 🎞️ [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)<sup>Official Course</sup>
* 🎞️ [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)<sup>Video Course</sup>

# Practice
Practice a lot with Kubernetes:

- [CKS Simulator - killer.sh](https://killer.sh/cks)
- [Kubernetes the Hard Way by Kelsey Hightower](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [CKS Scenarios - killercoda.com](https://killercoda.com/killer-shell-cks)
- [Learning Playground - by Docker](https://labs.play-with-k8s.com/)


# CKS Exam Questions And Answers

Practice a lot with Kubernetes:

- [CKS Exam Questions And Answers](g.cks-exam-questions-and-answers.md)
 

# kubectl Ninja

Tip: Use [kubectl Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) during the exam. You don't need to decorate everything.

## Useful commands or parameters during the exam:

```bash
# Use "kubectl describe" for related events and troubleshooting
kubectl describe pods <podid>

# Use "kubectl explain" to check the structure of a resource object.
kubectl explain deployment --recursive

## Add "-o wide" in order to use wide output, which gives you more details.
kubectl get pods -o wide

## Check always all namespaces by including "--all-namespaces"
kubectl get pods --all-namespaces
```

Generate a manifest template from imperative spec using the output option "-o yaml" and the parameter "--dry-run=client":

```shell
# create a service
kubectl create service clusterip my-service --tcp=8080 --dry-run=client -o yaml

# create a deployment
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml

# create a pod
kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml
```

Create resources using kubectl + stdin instead of creating them from manifest files. It helps a lot and saves time. You can use the output of the command above and modify as required:

```shell
cat <<EOF | kubectl create -f -
...
EOF
```

It saves lots of time, believe me.

Kubectl Autocomplete

```shell
source <(kubectl completion bash)
```

## TIPS

* 💬 Be fast
Use the history command to reuse already entered commands or use even faster history search through Ctrl r .

If a command takes some time to execute, like sometimes kubectl delete pod x. You can put a task in the background using Ctrl z and pull it back into foreground running command fg.

You can delete pods fast with:

``` bash
k delete pod x --grace-period 0 --force

k delete pod x $now # if export from above is configured
```

* 💬 Vim

Be great with vim.

toggle vim line numbers

When in vim you can press Esc and type :set number or :set nonumber followed by Enter to toggle line numbers. This can be useful when finding syntax errors based on line - but can be bad when wanting to mark&copy by mouse. You can also just jump to a line number with Esc :22 + Enter.

copy&paste

Get used to copy/paste/cut with vim:

``` shell
Mark lines: Esc+V (then arrow keys)
Copy marked lines: y
Cut marked lines: d
Past lines: p or P
Indent multiple lines
```

To indent multiple lines press Esc and type :set shiftwidth=2. First mark multiple lines using Shift v and the up/down keys. Then to indent the marked lines press > or <. You can then press . to repeat the action.


# 💬 Share To Your Network
If this repo has helped you in any way, feel free to share !
