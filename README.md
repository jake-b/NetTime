### Introduction
 
This is the Apple sample code “NetTime” that syncs with the old “TIME” protocol on port 37.  Many servers don’t support this, but the NIST servers still do.

A few notes:

	- The 711000 system patch changes the base time from January 1st 1993 to 2006.
	  In similarly, an offset in this code needed to be updated to calculate the
	  correct time.

	- This app uses a TIME server (Port 37). This is an old and largely discontinued
	  service in favor of the NTP protocol (Port 123).  You need a time server that
	  supports the older protocol.  the NIST time servers apparently still do:
	  
	  					http://tf.nist.gov/tf-cgi/servers.cgi

	- There's apparently a "newer" or "modified" version of NetTime.pkg that has a
	  checkmark for enabling/disabling auto synchronization and a button to "Sync Now"
	  My version of the source did not have these features, but I added back a 
	  "Sync Now" button.

	- A added some print statements for debugging, so fire up Inspector or Minspector
	  if you're having trouble and maybe you'll see something useful.

### How to Handle Resource Forks in this repository

This is stolen from the [Dash Board README](https://github.com/masonmark/Dash-Board-for-Newton-OS/blob/master/README.md).   This is the process by which you can split the resource forks to standard files for use with git, and then put them back to use with Mac Classic.

1. Clone the repo to your Mac OS X 10.x System
2. In the terminal, cd into the top level folder of the repo
3. To hack on the source code, you must re-assemble all the files, which to be used with git have been split into separate data and resource forks (AppleDouble format). To do so, try this command:

        /System/Library/CoreServices/FixupResourceForks .

  and do not omit that trailing . or who knows what the hell might happen.
4. Use the SheepShaver emulator to boot Mac OS 9, and configure it to mount the OS X folder containing the repo as a disk. *Don't copy the repo to your SheepShaver VM's native storage, because it seems to lose the invisible git dirs when copying it back, thereby corrupting the repo.*
5. Hack, hack, hack, build.
6. Once you have completed a change you want to commit to the git repo, quit out of Newton Toolkit, and then go back to the OS X side of things. Again cd into the repo root dir, and run this command:

        SplitForks .

  This will again split the resource forks off of all files who have one, and store them as a separate invisible file (AppleDouble format). This convoluted dance is necessary because git absolutely doesn't work with resource forks and Newton Toolkit absolutely doesn't work without them.
7. Commit your changes, then treat yourself to a frosty beverage.