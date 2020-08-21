# usb_rsync

Introduction:
-------------

"usb_rsync" is a bash script which uses rsync via a USB cable connected Android mobile phone to backup internal phone camera storage to computer.


Benefits:
---------

It is easy to connect using the highest speed USB cable connection available for the data transfer (eg 10mb/sec with USB-C).

More convenient and more secure than using a network connection especially if travelling.

"rsync" provides incremental copy so that only new files are transfered. This is useful if
the mobile storage is in, say, the 10s of GB.

Once the initial copy is complete and the local mirror copy established
then subsequent copies are only needed of newly added files (photos, etc).

A log of the details of the transfer is written to ~/logs/usb_rsync for reference and overview.


 Installing:
 -----------
 
 Clone the script to your local filespace:
 
     cd ~/Downloads && git clone https://github.com/wikigazer/usb_rsync

This will create ~/Downloads/usb_rsync/ and the script will be in ~/Downloads/usb_rsync/usb_rsync

Example:

    [user@localhost Downloads]$ cd usb_rsync/
    [user@localhost usb_rsync (master)]$ ls -l
    total 60
    -rw-r--r-- 1 user user 35149 Aug  9 17:59 LICENSE
    -rw-r--r-- 1 user user   112 Aug  9 17:59 README.md
    -rw-r--r-- 1 user user 18722 Aug  9 17:59 usb_rsync

Copy to your local bin directory, review and modify as needed (see next section "Before Using") then change permissions to execute.

    cp  ~Downloads/usb_rsync/usb_rsync ~/bin/usb_rsync
    vi ~/bin/usb_rsync      # review and modify as needed for #LOCAL needs
    chmod +x ~bin/usb_rsync
 
 
Before using:
-------------
Review the usb_rsync script and consider any changes for your local situation. Look for "#LOCAL" for hints.
This has been developed and tested on Mageia Linux with an LG G7+ mobile.

For the mount of the internal storage on the Android mobile to work, "gvfs-fuse" needs to be installed
and the kernel module "fuse" to be loaded. "usb_rsync" checks for these.

When the USB cable is connected: the path for Android internal storage is automatically mounted under:

    "/run/user/"${UID}"/gvfs/mtp:host=*/*/"

In "usb_rsync" local storage on computer has been initally defined as:

    local_dir=${HOME}/Photos_rsync/G7+_ThinQ/LM_G710/internal_storage/
    
                        ^               ^      ^
            rsync data /               /      /
                         device name  /      /
                                     model  /
  

How to use:
-----------
a) Connect Android mobile to computer (using highest speed USB connection available).

b) On computer, run: "usb_rsync".

c) Monitor progress: "tail -f ~/logs/usb_rsync".

d) When completed the mobile storage is automatically un-mounted so USB cable may be disconnected.
