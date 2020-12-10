New to NBD? Set everything up!
#####################################


In order to connect to all NBD facilities from outside the
office you will require VPN verification via OVPN. Here you 
have a short guideline on how to do it:


MAC
------------

1) Install tunnelblick `here <https://tunnelblick.net/downloads.html>`_ (stable version prefered)

2) Download the .ovpn, .cert, .key and other files in a same folder (ask your IT manager)

3) Drag the .ovpn file to tunnelblick icon on the top-right bar of your MAC and enter your username/password (ask IT manager)

.. figure:: tunnelblick.png
    :scale: 50%
    :align: center


4) You shoud be able to connect to ``ssh -X username@10.8.0.1`` from commandline


Windows
-------------


vpn
++++++

1) Install OpenVPN `here <https://openvpn.net/community-downloads/>`_ (stable version prefered)

2) Copy the .ovpn, .cert, .key and other files in OpenVPN/config

.. figure:: openvpn1.png
    :scale: 50%
    :align: center

3) Click the openVPN icon on the low bar of your computer and connect

4) You should be able to  ``ssh -X username@10.8.0.1`` from the window's cmd (type cmd on windows search to open it)

Winscp
++++++++

To easily manage files between machines install winscp.

1) Install winscp `here <https://winscp.net/eng/download.php>`_ (stable version prefered)

2) Open winscp and set the hostname (10.8.0.1) port (22) username (your_username) and password (your password)

3) You will be able to manage files between your laptop and the server. Do the same for the cluster (host: 94.24.113.46 / port: 22022) and the office machine (host: 192.168.1.4 / port: 22)
