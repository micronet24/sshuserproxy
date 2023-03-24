# user based SSH reverse proxy

## TL;DR Simple setup instructions

To setup the user-based reverse proxy the following steps should be
performed.

### On the Gateway

1. Create a key-pair for password-less login on the ssh-server using
   `ssh-keygen`
2. setup syncronization of `authorized_keys` for the proxied users
	* If the syncronization should be done via scp, add the public
	  key of the ssh-server to the gateways' `authorized_keys`. It
	  is recommended to call the syncronized variant
	  `authorized_keys2`
3. Install `sshproxy_gateway`
4. setup `~/ssh/proxy/gateway.conf`, a sample file is shipped
5. symlink the name of the ssh-application to `sshproxy_gateway`

### On the ssh app-server

1. If syncronization should be done via scp, create a key-pair using
   `ssh-keygen`
2. Install `sshproxy_host`
3. add `command="/usr/bin/sshproxy_host",no-port-forwarding,no-X11-forwarding,no-agent-forwarding,no-pty ssh-rsa ...`
   to the (not syncronized!) `authorized_keys` file
4. maybe setup path of `authorized_keys` in your application. the name
   `authorized_keys2` is recommended for that file

## Problem discussion

The complete discussion of the problem can be seen in the [Wiki](https://git.dresden.micronet24.de/benjamin/sshuserproxy/wiki)

