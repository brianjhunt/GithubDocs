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
### Install the PostGRESQL gem
Edit the Gemfile first.
...
gem, 'pg', '~> 1.0'
...

Stop the web container
```bash
> docker-compose stop web
```

Rebuild the image (includes bundle install)
```bash
> docker-compose build web
```

### Configure the config/database.yml file for PostGRESQL
```yaml
default: &default
adapter: postgresql
encoding: unicode
host:
<%= ENV.fetch('DATABASE_HOST') %>
username: <%= ENV.fetch('POSTGRES_USER') %>
password: <%= ENV.fetch('POSTGRES_PASSWORD') %>
database: <%= ENV.fetch('POSTGRES_DB') %>
pool: 5
variables:
statement_timeout: 5000

development:
<<: *default

test:
<<: *default
database: myapp_test

production:
<<: *default
```
### Update docker-compose file for web to include the same environment variables
```yaml
services:
  web:
    ...
    env_file:
      - .env/development/database
      - .env/development/web
    ...
  database:
    env_file:
      - .env/development/database
```

### Create dot files which will not be committed to version control
```bash
> mkdir -p .env/development
> touch .env/development/web
> touch .env/development/database
```

Add web-service-specific environment variables to .env/development/web
```
DATABASE_HOST=database
```

Add database-service-specific environment variables to .env/development/database
```
POSTGRES_USER=posgres
POSTGRES_PASSWORD=secret-password
POSTGRES_DB=to-do_development
```

### Create the development and test databases
```bash
> docker-compose run --rm web bin/rails db:create
```
### Restart the RAils Server and force docker to create a new container
```bash
> docker-compose up -d --force-recreate web
```
