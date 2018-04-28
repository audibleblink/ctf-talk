# what the SSH?!

An outline of a keynote delivered in 2016. Slides are executable with `bundle && ruby talk.rb`

## Authentication
  - how it works
    - password
    - key pairs
      - public > server
      - private > local computer
    - key exchange
      1. session id and intent to connect
      2. server receives, encrypt random string and send to  client
        a. server hashes string and session id and waits for reply
      3. client receives message; decrypts it and hashes is with the session id and sends it back
      4. server receives the hash and compares it against its own
  - keygen demo


## Configuration
  - user config
    - demo
  - server config
    - PasswordAuthenticate
    - AllowUsers
  - authorized_keys
    - holds public keys whose private key counterparts are allowed to connect
    - and much more! - see slides


## Tunnels
  - Remote
    - exposing a local service to the world
  - Local
    - exposing a service the ssh server has access to, locally
    - examples
  - Dynamic
    - create a tunnel that's not bound to a specific port or resource
  - Persistent
    - autossh

## Command Execution
  - run commands a remote machine and get the information locally


## Client Control
  - ~.
  - ~z
  - ~C
  - ~?


## Resources
  - [ssh-config](linux.die.net/man/5/ssh_config)
  - [tldr](http://tldr-pages.github.io)
  - [explainshell](http://explainshell.com)
  - [Digital Ocean SSH Rundown](http://j.mp/1SZpWbd)
  - [Black Magic of SSH (Vimeo)](http://vimeo.com/54505525)
  - [Diffe-Hellman Video](https://www.youtube.com/watch?v=YEBfamv-_do)
