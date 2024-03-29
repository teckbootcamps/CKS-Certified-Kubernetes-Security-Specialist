
# Minimizing Microservice Vulnerabilities (20%)

In a Kubernetes cluster, the apps we run usually follow a microservices architecture. The part about "minimizing microservice vulnerabilities" focuses on making sure security settings are tight at the Pod level. We'll look into Kubernetes' own security features and some external tools that help keep things tight. Also, we're going to discuss how to securely encrypt the communication between Pods that run these microservices.

- [x] Setting up appropriate OS-level security domains with security contexts, Pod Security Admission (PSA), and Open Policy Agent Gatekeeper

- [x] Managing Secrets

- [x] Using container runtime sandboxes, such as gVisor and Kata Containers

- [x] Implementing Pod-to-Pod communication encryption via mutual Transport Layer Security (TLS)

    - [Kubernetes Documentation > Concepts > Security > Pod Security Policies](https://kubernetes.io/docs/concepts/security/pod-security-policy/#what-is-a-pod-security-policy)
    
    - [Kubernetes Blog > OPA Gatekeeper: Policy and Governance for Kubernetes](https://kubernetes.io/blog/2019/08/06/opa-gatekeeper-policy-and-governance-for-kubernetes/)

    - [Kubernetes Documentation > Tasks > Configure Pods and > Containers > Configure a Security Context for a Pod or Container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

    - [Kubernetes Documentation > Concepts > Configuration > Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

    - [Kubernetes Documentation > Concepts > Security > Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/#what-about-sandboxed-pods)

    - [Kubernetes Documentation > Concepts > Containers > Runtime Class](https://kubernetes.io/docs/concepts/containers/runtime-class/)

    - [gvisor](https://gvisor.dev/docs/user_guide/quick_start/kubernetes/)

    - [kata containers](https://katacontainers.io/)
    
    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress > TLS](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)
