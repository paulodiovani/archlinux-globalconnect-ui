# GlobalProtect App for Linux

Arch Linux package

## Setup

### Install from a release (not public available)

1. Grab the latest [Release](https://github.secureserver.net/v-pgoncalves/archlinux-globalconnect-ui/releases)
and install with.

    ```
    sudo pacman -U globalprotect-ui-X.X.X.X_X-X-any.pkg.tar.xz
    ```

    - Note: This will also start the `gpd` service

2. Start the GPA user service

    ```
    systenctl --user enable gpa
    systenctl --user start gpa
    ```

3. Start the **Global Protect** app,

    or add to your autostart.

    ```
    cp /opt/paloaltonetworks/globalprotect/PanGPUI.desktop ~/.config/autostart
    ```

### Build on your own

1. Obtain the app package from your IT administrator or
  check at [Palo Alto website](https://docs.paloaltonetworks.com/globalprotect/4-1/globalprotect-app-user-guide/globalprotect-app-for-linux.html)

2. Unpack on the same directory you cloned this repository.

    There must be a `GlobalProtect_UI_tar-X.X.X_X.tgz` file.

3. Install

    ```
    makepkg -sri
    ```

    - Note: This will also start the `gpd` service

4. Follow steps **2 and followying** from [Install from a release](#install-from-a-release)


### Throubleshooting

>  /opt/paloaltonetworks/globalprotect/PanGPUI: error while loading shared libraries: libicuuc.so.71: cannot open shared object file: No such file or directory

Install [icu71](https://aur.archlinux.org/packages/icu71) package.
