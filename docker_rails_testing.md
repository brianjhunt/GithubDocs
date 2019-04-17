# Testing (BDD/TDD) a Rails Application in a Docker Environment
Example used here is with Rspec.

### Update the Gemefile
```ruby
group :development, :test do
  gem 'rspec-rails', '~> 3.8'
end
```
### Stop the web container and rebuild the container
```bash
> docker-compose stop web
> docker-compose build web
```
