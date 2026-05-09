# Install Instructions for 'ptouch-print'

To use the program, it must be compiled on your computer. The following instructions show step by step how to compile the source code.
Afterwards, the program can be found in the folder `~/.local/bin/ptouch-print` and can be called from in the terminal using `ptouch-print`.

Note: These instructions where tested on *Ubuntu 22.04 LTS*, but should work on other Debian-based distributions as well.

The Documentation from the maker of this program can be found here: https://dominic.familie-radermacher.ch/projekte/ptouch-print/


### Install dependencies:

```bash
sudo apt update
sudo apt install libgd-dev install build-essential cmake gettext libgd-dev libusb-1.0-0-dev pkg-config git
```

### Download and build:

```bash
cd ~/.local
git clone https://github.com/chabala/ptouch-print.git
```

```bash
cd ~/.local/ptouch-print
./compile.sh
```

### Set udev rules for ptouch-print:
```bash
cd ~/.local/ptouch-print/udev
sudo cp 20-usb-ptouch-permissions.rules /etc/udev/rules.d/
```
```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

### test ptouch-print:
```bash
~/.local/ptouch-print/build/ptouch-print
# output should be something like: PT-D450 found on USB bus 3, device 7
```

### add ptouch-print to local PATH variable:

```bash
echo 'export PATH="$HOME/.local/ptouch-print/build:$PATH"' >> ~/.bashrc
source ~/.bashrc
```


## Basic Usage:

For detailed usage instructions, please refer to the official documentation from the maker of this program:
https://dominic.familie-radermacher.ch/projekte/ptouch-print/

### print help
```bash
ptouch-print --help
```

### 2-line label
```bash
ptouch-print --text "Zeile 1" --newline "Zeile 2"
```

### multiple labels with cutmarks
```bash
ptouch-print --text "Label 1" --cutmark --text "Label 2"
``` 

### print with a specific font and size
```bash
ptouch-print --font "Ubuntu:bold" --fontsize 23 --text Blahblah
```

### make a test print into a png file
```bash
ptouch-print --fontsize 16 --text Blahblah --writepng ~/Desktop/LABEL_OUTPUT.png
```