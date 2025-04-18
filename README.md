# Spotify Clone Microservices Project

_A scalable, production-ready Spotify clone built with a modern microservices architecture._

---

## Overview

This project is a full-featured Spotify clone designed to demonstrate best practices in scalable microservices, cloud-native deployment, and modern web development.

**Key technologies:**

- **Frontend:** React
- **Backend:** NestJS microservices (Node.js/TypeScript)
- **Databases:** PostgreSQL and MongoDB (polyglot persistence)
- **Containerization:** Docker
- **Orchestration:** Kubernetes (AWS EKS)
- **Cloud Provider:** AWS (EKS, ECR, RDS/DocumentDB, S3, ACM)
- **CI/CD:** GitHub Actions
- **Cost Optimization:** AWS Free Tier and spot instances where possible

---

## Project Goals

- Implement core Spotify-like features: user management, playlists, music catalog, search, and streaming.
- Follow microservice architecture best practices with independent services and databases.
- Use polyglot persistence to optimize data storage per service.
- Containerize all components for consistent deployment.
- Deploy and manage services on AWS EKS with Kubernetes.
- Minimize AWS cost by leveraging free tier and efficient resource usage.
- Implement CI/CD pipelines for automated testing and deployment.
- Secure services using AWS Secrets Manager, IAM roles, and HTTPS.

---

## Architecture

### Microservices and Database Mapping

| Service                        | Description                                | Database                  | Reasoning                                                               |
| ------------------------------ | ------------------------------------------ | ------------------------- | ----------------------------------------------------------------------- |
| **Auth Service**               | Handles user authentication and tokens     | PostgreSQL                | Relational, transactional data requiring strong consistency             |
| **User Service**               | Manages user profiles and settings         | PostgreSQL                | Structured data with relationships and transactions                     |
| **Playlist Service**           | Manages user playlists and track relations | PostgreSQL                | Complex relational data, joins, and transactional integrity             |
| **Music Catalog Service**      | Stores metadata of artists, albums, tracks | MongoDB                   | Flexible schema, large unstructured documents, scalable                 |
| **Search Service**             | Provides search capabilities on music data | MongoDB or ElasticSearch  | Fast, flexible querying; ElasticSearch for advanced search              |
| **Streaming/Playback Service** | Handles streaming sessions, playback logs  | MongoDB or Redis          | High throughput session data; Redis for caching, MongoDB for durability |
| **Analytics Service**          | Collects user behavior and usage metrics   | MongoDB or Time-Series DB | Write-heavy, flexible schema or time-series optimized                   |

**Communication:**

- Services communicate via RESTful APIs or message brokers.
- API Gateway aggregates endpoints for frontend consumption.
- Authentication via JWT/OAuth tokens.

---

## Technology Stack

| Layer                  | Technology/Tool                       |
| ---------------------- | ------------------------------------- |
| Frontend               | React                                 |
| Backend                | NestJS (Node.js)                      |
| Databases              | PostgreSQL, MongoDB                   |
| Containerization       | Docker                                |
| Orchestration          | Kubernetes (EKS)                      |
| Cloud Provider         | AWS                                   |
| CI/CD                  | GitHub Actions                        |
| Logging & Monitoring   | AWS CloudWatch, Prometheus (optional) |
| Secrets Management     | AWS Secrets Manager                   |
| Load Balancing/Ingress | AWS ALB, K8s Ingress                  |
| Static Assets          | AWS S3 + CloudFront                   |

---

## Development Setup

### Frontend

- Scaffold React app (e.g., Vite).
- Use React Router, Redux/Context API for state management.
- Containerize with Docker.

### Backend

- Scaffold NestJS microservices (one repo per service or monorepo).
- Use TypeORM for PostgreSQL services.
- Use Mongoose for MongoDB services.
- Implement REST APIs with validation and authentication.
- Containerize each service with Docker.

### Local Orchestration

- Use `docker-compose` for local multi-container orchestration (optional).
- Run local PostgreSQL and MongoDB instances or use Docker images.

---

## Infrastructure as Code

- Write Kubernetes manifests for all services: Deployments, Services, ConfigMaps, Secrets, Ingress.
- Use Helm charts for templating and easier management (recommended).
- Use AWS managed DB services:
  - RDS for PostgreSQL (free tier eligible)
  - DocumentDB for MongoDB (if cost permits) or self-host MongoDB on EKS (not recommended for production)
- Store secrets securely in AWS Secrets Manager or Kubernetes Secrets.

---

## AWS Setup & Deployment

1. **AWS Account**

   - Set up billing alerts and budgets.
   - Create an ECR repository for Docker images.
   - Create an S3 bucket for static assets.
   - Request ACM certificates for HTTPS.

2. **EKS Cluster**

   - Create EKS cluster with smallest possible instance types (t3.micro or t3.small).
   - Enable autoscaling and spot instances for cost savings.
   - Configure `kubectl` and AWS CLI locally.

3. **CI/CD Pipeline**

   - Use GitHub Actions to:
     - Lint, test, build Docker images.
     - Push images to ECR.
     - Deploy to EKS using `kubectl` or Helm.

4. **Deploy Services**
   - Deploy backend microservices to EKS.
   - Deploy frontend as a containerized app or host static files on S3 + CloudFront.
   - Configure Ingress with AWS ALB and ACM for HTTPS.

---

## Monitoring & Logging

- Use AWS CloudWatch for logs and metrics aggregation.
- Optionally integrate Prometheus and Grafana for detailed monitoring.
- Centralize logs for troubleshooting and performance analysis.

---

## Security Best Practices

- Use JWT/OAuth for authentication and authorization.
- Store sensitive data in AWS Secrets Manager or Kubernetes Secrets.
- Apply least privilege principle for IAM roles and security groups.
- Use HTTPS for all communications.
- Regularly update dependencies and container images.

---

## Cost Optimization Tips

- Use AWS Free Tier services where possible (RDS, EKS, S3).
- Use spot instances for worker nodes in EKS.
- Set resource requests and limits in Kubernetes pods to avoid over-provisioning.
- Monitor AWS billing and shut down unused resources.
- Use S3 + CloudFront for frontend static hosting to reduce compute costs.

---

## Testing Strategy

- Unit tests for frontend and backend.
- Integration tests for API endpoints.
- End-to-end tests with Cypress or similar tools.
- Load and resilience testing in staging environment.

---

## Documentation

- Maintain up-to-date API documentation (Swagger/OpenAPI).
- Document architecture decisions and deployment steps.
- Write onboarding guides for new developers.

---

## Next Steps

- Define detailed feature list and API contracts.
- Scaffold repositories and initial microservices.
- Set up local development environment.
- Build CI/CD pipelines.
- Deploy initial MVP to AWS EKS.

---

## References

- [NestJS Documentation](https://docs.nestjs.com/)
- [React Documentation](https://react.dev/)
- [AWS EKS Documentation](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Docker Documentation](https://docs.docker.com/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [MongoDB Documentation](https://www.mongodb.com/docs/)

---

_This README provides a comprehensive guide for development, deployment, and scaling of a Spotify clone using microservices and cloud-native best practices._
