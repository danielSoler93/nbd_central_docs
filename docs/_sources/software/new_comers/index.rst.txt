New to NBD? Set everything up!
#####################################


In order to connect to all NBD facilities from outside the
office you will require VPN verification via OVPN. Here you 
have a short guideline on how to do it:


MAC
------------

1) Install tunnelblick `here <https://tunnelblick.net/downloads.html>`_ (stable version prefered)


2) Drag the .ovpn file (ask your IT manager) to tunnelblick icon on the top-right bar of your MAC.

.. figure:: tunnelblick.png
    :scale: 50%
    :align: center


3) You shoud be able to connect to ``ssh -X username@10.8.0.1`` from commandline

