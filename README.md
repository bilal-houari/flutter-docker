# Flutter Development Container

## Purpose

This configuration sets up a development container for Flutter projects with a focus on Android development using physical devices. It is particularly helpful for Linux users (Tested in Fedora) where additional setup may be required for USB debugging.

**Important Note:** This configuration does not currently support emulators. You can extend the setup to include emulator support if needed, but this would require additional configuration and is not covered in this README.

## Usage

### 1. Setting Up Your Android Device

1. **Enable USB Debugging:** On your Android device, enable Developer Options and turn on USB Debugging.
2. **Connect Your Device:** Connect your device to your PC via USB.
3. **Identify Device IDs:** Run `lsusb` in a terminal and find your device. Note the two numbers after "ID" (XXXX and YYYY).
4. **Update udev Rules:** Run the following command, replacing XXXX and YYYY with your device's IDs:
```bash
echo 'SUBSYSTEM=="usb", ATTR{idVendor}=="XXXX", ATTR{idProduct}=="YYYY", MODE="0666", GROUP="plugdev"' | sudo tee /etc/udev/rules.d/51-android.rules > /dev/null && sudo service udev restart
```
5. **Update Dockerfile:** Open `.devcontainer/Dockerfile` and find the same command. Replace XXXX and YYYY with your device's IDs there as well.

### 2. Using the Development Container

1. **Place the Folder:** Place the `.devcontainer/` folder in the root directory of your Flutter project.
2. **Install VS Code Extension:** Install the "Dev Containers" extension in VS Code for a seamless experience.
3. **Reopen in Container:** Reopen your project in the container. VS Code should automatically detect the configuration and build the container.

## Additional Notes

* The container is configured to use the stable branch of the Flutter SDK.
* The container includes essential tools and packages for Flutter development.
* You may need to install additional tools or dependencies depending on your specific project requirements.
* Only Android development is enabled, you can enable the rest in `Dockerfile`.
