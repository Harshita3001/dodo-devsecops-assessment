## Task 1 — Harden the Kubernetes Deployment

### Objective
Secure the Ledger API Kubernetes deployment using container and Kubernetes security best practices.

### Implemented
- Hardened Docker image using a non-root user.
- Added Kubernetes security contexts.
- Disabled privilege escalation.
- Dropped all Linux capabilities.
- Enabled read-only root filesystem.
- Added CPU and memory resource limits.
- Added liveness and readiness probes.
- Implemented RBAC with a dedicated ServiceAccount.
- Used Sealed Secrets instead of storing plaintext secrets.
- Enabled Kubernetes Pod Security restrictions.
- Added Kyverno admission policies.
- Blocked containers running as root.
- Blocked images using the `:latest` tag.

### Validation
- Ledger API replicas successfully running.
- Health endpoint verified.
- Pod security context verified.
- Kubernetes Pod Security rejected insecure workloads.
- Kyverno successfully rejected non-root violations.
- Kyverno successfully rejected `:latest` image tags.

### Evidence
Validation screenshots are available in:

`task-1/screenshots/`# dodo-devsecops-assessment
Dodo Payments Security &amp; DevOps Engineer assessment
