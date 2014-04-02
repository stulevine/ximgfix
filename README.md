xe1fix
======

A simple Perl script I to adjust the date of files on an SDXC SD card that contains Fujifilm X-E1 JPG and RAF files.

There is a know issue when shooting with an SDXC SD Card and the Fujifilm X-E1 camera where by the file created date is not properly set and different from the "data taken" in the file's EXIF info.  This makes it rather difficult to sort by date last modified since the files have the incorrect data associated with it.  Fujifilm is aware of this issue.  However, there is no ETA on a firmware solution.

With that said, and as an interim measure, I have created a short Perl script to adjust the creation date of the files on the card to coinside with the the EXIF information in the files (both JPG and RAF).

The script is efficient in that it keeps track of the files already fixed on the SD card (setting the create date to the "date taken" from the EXIF info of the JPG files).  I run this script on the SD card just before I transfer the images to my computer and it handles both the JPG and RAF files on the card setting the proper create date.  The script also keeps a running record of what files it has modified in a file on the SD card called ".filemods".  In this way I can have several cards each with separate state information.  If you initialize the SD card, then the next time you shoot with it, mount it on your computer and run the script, a new file is created to keep track of the file mods.

While the script is rather short and efficient, it does require the following Perl modules to be installed before the script will run successfully (use 'perl -MCPAN -e shell' from the command line to install them):

  Cwd;
  Image::ExifTool
  HTTP::Date;
  Tie::File::AsHash;

To install the script:

  sudo cp ximgfix /usr/local/bin/ximgfix

To run the script

  ximgfix [SD Card Name] [folder number]

For example, my SD card is names X-E2 and I have two folders in the DCIM directory, 100_FUJI and 101_FUJI.  Since I've already run this script for the former folder, and all new photos go into 101_FUJI,  I would run ximgfix as follows:

  ximgfix X-E2 101

You'll see a progression of "." chars as it processes the files and sets the proper create date from the image's embedded EXIF info followed by the number of files processed when the script finished.  That's it.
