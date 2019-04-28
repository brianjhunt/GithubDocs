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

### Database Commands
```bash
# migrate the database
> rails db:migrate

# undo a single migration step
> rails db:rollback

# roll database back to specific migration version
> rails db:migrate VERSION=0
```
