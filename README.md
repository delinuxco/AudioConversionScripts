# AudioConversionScripts
 A series of linux shell scripts for converting audio formats in batch process,
 example .wav to .flac   or .m4a to .mp3 and .flac to .wav etc.

Reasons for scripts
 These were orignally created for batch processing of multiple audio files with a one simple command. Just navigate to the directory where the audio files are and run the appropriate command.

 If you have a PLEX server and you can't get the server to find your .flac files even
 though they are there, the flac to flac scripts will usually cure most of these issues.
 
 You can also extract audio directly from webm and mp4 video formats.

![acs](https://user-images.githubusercontent.com/69424808/134647094-35839985-142f-4b45-b255-190c8b0b0fa9.gif)

----------------------

## Dependencies
 * linux system
 * ffmpeg

---------------------

## Installation
 Clone repo, or download zip file and unzip. From terminal, cd to directory
 AudioConversionScripts and run the command:

 `cp -r acs ~/.local/bin/`

 This will copy the folder "acs" to your local/bin directory. Which in most systems
 should be in your $PATH. 

 Next,the scripts need to be made executable by running these two commands:

 `chmod +x ~/.local/bin/acs/*`
 `chmod +x ~/.local/bin/acs/.acs`

 Now from the terminal, check if your local/bin is in your PATH by running:

 `echo "$PATH"`

 If you don't see /home/user_name/.local/bin then, you will need to add it.
 
 Edit your ~/.bashrc or ~/.bash_profile and add the following at the end of the file:

 `export PATH=$PATH: ~/.local/bin`

 You may have to logout and back in for changes to take effect.

### Multi-thread performace
 The scripts by default are set to use 2 threads, you can change this by editing the script
 directly and changing the FFMPEG flag *"-threads 2"* what what ever number of threads you want.
 But for those of you with many threads, you are limited by your IO, so too many threads can actually
 hurt performance.

---------------------

## How to use
 Because the scripts are in a folder that is in your PATH, executing the scripts is easy.
 First to see all of the current format combinations, open a terminal and type:

 `.acs` 

 Be sure to include the period at the beginning. You should see a list like this

 * flac-flac-43
 * flac-flac-44
 * flac-flac-48
 * flac-m4a-44
 * flac-m4a-48
 * flac-ogg-44
 * flac-wav-44
 * flac-wav-48
 * m4a-flac-43
 * m4a-flac-44
 * m4a-flac-48
 * m4a-mp3-44
 * mp3-m4a-44
 * mp3-m4a-48
 * mp3-ogg-43
 * mp3-ogg-44
 * mp3-ogg-48
 * mp4-flac-43
 * mp4-flac-44
 * mp4-flac-48
 * ogg-m4a-44
 * ogg-m4a-48
 * wav-flac-43
 * wav-flac-44
 * wav-flac-48
 * wav-m4a-44
 * wav-m4a-48
 * wav-mp3-44
 * webm-flac-43
 * webm-flac-44
 * webm-flac-48

 The script name says what it does, for example "wav-flac-48" means that the script
 will convert files with a .wav extentions to .flac with a sample rate of 48000.
 Make a copy of a directory with audio files with an extention of either flac, m4a or
 mp3 etc. Open a terminal in that directory and if your files are .flac, and you want to
 convert them to .wav, simply type: flac-wav-48 and the script will convert all files
 in the current directory to .wav files. 

 The numbers at the end of the file name represent sample rates:
 * 43 = 43200
 * 44 = 44100
 * 48 = 48000

 To encode files in .m4a, ffmpeg will need to have *libfdk_aac* enabled/compiled.

 NOTE: The existing files will be deleted, so ALWAYS work with copies of original files.

---------------------

# Creating your own custom scripts
 If you have other formats that you would like to convert, you can easily use any of
 of the existing scripts as a template. The only thing that need to be changed is
 the *iext* & *oext* extensions and the FFMPEG settings line if applicable. Save the file
 under a new name in the acs folder and make the new script executable. Do not add
 the .sh extention to the new script.

![acs_example](https://user-images.githubusercontent.com/69424808/134644593-0fbfa4fc-a6dd-44d2-9c5a-0ab96c602b16.png)

 When editing the FFMPEG flags (the green box in the above image), it is imparitive that
 the spaces before and after are there (red arrows) or the script will fail. You can add
 as many flags in the green box as necessary.

# Bulk Batch processing
 To batch process multiple directories, a separate script will execute the necessary script per directory.
 simply edit the *bulkbatch* file in ~/.local/bin/acs with your favorite editor. Edit/add the directories
 in the the section ***User Section ***. Please note that you may encounter errors in transcoding which causes
 the script to stop. As always, never work with origianl files, ALWAYS copies!

 To use the script, once edited to your liking, simply run `bulkbatch` from the terminal, does not matter the
 location where the script is executed.
