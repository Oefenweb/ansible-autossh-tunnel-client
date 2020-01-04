## autossh-tunnel-client

[![Build Status](https://travis-ci.org/Oefenweb/ansible-autossh-tunnel-client.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-autossh-tunnel-client) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-autossh--tunnel--client-blue.svg)](https://galaxy.ansible.com/Oefenweb/autossh-tunnel-client)

Set up a persistent tunnel (using `autossh`) in Ubuntu systems (client side).

#### Requirements

None

#### Variables

* `autossh_tunnel_client_autossh_debug`: [default: `1`]: If this variable is set, the logging level is set to `LOG_DEBUG`
* `autossh_tunnel_client_autossh_first_poll`: [default: `30`]: Specifies the time to wait before the first connection test
* `autossh_tunnel_client_autossh_gatetime`: [default: `0`]: Specifies how long ssh must be up before we consider it a successful connection. If it is set to `0`, then not only is the gatetime behaviour turned off, but autossh also ignores the first run failure of ssh
* `autossh_tunnel_client_autossh_loglevel`: [default: `7`]: Specifies the log level, corresponding to the levels used by syslog
* `autossh_tunnel_client_autossh_pidfile`: [default: `/var/run/autossh/autossh-tunnel-client.pid`]: Write pid to specified file
* `autossh_tunnel_client_autossh_poll`: [default: `60`]: Specifies the connection poll time in seconds

* `autossh_tunnel_client_key_map`: [default: `[]`]: SSH key declarations
* `autossh_tunnel_client_key_map.{n}.src`: [required]: The local path of the file to copy, can be absolute or relative (e.g. `../../../files/autossh-tunnel-client/etc/autossh/id_rsa`)
* `autossh_tunnel_client_key_map.{n}.dest`: [optional, default `src | basename`]: The remote path of the file to copy, relative to `/etc/autossh` (e.g. `id_rsa`)
* `autossh_tunnel_client_key_map.{n}.owner`: [optional, default `root`]: The name of the user that should own the file
* `autossh_tunnel_client_key_map.{n}.group`: [optional, default `owner`, `root`]: The name of the group that should own the file
* `autossh_tunnel_client_key_map.{n}.mode`: [optional, default `0600`]: The mode of the file to copy

* `autossh_tunnel_client_host`: [required] Remote host to connect to (e.g. `example.com`)
* `autossh_tunnel_client_port`: [default: `22`]: Remote port to connect to
* `autossh_tunnel_client_user`: [default: `autossh`]: Remote user for connection
* `autossh_tunnel_client_identity`: [default: `id_rsa`]: Remote user for connection

* `autossh_tunnel_client_autossh_options`: [default: `['M 0', '4', 'N']`]: Autossh options
* `autossh_tunnel_client_ssh_options`: [default: `['ServerAliveInterval 60', 'ServerAliveCountMax 3', 'BatchMode=yes', 'StrictHostKeyChecking=no']`]: SSH options

* `autossh_tunnel_client_forward`: [required]: Port forward to set up (e.g. `['3307:127.0.0.1:3306']`)
* `autossh_tunnel_client_forward_direction`: [default: `L`]: Specifies the direction of the tunnel. If it is set to `R`, then the direction of the tunnel is reversed making it into a reverse ssh tunnel

## Dependencies

None

## Recommended

* `ansible-autossh-tunnel-server` ([see](https://github.com/Oefenweb/ansible-autossh-tunnel-server))

#### Example(s)

##### MySQL tunnel

```yaml
---
- hosts: all
  roles:
    - autossh-tunnel-client
  vars:
    autossh_tunnel_client_key_map:
      - src: ../../../files/autossh-tunnel-client/etc/autossh/id_rsa
    autossh_tunnel_client_host: 'example.com'
    autossh_tunnel_client_forward: ['3307:127.0.0.1:3306']
```

You will be able to connect to mysql using:

```bash
mysql -h 127.0.0.1 -P 3307 -u#### -p#### --skip-ssl;
```

#### License

MIT

#### Author Information

Mischa ter Smitten (based on work of netkernelroc)

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-autossh-tunnel-client/issues)!
