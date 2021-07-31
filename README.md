# libudev-stub

[Libudev-stub](https://github.com/suhan-paradkar/libudev-stub) is a shim library for `libudev`, created primarily for the Windows Subsystem for Linux [WSL](https://msdn.microsoft.com/en-us/commandline/wsl/about). Theoretically it could be useful for other Linux-ish systems that lack udev support. [Udev](https://www.freedesktop.org/software/systemd/man/udev.html) is part of [systemd](https://www.freedesktop.org/wiki/Software/systemd/). It provides a well-known interface for device events (such as hot plugging of usb dongles and cameras) for many Linux distributions like [Ubuntu](https://www.ubuntu.com/). Unfortunately, WSL currently lacks much of the functionality required to support `udev`; at least as of [Windows Insider](https://insider.windows.com/) build 16257.

`libudev-stub` implements a subset of the `libudev` interface and does not actually communicate with the kernel. The theory of operation is pretty straightforward. When an application uses `libudev` to ask for a list of devices, the stub library says there aren't any devices worth mentioning. When an application asks to monitor for device events, the library obliges, and then never raises any event notifications. The code is structured in a way that a static device list could be faked, but it does not do so as of right now.

```
bash
```

Then,

```bash
wget https://github.com/suhan-paradkar/tewmux-disabled/releases/download/udev-stub/libudev-stub_228_$(dpkg --print-architecture).deb
dpkg -i libudev-stub_228_aarch64.deb
```
## Hacking

There is also an environment variable to turn the stub library into a passthrough proxy for the real `libudev.so.1`. It is useful to see where applications fail when using the `libudev` interface. Enable it with:
```
export LIBUDEV_STUB_PASSTHROUGH=$PREFIX/lib/libudev.so.1.6.4
```
