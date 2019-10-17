Visualize through vpn efficiently
===================================

To render&visualize GUIs of any software (maestro, vmd, pymol ...) thorugh vpn you must follow the next steps:


1- Activate the vpn with your password

2- Connect to  https://172.16.1.3:28443/enginframe/vdi/ with your normal useraccount&password

3- On the left panel go to Services>Linux Desktop

4- Double click on the new linux desktop that will appear in the central panel to connect to the machine

5- You will enter in the nbdcalc01 computer (Nexus office) where you can visualize and calculate schordinger jobs

6- Open a terminal and run the next commands to deactivate the screen lock: (Temporal step until we fix it with nice distributors)

    - ``gsettings set org.gnome.desktop.screensaver lock-enabled false``
    - ``gsettings set org.gnome.desktop.lockdown disable-lock-screen true``


