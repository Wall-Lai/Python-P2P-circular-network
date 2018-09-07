# Python-P2P-circular-network
Developed for COMP9331 at UNSW

An example shell script (using gnome) would be:
#!/bin/bash
gnome-terminal --title PEER 30 -e "python3 p2p.py 30 32 34" &
gnome-terminal --title PEER 32 -e "python3 p2p.py 32 34 36" &
gnome-terminal --title PEER 34 -e "python3 p2p.py 34 36 30" &
gnome-terminal --title PEER 36 -e "python3 p2p.py 36 30 32" &
exit 0

This will open 4 terminals with the folloiwng:
Peer 30 with first peer 32 and second 34.
Peer 32 with first peer 34 and second 36.
Peer 34 with first peer 36 and second 30.
Peer 36 with first peer 34 and second 36.

peers are limited to the following criteria 0 <= peer <= 255.

The network will ping its successors every 2 seconds, if five successive pings are not the peers will self update.
This can occur if one peer is unexpectably shut.
Furthermore, if a quit is typed into the terminal of a peer, the peer will quit and peers will be updated.

File requesting:
Files can be requested (just for demonstration purposes), using a hash function between 0 and 9999.
The file number is hashed using file%256.The peer storing that file will be the next number after the has number.
For example:
1 is stored at 30.
35 is stored at 36.
36 is stored at 36. 
255 is stored at 30.
