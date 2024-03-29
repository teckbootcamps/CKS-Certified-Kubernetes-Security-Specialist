# ☸️ Certified Kubernetes Security Specialist (CKS) Study Guide 2024

<p align="center">
  <img src="assets/cks.png" alt="CKS EXAM">
</p>

The [Certified Kubernetes Security Specialist (CKS) certification](https://www.cncf.io/certification/cks/)  program provides assurance that a CKS has the skills, knowledge, and competence on a broad range of best practices for securing container-based applications and Kubernetes platforms during build, deployment and runtime. CKA certification is required to sit for this exam.

 
Not sure where to start? You may consider reviewing our suggested CKS learning path.

EXAM SIMULATOR! Learners will now have access to an exam simulator, provided by Killer.sh, to experience the exam environment. You will have two exam simulation attempts (36 hours of access for each attempt from the start of activation).
Simulation includes 20-25 questions (which are exactly the same for every attempt and every user (unlike those found on the actual exams) and graded simulation results).

UPCOMING POLICY CHANGE: Please note that our Certification Period Policy is changing effective April 01, 2024, 00:00UTC. Certifications achieved on or after this date will expire 24 months from the date the program certification requirements, including passing the exam, are met. We encourage anyone interested and prepared to schedule and take your exam before the policy change. Please see additional details here.

* 📚 [Mohamed BEN HASSINE: Guide to Certified Kubernetes Security Specialist (CKS) ](https://teckbootcamps.com/cks-exam-study-guide/)<sup>Blog</sup>

# Register for the CKS Certification [Save 20% Today]
To begin your journey of becoming a Certified Kubernetes Administrator(CKS) – start by registering for the CKS exam on the Linux Foundation portal. When you register you get free access to two sessions of killer.sh CKS practice exams that will help you clear the CKS exam.

Register today and use our exclusive coupon code TECK20 for the CKS exam to get a 20% discount on CKS (and KCNA, CKAD, and CKA certifications ). This code "TECK20" expires soon.

- [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)<sup>Github</sup>

💰💰 [GET 20% OFF ON KUBERNETES CKS VOUCHER $395 --> $316](https://teckbootcamps.com/linux-foundation-coupons/#%f0%9f%94%a5-20-off-kubernetes-certification-coupon-ckad-cka-cks-running-now)<sup>Blog</sup>


<p align="center">
  <img src="assets/voucher.png" alt="CKS EXAM Voucher">
</p>

📚 [GET Kubernetes 1.29 New features (Blog Post): ](https://teckbootcamps.com/an-overview-of-new-features-in-kubernetes-v1-29/) 

# CKS Exam Syllabus (Kubernetes 1.29) 
- [Cluster Setup - 10%](a.cluster-setup.md)
- [Cluster Hardening - 15%](b.cluster-hardening.md)
- [System Hardening - 15%](c.system-hardening.md)
- [Minimize Microservice Vulnerabilities - 20%](d.minimize-microservice-vulnerabilities.md)
- [Supply Chain Security - 20%](e.supply-chain-security.md)
- [Monitoring, Logging and Runtime Security - 20%](f.monitoring-logging-and-runtime-security.md)


# Additional Resources
* 💬 [Kubernetes Slack Channel #certifications](https://kubernetes.slack.com/)<sup>Slack</sup>
* 📚 [Mohamed BEN HASSINE: Guide to Certified Kubernetes Administrator (CKA)](https://teckbootcamps.com/cka-exam-study-guide/)<sup>Blog</sup>
* 📚 [Mohamed BEN HASSINE: Guide to Certified Kubernetes Security Specialist (CKS) ](https://teckbootcamps.com/cks-exam-study-guide/)<sup>Blog</sup>
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

# 💬 Author
* 👨 🇹🇳 [Aboute ME : Mohamed BEN HASSINE](https://teckbootcamps.com/about-me/)<sup>Blog</sup>
* 👨 [Contact ME in LinkedIn ](https://www.linkedin.com/in/mohamedbnhassine/)<sup>LinkedIn</sup>
* 👨 [Find ME in Medium ](https://medium.com/@teckbootcamps)<sup>Medium</sup>
* ☸ ☸ 3X Certified Kubernetes([CKAD](https://teckbootcamps.com/ckad-exam-study-guide/)<sup>Blog</sup>, [CKA](https://teckbootcamps.com/cka-exam-study-guide//)<sup>Blog</sup> ,[CKS](https://teckbootcamps.com/cks-exam-study-guide/)<sup>Blog</sup>)
* ☁️ ☁️ Google Cloud Solutions Architect ||  [4X certified GCP Cloud](https://www.credential.net/profile/mohamedbenhassine968370/wallet)<sup>Certifications</sup>
* 👨🏼‍💻 👨🏼‍💻 14+ years of experience in the tech