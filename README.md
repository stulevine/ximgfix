xe1fix
======

A simple Perl script I to adjust the date of files on an SDXC SD card that contains Fujifilm X-E1 JPG and RAF files.

There is a know issue when shooting with an SDXC SD Card and the Fujifilm X-E1 camera where by the file created date is not properly set and different from the "data taken" in the file's EXIF info.  This makes it rather difficult to sort by date last modified since the files have the incorrect data associated with it.  Fujifilm is aware of this issue.  However, there is no ETA on a firmware solution.

With that said, and as an interim measure, I have created a short Perl script to adjust the creation date of the files on the card to coinside with the the EXIF information in the files (both JPG and RAF).

The script is efficient in that it keeps track of the files already fixed on the SD card (setting the create date to the "date taken" from the EXIF info of the JPG files).  I run this script on the SD card just before I transfer the images to my computer and it handles both the JPG and RAF files on the card setting the proper create date.  The script also keeps a running record of what files it has modified in a file on the SD card called ".filemods".  In this way I can have several cards each with separate state information.  If you initialize the SD card, then the next time you shoot with it, mount it on your computer and run the script, a new file is created to keep track of the file mods.

While the script is rather short and efficient, it does require the following Perl modules to be installed before the script will run successfully:

  Cwd;
  Image::ExifTool
  HTTP::Date;
  Tie::File::AsHash;

To install the script:

  sudo cp xe1fix /usr/local/bin/xe1fix

To run the script

  1) cd to your SD card directory where the files are located
  2) xe1fix

You'll see a progression of "." chars as it processes the files and sets the proper create date followed by the number of files processed when the script finished.  That's it.
