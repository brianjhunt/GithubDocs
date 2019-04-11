# PostGRESQL and Docker
This details how to add a database (open-sourced PostGRESQL) in this case.

### Docker Compose File Setup (docker-compose.yml
```yaml
...
services:
  database:
    image: postgres
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: secret-password
      POSTGRES_DB: myapp_development
...
```
