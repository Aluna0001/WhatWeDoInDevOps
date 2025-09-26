# CI/CD Pipeline

## CI/CD/CD

### Continuous Integration (CI)
* Automatisk bygning og test ved hver commit
* Opdager konflikter tidligt

### Continuous Delivery (CD)
* Automatisk pakning til deployment-klar tilstand
* **Eksempler:** Docker images, GitHub packages, Docker Hub registry

### Continuous Deployment (CD)
* Automatisk deployment til production
* Ingen manual intervention

## Pipeline Flow
```
Code Commit → Build & Test → Package → Deploy
```