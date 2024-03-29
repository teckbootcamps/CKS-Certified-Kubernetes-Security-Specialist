# Cluster Setup (10%)

The first part of the exam focuses on setting up and configuring Kubernetes clusters. In this section, we're going to talk only about the security parts, leaving out the usual tasks of a Kubernetes administrator.


- [x] Using network policies to restrict Pod-to-Pod communication

- [x] Running CIS benchmark tooling to identify security risks for cluster components

- [x] Setting up an Ingress object with TLS support

- [x] Protecting node ports, API endpoints, and GUI access

- [x] Verifying platform binaries against their checksums


    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)

    - [CIS Security > Securing Kubernetes](https://www.cisecurity.org/benchmark/kubernetes)

    - [Cloud Native Wiki - CIS Benchmark Best Practices](https://www.aquasec.com/cloud-native-academy/kubernetes-in-production/kubernetes-cis-benchmark-best-practices-in-brief/)
    
    - [GitHub > Aqua Security > kube-bench](https://github.com/aquasecurity/kube-bench)

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress > TLS](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Securing a Cluster](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/#restricting-cloud-metadata-api-access)

        ```yaml
        # all pods in namespace cannot access metadata endpoint
        apiVersion: networking.k8s.io/v1
        kind: NetworkPolicy
        metadata:
        name: cloud-metadata-deny
        namespace: default
        spec:
        podSelector: {}
        policyTypes:
        - Egress
        egress:
        - to:
            - ipBlock:
                cidr: 0.0.0.0/0
                except:
                - 169.254.169.254/32
        ```

    - [Kubernetes Documentation > Tasks > Access Applications in a Cluster > Deploy and Access the Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#accessing-the-dashboard-ui)

    - [Kubernetes Documentation > Tasks > Install Tools > Install and Set Up kubectl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

        > Note: Check the step 2 - validate binary
