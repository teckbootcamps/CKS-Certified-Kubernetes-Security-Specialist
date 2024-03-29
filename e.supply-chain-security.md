
# Supply Chain Security (20%)

Earlier sections focused on securing the Kubernetes environment and operations with existing images. Now, we shift to designing, building, and improving container images. Sometimes, you might use a container image made by others. It’s crucial to scan these images for vulnerabilities before deployment. We’ll explore ways to vet these pre-built images for security risks, touching on methods important for the CKS exam.


- [x] Minimizing base image footprint

- [x] Securing the supply chain

- [x] Using static analysis of user workload

- [x] Scanning images for known vulnerabilities


    - [Kubernetes Documentation > Reference > API Access Control > Using Admission Controllers > ImagePolicyWebhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#imagepolicywebhook)

    - [Trivy](https://github.com/aquasecurity/trivy)

