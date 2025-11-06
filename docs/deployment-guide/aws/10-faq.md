---
sidebar_position: 10
title: FAQ
description: Frequently asked questions about AI/Run CodeMie deployment on AWS
---

# Frequently Asked Questions

## General Questions

### What is AI/Run CodeMie?

AI/Run CodeMie is an AI-powered platform for code analysis, documentation, and assistance. It helps development teams understand, maintain, and improve their codebases.

### What are the minimum requirements for deployment?

Please refer to the [Architecture](./03-architecture.md) section for detailed resource requirements. At minimum, you'll need:

- An AWS account with appropriate permissions
- A domain name for the application
- Resources for EKS cluster and supporting services

## Deployment Questions

### How long does the deployment take?

A typical deployment takes 2-4 hours depending on:

- Infrastructure deployment: 30-60 minutes
- Components deployment: 30-60 minutes
- Post-installation configuration: 30-60 minutes
- AI models integration: 30-60 minutes

### Can I deploy to an existing EKS cluster?

Yes, you can deploy to an existing EKS cluster. However, ensure it meets the requirements specified in the [Prerequisites](./02-prerequisites.md) section.

### What happens if deployment fails?

If deployment fails:

1. Check the error messages in the deployment logs
2. Verify all prerequisites are met
3. Check the troubleshooting sections in relevant deployment guides
4. Review Kubernetes pod logs for specific component failures

### Can I use a different cloud provider?

This guide is specific to AWS. For other cloud providers, please refer to their respective deployment guides if available.

## Configuration Questions

### Which AI models are supported?

AI/Run CodeMie supports various AI model providers:

- AWS Bedrock (Anthropic Claude, Amazon Titan, etc.)
- Azure OpenAI
- OpenAI
- Google Vertex AI
- Custom model endpoints

See [AI Models Integration](./07-ai-models-integration.md) for details.

### Can I use multiple AI models?

Yes, you can configure multiple AI models from different providers. The LiteLLM Proxy extension can help with load balancing across models.

### How do I configure authentication?

Authentication is managed through Keycloak, which is deployed as part of the installation. Configuration steps are covered in [Post-Installation Configuration](./06-post-installation.md).

## Maintenance Questions

### How do I update AI/Run CodeMie?

Follow the procedures in the [Update AI/Run CodeMie](./08-update.md) guide. Updates can be performed using scripted or manual methods.

### How do I backup my data?

Critical data to backup includes:

- PostgreSQL databases
- Elasticsearch indices
- Keycloak configuration
- ConfigMaps and Secrets

Implement regular backup procedures for these components.

### How do I monitor the deployment?

Monitoring options include:

- Kubernetes pod logs: `kubectl logs`
- Kibana dashboards for application logs
- AWS CloudWatch for infrastructure metrics
- Application health endpoints

## Troubleshooting

### Pods are not starting

Common causes:

- Insufficient cluster resources
- Missing or incorrect ConfigMaps/Secrets
- Image pull errors
- Node selector/affinity issues

Check pod status and logs:

```bash
kubectl get pods -n codemie
kubectl describe pod <pod-name> -n codemie
kubectl logs <pod-name> -n codemie
```

### Cannot access the application

Check:

1. Ingress controller is running
2. DNS records are configured correctly
3. SSL certificates are valid
4. Network policies and security groups allow traffic

### Database connection issues

Verify:

- PostgreSQL instance is running
- Connection credentials are correct in Secrets
- Network connectivity between pods and database
- Database user has required permissions

### Elasticsearch issues

Common issues:

- Insufficient disk space
- Memory pressure
- Index corruption
- Version compatibility

Check Elasticsearch logs and cluster health:

```bash
kubectl logs <elasticsearch-pod> -n elastic
```

## Performance Questions

### How do I scale the deployment?

Scaling options:

- Horizontal pod autoscaling (HPA) for application pods
- Increase replica counts in Helm values
- Scale EKS node groups
- Optimize resource requests/limits

### What are the performance considerations?

Key factors affecting performance:

- AI model response times
- Elasticsearch indexing speed
- Database query performance
- Network latency
- Resource allocation

## Security Questions

### How is data secured?

Security measures include:

- Authentication via Keycloak
- TLS/SSL for all connections
- Secrets management in Kubernetes
- Network policies
- IAM roles and policies (AWS)
- Data encryption at rest and in transit

### Can I integrate with my organization's SSO?

Yes, Keycloak supports various identity providers including:

- SAML
- OAuth 2.0
- OpenID Connect
- LDAP/Active Directory

### How are API keys and credentials managed?

Credentials are stored as Kubernetes Secrets and mounted into pods as needed. Use AWS Secrets Manager or similar services for additional security.

## Extensions Questions

### What extensions are available?

Available extensions include:

- LiteLLM Proxy (load balancing for AI models)
- AI/Run CodeMie Assistants Evaluation
- AI Code Explorer (AICE)
- Angular Upgrade Assistant
- Salesforce DevForce AI

See [Extensions](./09-extensions.md) for details.

### Are extensions required?

No, all extensions are optional. They provide additional functionality but are not required for core AI/Run CodeMie operation.

## Support

### Where can I get help?

For support:

1. Check this FAQ and deployment documentation
2. Review component-specific documentation in the codemie-helm-charts repository
3. Contact the AI/Run CodeMie support team
4. Check the project's issue tracker or support channels

### How do I report issues?

When reporting issues, include:

- Deployment method (scripted/manual)
- Component versions
- Error messages and logs
- Steps to reproduce
- Environment details (AWS region, cluster size, etc.)
