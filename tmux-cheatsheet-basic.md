# TMUX Cheatsheet (Basic Commands and Operations)

### Open TMUX
```sh
> tmux
```

### Close TMUX
```sh
> exit
```

### List TMUX Sessions
```sh
> tmux ls
or
> tmux list-sessions
```

### Create a Named Session
```sh
> tmux new-session -s name_of_session
or
> tmux new -s name_of_session
```

### Detach a Session
```sh
> PREFIX d
```

### Attach to a session
```sh
> tmux attach
0r
> tmux attach -t session_name
```

### End Session
```sh
> tmux kill-session -t session_name
or
> exit
```
