[###](###) == Xserver ==


Simply install xauth on your machine and enable x11 forwarding in your Vagrantfile.

```
config.ssh.forward_agent = true
config.ssh.forward_x11 = true
```

### == SnapShots ==

For better management of snaps
```vagrant plugin install vagrant-vbox-snapshot```
