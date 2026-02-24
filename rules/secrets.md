# Secrets Management

Never store secrets, passwords, API keys, or sensitive credentials directly in code.

## Rules

1. **Environment Variables Only**: All secrets must be stored in environment variables and loaded from `.env` files locally
   - Use `.env` for local development
   - Ensure `.env` is in `.gitignore`
   - Provide `.env.example` or `.env.template` with placeholder values (never real secrets)

2. **Secret Management Systems**: For production and deployment, use proper secret management:
   - **Docker**: Use Docker Secrets
   - **Google Cloud Platform**: Use GCP Secret Manager
   - **AWS**: Use AWS Secrets Manager or AWS Systems Manager Parameter Store
   - **Azure**: Use Azure Key Vault
   - **Kubernetes**: Use Kubernetes Secrets
   - **HashiCorp Vault**: For multi-cloud or on-premise deployments

3. **Never Commit Secrets**:
   - Do not hardcode API keys, passwords, tokens, or credentials in source code
   - Do not commit `.env` files with real secrets
   - Do not include secrets in configuration files that are version controlled
   - Do not log secrets or include them in error messages

4. **Code Patterns**:
   ```python
   # ✅ CORRECT
   import os
   api_key = os.getenv('API_KEY')
   db_password = os.getenv('DATABASE_PASSWORD')
   
   # ❌ WRONG
   api_key = 'sk-1234567890abcdef'
   db_password = 'mypassword123'
   ```

5. **Environment File Structure**:
   - `.env` - Local secrets (git ignored)
   - `.env.example` - Template with dummy values (committed to git)
   - `.env.test` - Test environment variables (no real secrets)

6. **Validation**:
   - Always validate that required environment variables are set before using them
   - Fail fast with clear error messages if secrets are missing
   - Never use default secret values in production code

## Examples

### .env.example (committed)
```
API_KEY=your_api_key_here
DATABASE_PASSWORD=your_db_password_here
JWT_SECRET=your_jwt_secret_here
```

### .env (git ignored, never committed)
```
API_KEY=sk-real-api-key-value
DATABASE_PASSWORD=actual_secure_password
JWT_SECRET=actual_jwt_secret_value
```

### Docker Secrets
```yaml
# docker-compose.yml
services:
  app:
    secrets:
      - db_password
      - api_key

secrets:
  db_password:
    external: true
  api_key:
    external: true
```

### GCP Secret Manager
```python
from google.cloud import secretmanager

def get_secret(secret_id):
    client = secretmanager.SecretManagerServiceClient()
    name = f"projects/{project_id}/secrets/{secret_id}/versions/latest"
    response = client.access_secret_version(request={"name": name})
    return response.payload.data.decode("UTF-8")
```

## Before Committing

Always verify:
1. `.env` is in `.gitignore`
2. No secrets are hardcoded in source files
3. `.env.example` exists with placeholder values
4. Secret management is properly configured for deployment environments

