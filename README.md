# L4S Box for Vagrant

This repo contains the `Vagrantfile` for a [Vagrant](https://www.vagrantup.com/)
box (in [Virtualbox](https://www.virtualbox.org/)) format) that runs an
[L4S](https://l4steam.github.io/)-enabled kernel that uses the [TCP
Prague](https://netdevconf.info/0x13/session.html?talk-tcp-prague-l4s)
congestion controller by default. [Mininet](http://mininet.org/) is also
installed, to enable easier experimentation with L4S and TCP Prague.

A pre-built version of the box can be downloaded as an artifact of the latest
[GitHub Action](https://github.com/larseggert/l4s-box/actions).
