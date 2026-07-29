\# Task 2 – Secure CI/CD and GitOps



\## Overview



This task implements a secure CI/CD pipeline and GitOps-based deployment workflow for the Ledger API developed in Task 1.



The implementation focuses on automated security scanning, container image publishing, keyless image signing, provenance generation, signature verification, vulnerability scanning, and Kubernetes deployment through ArgoCD.



\## CI/CD Pipeline



The GitHub Actions workflow is defined at:



`.github/workflows/secure-ci.yml`



The pipeline runs on pushes and pull requests to the `main` branch.



\### Pipeline Stages



1\. Checkout source code

2\. Set up Python

3\. Install application dependencies

4\. Run Gitleaks secret scanning

5\. Run Semgrep SAST scanning

6\. Install Cosign

7\. Authenticate to GitHub Container Registry (GHCR)

8\. Build the Ledger API Docker image

9\. Push the image to GHCR

10\. Sign the container image using keyless Cosign

11\. Generate SLSA-style provenance

12\. Verify the Cosign signature

13\. Run Trivy vulnerability scanning



\## Security Controls



\### Gitleaks



Gitleaks scans the repository for accidentally committed secrets and credentials.



\### Semgrep



Semgrep performs static application security testing against the application source code.



\### Trivy



Trivy scans the built container image for HIGH and CRITICAL vulnerabilities.



The pipeline is configured to fail when unacceptable HIGH or CRITICAL vulnerabilities are detected.



\### Cosign Keyless Signing



Container images published to GHCR are signed using Cosign keyless signing with GitHub Actions OIDC identity.



This avoids maintaining long-lived private signing keys.



\### Signature Verification



The pipeline verifies the generated Cosign signature against the GitHub Actions OIDC identity before considering the image trusted.



\## Supply Chain Provenance



The pipeline generates provenance metadata containing information about the build invocation, source repository, commit SHA, and build environment.



The provenance is attached to the container image using Cosign attestation.



This provides traceability between source code and the resulting container artifact.



\## GitOps Deployment



ArgoCD is used for GitOps-based Kubernetes deployment.



The ArgoCD Application manifest is located at:



`task-2/gitops/apps/ledger-api.yaml`



ArgoCD tracks Kubernetes manifests stored in Git and automatically reconciles the desired state with the Kubernetes cluster.



Automated sync, pruning and self-healing are enabled.



\## Runtime Validation



The Ledger API was deployed to the `payments` namespace in the local Kubernetes cluster.



The application health endpoint was validated successfully and returned HTTP 200 responses.



ArgoCD was also configured to manage the application from the Git repository.



\## Evidence



Execution evidence is available under `task-2/screenshots/`.



The screenshots demonstrate:



\- Successful CI security checks

\- Successful complete security pipeline

\- Container image publishing to GHCR

\- GHCR package publication

\- Cosign image signing

\- SLSA provenance generation

\- Cosign signature verification



\## Repository Structure



```text

task-2/

├── README.md

├── docs/

├── gitops/

│   └── apps/

│       └── ledger-api.yaml

└── screenshots/

