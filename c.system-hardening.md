# System Hardening (15%)


The "system hardening" section is all about making sure the computers running the Kubernetes cluster are as secure as possible. We'll talk about things that are really important in Linux, like turning off certain services and getting rid of unnecessary software, handling user and group accounts, blocking off ports, and setting up firewalls. Plus, we'll dive into tools for making the Linux kernel tougher, which help limit what a program running in a container can do on the computer itself.


- [x] Minimizing the host OS footprint

- [x] Minimizing IAM roles

- [x] Minimizing external access to the network

- [x] Using kernel hardening tools like AppArmor and seccomp

    - [AWS > Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

    - [GCP - Using IAM securely](https://cloud.google.com/iam/docs/using-iam-securely)

    - [Azure > Best practices for Azure RBAC](https://docs.microsoft.com/en-us/azure/role-based-access-control/best-practices)

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

    - [Kubernetes Documentation > Tutorials > Security > Restrict a Container's Access to Resources with AppArmor](https://kubernetes.io/docs/tutorials/security/apparmor/)

    - [Kubernetes Documentation > Tutorials > Security > Restrict a Container's Syscalls with seccomp](https://kubernetes.io/docs/tutorials/security/seccomp/)
    
    - [AppArmor Documentation](https://gitlab.com/apparmor/apparmor/-/wikis/Documentation)