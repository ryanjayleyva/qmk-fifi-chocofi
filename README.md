# Custom Keymaps With QMK

In this guide, we'll walk you through creating a custom keymap for your mechanical keyboard using QMK. We'll cover the process from installation to flashing your keyboard with your new layout.

# Install QMK CLI using Homebrew (MAC)

First, you need to install the QMK Command Line Interface (CLI) tool. This will allow you to interact with QMK directly from your terminal.

Open your terminal and run:

```bash
brew install qmk/qmk/qmk
```

Homebrew will handle the installation for you.

# Install QMK Toolbox

The QMK Toolbox is a graphical user interface (GUI) that makes flashing your keyboard much easier.

- Download the installer for macOS from the official release page:
  [Download QMK Toolbox](https://github.com/qmk/qmk_toolbox/releases)
- Run the installer and follow the on-screen instructions to set up QMK Toolbox.

# Set Up QMK on Your Computer

Once the CLI and Toolbox are installed, we need to set up QMK on your computer. This will download the QMK firmware and related files.

In your terminal, run:

```bash
qmk setup
```

This command will clone the QMK firmware repository into a directory on your computer.

# Find Your Keyboard

To make sure QMK supports your keyboard, we need to check the list of supported keyboards. Run this command:

```bash
qmk list-keyboards
```

This will display all the keyboards that QMK supports.
For example, my keyboard is a Fifi Chocofi, which is listed as crkbd/rev1 (this is the same as the Corne keyboard).

# Create Your Custom Keymap

Now that we know your keyboard is supported, let's create a custom keymap.

To do this, run the following command in your terminal:

```bash
qmk new-keymap -kb crkbd/rev1 -km rjleyva
```

- `crkbd/rev1` is the keyboard model (change this to your keyboard model from the list if it’s different).
- `rjleyva` is the name of the keymap we’re creating. You can replace this with your own name or something meaningful to you.

This command will create a new directory for your keymap. For example, on my MacBook, it will be located at:

```bash
~/qmk_firmware/keyboards/crkbd/keymaps/rjleyva/
```

# Navigate to Your Keymap Directory

Once your keymap is created, navigate to the directory where it was saved. Run:

```bash
cd ~/qmk_firmware/keyboards/crkbd/keymaps/rjleyva/
```

This will bring you to the folder where your keymap files are located.

# Customize Your Keymap

At this point, you can edit your keymap to customize the layout as you like.

You can use any text editor to open and modify the keymap. If you're using Neovim, for example, just run:

```bash
nvim keymap.c
```

Inside `keymap.c`, you will see the default keymap, and you can start editing it. If you're unfamiliar with how to modify keymaps, you can refer to the [QMK documentation](https://docs.qmk.fm) for detailed guidance on how to configure each key and function.

# Compile Your Firmware

Once you're happy with your changes, it's time to compile the firmware. This will create a file that you can flash to your keyboard.

In your terminal, run the following command:

```bash
qmk compile -kb crkbd -km rjleyva
```

This will compile the firmware for your crkbd keyboard using the rjleyva keymap. The resulting firmware file will be saved in your `qmk_firmware` directory.

# Put Your Keyboard in Bootloader Mode

To flash your keyboard, you’ll need to put it into bootloader mode. Here’s how to do that:

- Open **QMK Toolbox** on your computer.
- Put your keyboard into bootloader mode. This is usually done by pressing a reset button on the keyboard or using a key combination (depending on your keyboard model).

After that, you should see a message in QMK Toolbox like this:

```bash
*** DFU device connected: Atmel Corp. ATmega32U4 (03EB:2FF4:0000)
```

# Open the Compiled Firmware in QMK Toolbox

Now that your keyboard is in bootloader mode, it's time to load the compiled firmware.

- In QMK Toolbox, click on the "Open" button.
- Navigate to the folder where the firmware was saved (it should be inside the `qmk_firmware` folder).
- Look for the firmware file that matches the format:

```php
<keyboard_name>_<keymap_name>.bin
```

For example, the file might be named crkbd_rjleyva.bin.

# Flash Your Keyboard

Finally, we can flash the firmware to your keyboard.

- Ensure the correct bootloader is selected in the top right corner of QMK Toolbox.
- Click Flash to start the flashing process.

**IMPORTANT**: Don’t disconnect your keyboard until the flashing process is complete.

When flashing is finished, you should see a message like this:

```bash
Flash complete
*** DFU device disconnected: Atmel Corp: ATmega32U4 (03EB:2FF4:0000)
```

Congratulations, You're Done! 🎉
