# camctl
Fan/pump speed control on Linux for NZXT Kraken X62 (possibly other editions)

# DISCLAIMER
Use at your **own risk**, I take **NO** responsibility if anything crazy happens. Neither does NZXT as they are not involved.

With that said however, this is basic stuff - nothing crazy has happened in my testing, and I can't think of a reason why anything bad could happen.

## Supported devices

* NZXT Kraken X62

If you have an earlier version of the NZXT Kraken than those listed here, I recommend looking at https://github.com/jaksi/leviathan

## Tested on
Fedora 25 x64 Kernel 4.10.10-200.fc25.x86_64

## Dependencies
* Python 3
* pyusb ```sudo python3 -m pip install pyusb```

## Installation
```Shell
sudo ./install.sh
```

## Usage
```Shell
sudo camctl --help
```
