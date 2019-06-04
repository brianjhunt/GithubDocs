# Server is already running error
```bash
A server is already running. Check /usr/src/app/tmp/pids/server.pid
```

## Quick fix
```bash
> rm tmp/pids/server.pid
```

## More permanent solution

### Create docker-entrypoint.sh in the Rails root
```sh
#!/bin/sh
set -e
if[-f tmp/pids/server.pid]; then
  rm tmp/pids/server.pid
fi
exec "$@"
```
### Make the file executable
```bash
> chmod +x docker-entrypoint.sh
```

### Specify the enterpoint instruction in the Dockerfile file by adding the following line before the final CMD statement
```
ENTRYPOINT["./docker-entrypoint.sh]

### Stop, rebuild, and restart the server
```bash
> docker-compose stop <service>
> docker-compose build <service>
> docker-compose start <service>
```
### Bye Bug is not working
We want an interactive sessions with the container. Instead of bringing up compose in detached mode, bring up like this:
```bash
> docker-compose run --service-ports <container name>
```
docker-compose run by default will ignore port mappings specified in the docker-compose.yml file for the service. --service-ports changes this behavior and maps them. Without this option, the application could not be reached at localhost:3000 in the browser.
