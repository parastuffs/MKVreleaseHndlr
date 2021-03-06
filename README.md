MKV Release Handler
===================
Script written in order to save some time in the process
of producing an mkv video from different pieces.
It requires the *String::CRC32* perl library and the *mkvtoolnix* as well as
*mktorrent* packages.

What it does
------------
```
Usage: ./MKVreleaseHndlr.pl [options]
Options
-v vid1,vid2,... 	adding videos
-s script1,script2,... 	adding subtitles scripts
-c chaptersFile     	adding chapters
-f dir                  adding fonts directory
-b                      specify if it's a blu-ray release
-g group                specify fansub group to tag in the release name
--season                Season of the show; will be appended right after the show name
-h                      display this help

Require 'mktorrent', 'mkvtoolnix' ('mkvmerge' & 'mkvinfo') and String::CRC32.
https://github.com/parastuffs/MKVreleaseHndlr
```

The script will produce an mkv video following this patern: 
```
[group]_show_season_-_episode_bluray_definition_bitDepth_[CRC32].mkv.
```
The files will then be passed to mktorrent in order to create one torrent per 
file that will be copied to /srv/ftp/, being the local directory of the FTP server hosted on the machine.


How it works
------------
### Video definition
Through mkvinfo, the height of the video is displayed at '|   + Pixel height: 720'.

### Video bit depth, episode and show
By regex on the video name given as a parameter to the script.

### Fonts
The archive is extracted to fonts/ based on the file extension. All the fonts are then
listed and saved.
