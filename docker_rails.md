# Docker Cheatsheet for Ruby on Rails

## Setting up a Ruby on Rails image

#### Get application code on your local computer without having Ruby installed:
```bash
# Start in the project directory
> cd project_directory

# Start a temporary container
> docker container run --rm -it -v ${PWD}:/usr/src/app ruby:2.6 bash

#Inside the container, change to the directory listed above
> cd usr/src/app

# Install the Rails gem and generate a new Rails app
> gem install rails
> rails new myapp --skip-test --skip-bundle

# Change ownership of files from root to user
> sudo chown $USER:$USER -R
```

#### Create a Dockerfile for the image:
```bash
# Create the Dockerfile
> cd myapp
> touch Dockerfile

# Open the new Dockerfile
> vim Dockerfile
```

#### Dockerfile
The dockerfile will be used as a blue print to create the image.
```txt
FROM ruby:2.6

LABEL maintainer="name@email.com"

RUN apt-get update -yqq && apt-get install -yqq --no-install-recommends \
  nodejs
  
COPY Gemfile* /usr/src/app/
WORKDIR /usr/src/app
RUN bundle install

COPY . /usr/src/app/

CMD ["bin/rails", "s", "-b", "0.0.0.0"]
```

#### Build the image from the Dockerfile
```bash
# From within the myapp directory
> docker build .

# View the new image
> docker images
```

#### Start the Rails server
```bash
> docker container run -p 3000:3000 image_id
```

## Setting up a Docker Compose File for a Ruby on Rails Application

#### Create the docker compose file in the project directory
```bash
> touch docker-compose.yml
```

#### Docker Compose File
This file describes the application.
```yaml
version: '3'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/usr/src/app
```

Note: By default, Ruby buffers output to stdout , which doesn’t play well with Com-
pose. To avoid this:

```ruby
# config/boot.rb
$stdout.sync = true
```

#### Start the Services
```bash
> docker-compose up
```

### Docker Compose Commands
```bash
# See running containers (Name, Command, State, Ports)
> docker-compose ps

# Stop containers
> docker-compose stop <service name>

# Start containers
> docker-compose start <service name>

# Restart containers to pick up config changes
> docker-compose restart <service name>

# View container logs
> docker-compose logs <service name>

# View container logs and continue to follow / append
> docker-compose logs -f <service name>

# Run one off commands
> docker-compose run --rm web echo "running a different command"

# Run one off commands without starting up a new container
> docker-container exec web echo "running a different command"

# Rebuilding images
> docker-compose build web
# Why rebuild images? 
# Updated Gemfile and need to reinstall your gems
# Modified Dockerfile with new dependencies
# Want to share your image and need to include the latest code charges

# Remove the app's containers
> docker-compose rm

# Remove unused images
> docker image prune

# Free up all unused resources
> docker system prune
```
