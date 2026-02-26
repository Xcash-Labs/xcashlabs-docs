---
title: IInstalling XCash-Labs software
---
# Installing XCash-Labs software

So now you have downloaded and verified the software package. This secting is from the a end users standpoint. If you want to run a node see [Delegated Proof of Private Stake (DPOPS)](../interacting/dpops/get-started.md).

## Wallet

??? abstract "Installing xcash-gui on Windows (tested on 10/11)"

    1. At this point you should have xcash-gui-win-x64-v0.18.4.3.exe install package on your desktop.
    
    2. Right click the install package icon and clik Properties.
    
    3. At the bottom of the general block, click Unblock and then OK.
    
    4. Then double click the install package icon and just follow the prompts.

??? abstract "Installing xcash-gui on Ubuntu (tested on Ubuntu Desktop 22.04)"

    ### 1. At this point you should have `xcash-gui-linux-x64-v0.18.4.3.tar.bz2` on your desktop.

    ### 2. Open a terminal and navigate to your Desktop
    
    ### 3. Extract the archive

    ```
    tar -xjf xcash-gui-linux-x64-v0.18.4.3.tar.bz2
    ```

    This will create a folder such as:

    ```
    xcash-gui-linux-x64-v0.18.4.3
    ```

    ### 4. Open the folder and make the GUI wallet and the appimage executable (only needed once)

    ```
    chmod +x xcash-wallet-gui
    chmod +x xcash-wallet-gui.AppImage
    ```

    ### 6. Start the wallet

    ```
    ./xcash-wallet-gui.AppImage (or just double click the icon if on Ubuntu Desktop)
    ```