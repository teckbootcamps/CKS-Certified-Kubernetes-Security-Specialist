
# Minimizing Microservice Vulnerabilities (20%)

In a Kubernetes cluster, the apps we run usually follow a microservices architecture. The part about "minimizing microservice vulnerabilities" focuses on making sure security settings are tight at the Pod level. We'll look into Kubernetes' own security features and some external tools that help keep things tight. Also, we're going to discuss how to securely encrypt the communication between Pods that run these microservices.

- [x] Setting up appropriate OS-level security domains with security contexts, Pod Security Admission (PSA), and Open Policy Agent Gatekeeper

- [x] Managing Secrets

- [x] Using container runtime sandboxes, such as gVisor and Kata Containers

- [x] Implementing Pod-to-Pod communication encryption via mutual Transport Layer Security (TLS)