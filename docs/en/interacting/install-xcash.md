---
title: IInstalling XCash-Labs software
---
# Installing XCash-Labs software

So now you have downloaded and verified the software package. This secting is from the a end users standpoint. If you want to run a node see [Delegated Proof of Private Stake (DPOPS)](../interacting/dpops/get-started.md).

## Wallet

??? abstract ## "Installing xcash-gui on Windows (tested on windows 10/11)"

    1. At this point you should have xcash-gui-win-x64-v0.18.4.3.exe install package on your desktop.
    
    2. Right click the install package icon and clik Properties.
    
    3. At the bottom of the general block, click Unblock and then OK.
    
    4. Then double click the install package icon and just follow the prompts.

??? abstract "Installing xcash-gui on Ubuntu (tested on Ubuntu Desktop 22.04)"

    1. At this point you should have `xcash-gui-linux-x64-v0.18.4.3.tar.bz2` on your desktop.

    2. Open a terminal and navigate to your Desktop
    
    3. Extract the archive

    ```
    tar -xjf xcash-gui-linux-x64-v0.18.4.3.tar.bz2
    ```

    This will create a folder such as:

    ```
    xcash-gui-linux-x64-v0.18.4.3
    ```

    4. Open the folder and make the GUI wallet and the appimage executable (only needed once)

    ```
    chmod +x xcash-wallet-gui
    chmod +x xcash-wallet-gui.AppImage
    ```

    5. Start the wallet

    ```
    ./xcash-wallet-gui.AppImage (or just double click the icon if on Ubuntu Desktop)
    ```

??? abstract "Installing xcash-wallet-cli on Windows (tested on windows 10/11)"

    1. At this point you should have xcash-gui-win-x64-v0.18.4.3.exe install package on your desktop.

    2. Right click the zip file and clik Properties.
    
    3. At the bottom of the general block, click Unblock and then OK.

    !!! warning "Windows SmartScreen / Antivirus warning"

        Some antivirus tools may flag the download as `Win32/Contebrew.A!ml` or similar.

        This is a **false positive** that can occur with newly built or unsigned binaries.

        The official XCash-Labs releases are safe when downloaded from the official site and when the SHA-256 hash matches the value published on the downloads page.

        If Windows quarantines the file:

        1. Open **Windows Security**
        2. Go to **Protection history**
        3. Locate the blocked file
        4. Choose **Allow on device**

    2. Right click on the download zip file and extract all.
    
    3. There should be two files extracted (the bat file and the exe).  Just double click the .bat file to get started.

    4. In the batch file, you may want to change the daemon address to one that is geographically close to you.
    !!! info
        --daemon-address seeds.xcashseeds.us:18281