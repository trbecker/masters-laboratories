# Installation
Follow the installation instructions in https://openaicellular.github.io/oaic/oran_installation.html and https://openaicellular.github.io/oaic/srsRAN_installation.html. Make sure that you upgrade the kernel to `linux-image-5.8.0-63-lowlatency` otherwise sctp may not be available.

Also, enable sctp at startup.
```
echo sctp  > /etc/modules-load.d/sctp.conf
```

# Helper installation
```
ln -s $PWD/bin/start-srsenb /usr/local/bin/
ln -s $PWD/srsepc.service /lib/systemd/system
ln -s $PWD/srsenb.service /lib/systemd/system
ln -s $PWD/netns@.service /lib/systemd/system
systemctl daemon-reload
systemctl enable --now srsepc
systemctl enable --now netns@ue1
systemctl start srsenb
```

- `srsenb` needs to be started mannually, as the e2term address will only be available late in the boot process.
- `netns@.service` can be instantiated for each UE netns, e.g. `systemctl enable --now netns@ue2` for a second UE. For multiple UEs, see https://openaicellular.github.io/oaic/multi_ue_example.html.
