# docker-mac-ssh-auth-sock

This is an improved version of [mariusgrigaitis/docker-mac-ssh-auth-sock](https://github.com/mariusgrigaitis/docker-mac-ssh-auth-sock),
which can be installed via Homebrew as a service.

## Install

```bash
brew install punktde/public/docker-ssh-auth-sock
brew services start punktde/public/docker-ssh-auth-sock
```

The service will restart on boot.

## Usage

### docker run

```bash
docker run -v "${SSH_AUTH_SOCK}:${SSH_AUTH_SOCK}" -e "SSH_AUTH_SOCK=${SSH_AUTH_SOCK}" --entrypoint /usr/bin/ssh-add alpine/git -l
```

The output should match the output of `ssh-add -l` on your host.

### docker-compose

```yaml
version: '3.6'
services:
  myservice:
    image: alpine/git
    volumes:
      - ${SSH_AUTH_SOCK}:${SSH_AUTH_SOCK}
    environment:
      - SSH_AUTH_SOCK=${SSH_AUTH_SOCK}
    entrypoint: /usr/bin/ssh-add
    command: -l
```

The output should match the output of `ssh-add -l` on your host.
