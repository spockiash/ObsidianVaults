Secure Shell is protocol for secure access over encrypted connection. The basic command usage is:
```sh
ssh <user>@<host>
ssh root@192.168.1.100
```

Custom port can be specified using option `-p <port_number>`

## Key-based authentication
Passwords are less secure then using keys. To do thins run key generator on local machine:
```sh
ssh-keygen -t rsa -b 4096
```
This generates a private key at `~/.ssh/id_rsa` and public key at `~/.ssh/id_rsa.pub`.

Then we can copy the key to the remote machine:
```
ssh-copy-id <user>@<remote_host>
```
## SSH Tunneling and Port forwarding
This can be used for bypassing of firewalls or accessing remote services securely.
### Access a remote service locally
Forwards a port from the remote server to your machine:
```sh
ssh -L local_port:target_host:target_port user@remote_host
```
For example when we want to expose to local machine a remote service (here running SE toolkit on docker):
```sh
ssh -L 8000:127.20.0.2:8000 root@127.0.0.1 -p 2222
```
This way we can access the remotely running service on our local machine.
### Remote Port Forwarding