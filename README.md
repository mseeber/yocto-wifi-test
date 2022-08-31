# Layer stack for testing wifi functionality inside qemu with mac80211\_hwsim


## Setup

The layers need to be added to bblayers manually.

This should look something like this in bblayers.conf

```
BBLAYERS ?= " \
  /workdir/poky/meta \
  /workdir/poky/meta-poky \
  /workdir/poky/meta-yocto-bsp \
  /workdir/meta-qt5 \
  /workdir/meta-wifi-test \
  /workdir/build/workspace \
  /workdir/meta-openembedded/meta-oe \
  /workdir/meta-openembedded/meta-python \
  /workdir/meta-openembedded/meta-networking \
  "
```

Workspace may only appear after devtool was used.

## Usage

All configuration happens in meta-wifi-test. 

To build the image run:

    bitbake wifi-test-image

To run the image in qemu:

    runqemu qemux86-64 wifi-test-image slirp nographic


Currently to have NetworkManager or ConnMan work properly,
dnsmasq and hostapd services have to be disabled (inactive)

To prepare for testing, run the image and after login:

    modprobe mac80211_hwsim

Now, the system should be ready for testing WiFi related functionality.
