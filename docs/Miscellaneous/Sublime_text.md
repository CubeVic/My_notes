Some configuration for sublime text

## 'End' Key of the keyboard not working on sublime text 3 MAC

Go to preference -> Key Bindings - User add
```
{ "keys": ["end"], "command": "move_to", "args": {"to": "eol"} },
{ "keys": ["home"], "command": "move_to", "args": {"to": "bol"} }
```
