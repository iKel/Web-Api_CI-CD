# CI/CD implementation
This repo contains code for a Node.js multi-tier application with Jenkins configuration.

The application overview is as follows
```

web <=> api <=> db

```
---
The project consists of:
- Front and backend. (API and Web folders).
- Both folders have Dockerfile (package installation).
- Both folders have Makefiles (ECR configuration, testing, building image, and deployment of application).
- Both folders have Helm charts and K8s deployments, services, and Ingresses.
- Both folders have configuration files for configuring the Helm chart according to the stage.
- The root folder has Jenkinsfile with the configurations.
-  The root folder contains a Script providing CI/CD logic. 
---

This Project has 3 stages: Dev, Stage, and Prod. Jenkins is connected to GitHub via Webhook polling for updates at 1-minute intervals. Once the updated code is pushed to a specified branch on GitHub, Jenkins will automatically start a job in the correct namespace. Once the job is completed the result can be accessed via the DNS name provided in the Helm chart configuration. 

The folders `web` and `API` describe how to install and run each app.
