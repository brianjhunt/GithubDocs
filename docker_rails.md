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
