# Trevy Infrastructure

CloudFormation templates and infrastructure automation for Trevy platform.

## Architecture

Separate repo pattern with SSM-based configuration sharing.

## Stacks

- `github-oidc-role.yml` - GitHub OIDC provider and IAM role
- `ecs-cluster.yml` - ECS Fargate cluster
- `iam-roles.yml` - Task execution and app roles
- `data-layer.yml` - RDS PostgreSQL + ElastiCache Redis
- `frontend.yml` - S3 + CloudFront distribution
- `web-service.yml` - Laravel web service
- `horizon-service.yml` - Laravel Horizon queue worker
- `scheduler-service.yml` - Laravel scheduler
- `ai-service.yml` - FastAPI AI service

## SSM Parameter Contract

Infrastructure writes outputs to SSM for services to consume:

- `/trevy/{env}/iam/*` - IAM role ARNs
- `/trevy/{env}/data/*` - Database and Redis connection info
- `/trevy/{env}/frontend/*` - S3 bucket and CloudFront distribution

Services write their outputs back to SSM for cross-service communication.
