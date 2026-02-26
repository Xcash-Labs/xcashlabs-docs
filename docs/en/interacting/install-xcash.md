---
title: IInstalling XCash-Labs software
---
# Installing XCash-Labs software

So now you have downloaded and verified the software package. This secting is from the a end users standpoint. If you want to run a node see [Delegated Proof of Private Stake (DPOPS)](../interacting/dpops/get-started.md).

## Wallet Instalation

??? abstract "Installing xcash-gui on Windows (tested on Windows 10/11)"

    1. At this point you should have `xcash-gui-win-x64-v0.18.4.3.exe` on your desktop.

    2. Right-click the installer and select **Properties**.

    3. At the bottom of the **General** tab, click **Unblock**, then click **OK**.

    4. Double-click the installer and follow the setup prompts.

    5. After installation, launch **XCash Wallet GUI** from the Start Menu.

    The wallet will automatically start the network daemon (`xcashd`) and begin blockchain synchronization.

??? abstract "Installing xcash-gui on Ubuntu (tested on Ubuntu Desktop 22.04)"

    1. At this point you should have `xcash-gui-linux-x64-v0.18.4.3.tar.bz2` on your server or desktop.

    2. Open a terminal and navigate to the download location

    ```
    cd ~/Desktop
    ```
    *(or wherever the file was downloaded)*

    3. Extract the archive

    ```
    tar -xjf xcash-gui-linux-x64-v0.18.4.3.tar.bz2
    ```

    This will create a folder such as:

    ```
    xcash-gui-linux-x64-v0.18.4.3
    ```

    4. Open the folder

    ```
    cd xcash-gui-linux-x64-v0.18.4.3
    ```

    5. Make the GUI wallet executable (only needed once)

    ```
    chmod +x xcash-wallet-gui
    ```

    If an AppImage is included, also run:

    ```
    chmod +x xcash-wallet-gui.AppImage
    ```

    6. Start the wallet

    ```
    ./xcash-wallet-gui
    ```

    If using the AppImage:

    ```
    ./xcash-wallet-gui.AppImage
    ```

    You can also double-click the file if using Ubuntu Desktop.

??? abstract "Installing xcash-wallet-cli on Windows (tested on Windows 10/11)"

    1. At this point you should have `win-x64-v0.18.3.4-xck-beta1.zip` on your desktop.

    2. Right-click the `.zip` file and select **Properties**.

    3. At the bottom of the **General** tab, click **Unblock**, then click **OK**.

    !!! warning "Windows SmartScreen / Antivirus warning"

        Some antivirus tools may flag the download as `Win32/Contebrew.A!ml` or similar.

        This is a **false positive** that can occur with newly built or unsigned binaries.

        Official XCash-Labs releases are safe when downloaded from the official site and when the SHA-256 hash matches the value published on the downloads page.

        If Windows quarantines the file:

        1. Open **Windows Security**
        2. Go to **Protection history**
        3. Locate the blocked file
        4. Choose **Allow on device**

    4. Right-click the `.zip` file and select **Extract All**.

    5. Open the extracted folder. You should see:

       - `xcash-wallet-cli.exe`
       - `run-wallet.bat`

    6. Double-click `run-wallet.bat` to start the wallet.

    7. (Optional) You may edit the batch file to change the daemon address to one geographically close to you.

    !!! info
        Example daemon address:

        ```
        --daemon-address seeds.xcashseeds.us:18281
        ```

??? abstract "Installing xcash-wallet-cli on Ubuntu (tested on Ubuntu Desktop 22.04)"

    1. At this point you should have `linux-x64-v0.18.3.4-xck-beta1.zip` on your server or desktop.

    2. Open a terminal and navigate to the download location

    ```
    cd ~/Desktop
    ```
    *(or wherever the file was downloaded)*

    3. Extract the archive

    ```
    unzip linux-x64-v0.18.3.4-xck-beta1.zip
    ```

    This will create a folder such as:

    ```
    linux-x64-v0.18.3.4-xck-beta1
    ```

    4. Open the folder

    ```
    cd linux-x64-v0.18.3.4-xck-beta1
    ```

    5. Make the wallet executable (only needed once)

    ```
    chmod +x xcash-wallet-cli
    chmod +x run-wallet.sh
    ```

    6. Start the wallet

    ```
    ./run-wallet.sh
    ```

    7. In the .sh file, you may want to change the daemon address to one that is geographically close to you.
    !!! info
        --daemon-address seeds.xcashseeds.us:1828