# Rails Commands

## Generators

### Controllers
```bash
# Create a controller with actions
> rails g controller StaticPages home about contact

# Undo the creation (pass in the actions) of the controller
> rails destroy controller StaticPages home about contact
```

### Models
```bash
# Create model
> rails g model User name:string email:string

# Undo the creation of a model (do not pass in actions/attributes)
> rails destroy model User
```
