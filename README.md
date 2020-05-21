# GlobalProtect App for Linux

Arch Linux package

## Setup

1. Obtain the app package from your IT administrator or
  check at [Palo Alto website](https://docs.paloaltonetworks.com/globalprotect/4-1/globalprotect-app-user-guide/globalprotect-app-for-linux.html)

2. Unpack on the same directory you cloned this repository.

    There must be a `GlobalProtect_UI_tar-X.X.X_X.tgz` file.

3. Install

    ```
    makepkg -sri
    ```

    - Note: This will also start the `gpd` service

4. Start the GPA user service

    ```
    systenctl --user enable gpa
    systenctl --user start gpa
    ```

5. Start the **Global Protect** app,

    or add to your autostart.

    ```
    cp /opt/paloaltonetworks/globalprotect/PanGPUI.desktop ~/.config/autostart
    ```
