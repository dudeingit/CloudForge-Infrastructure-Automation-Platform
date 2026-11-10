# CloudForge-Infrastructure-Automation-Platform
CloudForge is a local-first cloud infrastructure automation platform that demonstrates how modern engineering teams can provision infrastructure, deploy containerized applications, validate changes, enforce security, monitor workloads, and automatically recover from failed deployments — without requiring a live cloud account
Primary Use Case
A development/platform team needs to deploy an application reliably across Dev and Production-like environments.

Instead of manually performing:
Infrastructure setup
        ↓
Application deployment
        ↓
Configuration
        ↓
Security checks
        ↓
Testing
        ↓
Monitoring
        ↓
Failure recovery

CloudForge automates the entire lifecycle.

Real-world scenario
A developer changes the application or infrastructure code and creates a GitHub Pull Request.

CloudForge automatically:
1. Validates Terraform
2. Checks infrastructure security
3. Builds the Docker image
4. Runs application tests
5. Validates Kubernetes manifests
6. Deploys to the local Kubernetes environment
7. Performs health checks
8. Starts monitoring
9. Detects deployment failure
10. Automatically rolls back to the previous healthy version

End-to-End Workflow
Developer
   │
   │ Git Push / Pull Request
   ▼
GitHub Repository
   │
   ▼
GitHub Actions
   │
   ├── Terraform Format
   ├── Terraform Validate
   ├── Security Scan
   ├── Python Tests
   ├── Docker Build
   └── Kubernetes Validation
          │
          ▼
     Deployment
          │
          ▼
   Kubernetes / kind
          │
     ┌────┴────┐
     │         │
   App       Service
     │         │
     └────┬────┘
          ▼
     Health Checks
          │
     ┌────┴────┐
     │         │
   Healthy   Failed
     │         │
     ▼         ▼
 Monitor    Rollback
     │         │
     └────┬────┘
          ▼
   Final Validation

   The interesting use case: failure recovery
   Normal deployment
   v1 Application
      ↓
Deploy
      ↓
Health Check
      ↓
PASS ✓
      ↓
Monitoring

Then intentionally introduce a bad configuration:
v2 Application
      ↓
Deploy
      ↓
Health Check
      ↓
FAIL ✗
      ↓
Rollback
      ↓
v1 restored
      ↓
Health Check
      ↓
PASS ✓
