# mkpl - Create playlists suitable for the Chord Poly music streamer

The `mkpl` script creates playlists suitable for the Chord Poly music streamer.

Usage and options are found within the script itself.


## About Chord Poly playlists

The Chord Poly music streamer is a device that can be used to play music from various sources - including a Micro SD/TF card inserted into the Poly. In order to play the music on the card the Poly needs to be told where to find the music. This is done by creating one or more playlist files on the card. The playlist file is a text file that contains the path to the music files, relative to the root of the card. The Poly can then read the playlist file and play the music using the "quickplay" feature of the GoFigure app. The playlist files should be created in the root directory of the card, it seems that this is the only place that the Poly looks for playlists.

The `mkpl` script found here simplifies the creation of playlists for the Poly. It scans a directory hierarchy and creates a playlist file at the root of the directory for each directory that contains music files (ie. files ending with .mp3 or .flac). 

On startup the Poly scans the TF card and creates a set of database files on the root of the card. These are `art-cache-a.tar.gz`, `dlna-sdfree.dat` and `mpd.db`. If you add music and playlists to a card that already contains database files the Poly seems unable to update them and will be unable to play music from the new playlists. The only way to get the Poly to create a valid set of database files is to delete them from the card. The `-p` option of mkpl does this for you. (This problem is present at least up to and including firmware version 3.2.0.)

When the Poly is restarted with a card that doesn't have database files it will scan the card and create them. This will take some time and while scanning is happening the P-status light on the Poly will flash red/green. Once scanning is completed the P-status light will stop flashing and turn blue. At this point the Poly is ready to play music from the card.

If you remove any music on the card you will need to delete the corresponding playlist(s). 
This can be done by adding the `-z` option to the mkpl command line, it will delete all old playlists before creating new ones.

## Example
To recreate all playlists and prepare the Poly TF card for use, while logging progress to the console:
```cd /path/to/card
mkpl -v -p -z
```

