
# MacBook Bridge/T2 Linux Driver
A driver for MacBook models 2018 and newer, implementing the VHCI (required for mouse/keyboard/etc.) and audio functionality.

The project is divided into 3 main components:
- BCE (Buffer Copy Engine) - this is what the files in the root directory are for. This estabilishes a basic communication channel with the T2. VHCI and Audio both require this component.
- VHCI - this is a virtual USB host controller; keyboard, mouse and other system components are provided by this component (other drivers use this host controller to provide more functionality, however USB drivers are not in this project's scope).
- Audio - a driver for the T2 audio interface, currently only audio output is supported.

Please note that the `master` branch does not currently support system suspend and resume.

If you want to support me, you can do so by donating to me on PayPal: https://paypal.me/mcmrarm

# About this specific fork

Updated fork to use the built-in keyboard on MacBook Air* / MacBook Pro* with Open Mandriva 5.x (*Laptops with Intel chipsets)


## Requirements

You need clang and other tools to build the module. Grab it with:

```
dnf install task-devel
```

You also need the kernel headers files. Fetch it with:

```
dnf install kernel-desktop-devel
```

Finally you need a kernel tool  called _dkms_ to make the process easier:

```
dnf install dkms
```


## Build

### Tarball

Download the tarball (zip) from Github and extract the content to the following directory on your local machine:

```
/usr/src/apple-bce-0.1
```

### Compile & install

Just open a terminal and type

```
sudo dkms install apple-bce/0.1
```

When done, activate the module with the following command:

```
sudo modprobe apple-bce
```

### Login screen

To make the keyboard usable at the login screen, create the file 

```
/usr/lib/modules-load.d/apple-bce.conf
```

Then add a single line with the module name 

```
apple-bce
```

You are good to go !

### The end

It's time now to:

```
reboot
```
