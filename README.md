# Linux

## ping: socket: Operation not permitted

Some distros by default will allow only a specific subset of users to ping.
We can edit a kernel config and enable it for all users.

```bash
echo 'net.ipv4.ping_group_range = 0 2147483647' > /etc/sysctl.d/99-ping.conf
sysctl -p /etc/sysctl.d/99-ping.conf
```

### References

- https://fedoraproject.org/wiki/Changes/EnableSysctlPingGroupRange
- https://github.com/systemd/systemd/pull/13141
- https://github.com/systemd/systemd/blob/main/sysctl.d/50-default.conf


## LG29 Ultrawide display working with an `AMD HD 5850`
X.Org must be used. The following Modeline works "fine"
```
Modeline “2560x1080x53.92” 162.500000 2560 2608 2640 2720 1080 1083 1087 1108 +HSync -VSync
```

https://forum.manjaro.org/t/it-is-possible-to-use-2560x1080-resolution-on-linux-using-ati-radeon/21315/13

Assuming that it is connected to the `HDMI-1` port:
```bash
#/bin/sh

[ "$XDG_SESSION_TYPE" = x11 ] || exit 0

xrandr --newmode “2560x1080x53.92” 162.500000 2560 2608 2640 2720 1080 1083 1087 1108 +HSync -VSync
xrandr --addmode HDMI-0 “2560x1080x53.92”
xrandr --verbose --output HDMI-0 --mode “2560x1080x53.92” 
```
This will create and activate the mode.

# Docker
## docker-compose documentation

- https://github.com/compose-spec
- https://github.com/compose-spec/compose-spec/blob/master/spec.md
- https://github.com/compose-spec/compose-spec/blob/master/deploy.md

## Tini - A tiny but valid init for containers

```dockerfile
# Add Tini
ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]
```

### References

- https://github.com/krallin/tini
