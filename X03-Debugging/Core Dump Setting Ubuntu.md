
Disable apport `sudo systemctl disable apport`

Then, set kernel.core_pattern
`sudo sysctl -w kernel.core_pattern=core.%u.%p.%t` # to enable core generation

then change ulimit
`ulimit -c unknown`

Core dump is in the working directory now.

The changes don't persist past reboot .

Note: 
Disabling apport will persist. To make the sysctl change persist, store it in a custom file in `/etc/sysctl.d` To make the ulimit change persist... I'm not sure if it's still `/etc/security/limits.conf` or if some systemd supersedes that :) 
 
Without needing to reboot, once done, you can restore apport as-is with: 
```
sudo systemctl enable apport; 
sudo systemctl start apport; 
sudo sysctl -w kernel.core_pattern='|/usr/share/apport/apport %p %s %c %d %P %E'; 
ulimit -S -c 0 – 
```

