
# Monitoring, Logging, and Runtime Securit (20%)

The final part of our course focuses on identifying unusual activities in Kubernetes clusters at both the host and container levels. We'll start by explaining behavior analytics within Kubernetes, then introduce Falco, a tool for spotting intrusions.

Containers, even after being started, can be altered—for instance, by adding tools or files. Such changes can create security risks. We advocate for the use of immutable containers, which cannot be modified post-launch. We'll show how to set up a Pod to ensure its containers remain unchanged.

Lastly, we'll cover how to collect logs from cluster events. These logs are valuable for fixing issues, understanding changes that led to problems, or tracking ongoing attacks to respond appropriately.


- [x] Performing behavior analytics to detect malicious activities

- [x] Performing deep analytical investigation and identification

- [x] Ensuring immutability of containers at runtime

- [x] Using audit logs to monitor access