# Build

This will permanently modify your system, so it is preferred to build this snap in a disposable environment, such as an LXD container.
The build **MUST** be performed on **Ubuntu 22.04**.

```sh
grep 'deb [arch=amd64]' /etc/apt/sources.list &>/dev/null
if [ "$?" = "0" ]; then
    sudo sed 's/deb /deb [arch=amd64] /' -i /etc/apt/sources.list
fi

snap install snapcraft --classic

cd kernel
snapcraft

cd ../gadget
snapcraft

cd ..
snap install ubuntu-image --classic
ubuntu-image snap soquartz.model \
    --snap gadget/*.snap \
    --snap kernel/*.snap
```

# Install
```sh
sudo dd if=quartz64.img bs=4M of=/dev/sdX status=progress oflag=sync
```
