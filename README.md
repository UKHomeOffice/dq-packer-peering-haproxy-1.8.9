# dq-packer-peering-haproxy
This repository creates an AMI in AWS with HAProxy with logging to rsyslog

## `packer.json`
This file contains a wrap up for Ansible script to be run inside small Centos 7.5 machine

## `playbook.yml`
Ansible playbook installing the following:
- rsyslog
- HAProxy v.1.8.9 - installed from source and compiled locally wih the follwing options:
    - TARGET: linux2628
    - USE_PCRE: 1
    - USE_OPENSSL: 1
    - USE_ZLIB: 1
    - USE_LIBCRYPT: 1

    More information can be found [here](https://github.com/joyent/haproxy-1.8/blob/master/Makefile)

## `templates`

#### `gets3content.sh`
This file is copied to `/home/ec2-user/` and cron entry created to run it every hour

#### `rsyslog.conf.j2`
Initial rsyslog main configuration

#### `49-haproxy.conf.j2`
Initial rsyslog config to capture logs from HAProxy

#### `haproxy.cfg`
HAProxy initial configuration. It contains TCP frontend (23) which is used for testing if proxy is up.
if you plan to change it, update `playbook.yml` accordingly

Please note: the following line needs to be in all configurations for socket being created at start time:
```
    stats socket /var/run/haproxy.sock mode 660 level admin expose-fd listeners
```



## Contributing

If you'd like to contribute, please fork the repository and use a feature
branch. Pull requests are warmly welcome.

More information in [`CONTRIBUTING.md`](./CONTRIBUTING.md)

## Links

- Project homepage: https://github.com/pawniemiec/repo-template
- Repository: https://github.com/pawniemiec/repo-template
- Issue tracker: https://github.com/pawniemiec/repo-template/issues
- In case of sensitive bugs like security vulnerabilities, please contact 
    pniemiec@noledgetech.com directly instead of using issue tracker. 
    We value your effort to improve the security and privacy of this project!
- Related projects:
  - Your other project: https://github.com/your/other-project/
  - Someone else's project: https://github.com/someones/awesome-project/

## Licensing
The code in this project is licensed under this [`LICENSE`](./LICENSE.md)

## Code of Conduct
Please follow this [`CODE OF CONDUCT`](./CODE_OF_CONDUCT.md)
