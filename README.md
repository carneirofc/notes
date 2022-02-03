# notes

Useful information on various topics

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

## Docker: Tini - A tiny but valid init for containers

```dockerfile
# Add Tini
ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]
```

### References

- https://github.com/krallin/tini
