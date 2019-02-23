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

### Create a named session with window name
```sh
> tmux new -s session-name -n window_name
```

### Open another window inside a session
```sh
> PREFIX C
```

### Name a Window
```sh
> PREFIX ,
```

### Navigate windows
```sh
> PREFIX n // next window
or
> PREFIX p // previous window

> PREFIX NUMBER // 0 index based array
```

### Search through windows
```sh
> PREFIX f name_of_window
> PREFIX w // visual representation of the windows, select one
```

### Close a Window
```sh
> PREFIX & // will show a confirmation
```
