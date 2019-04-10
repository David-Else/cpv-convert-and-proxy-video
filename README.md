# CPV - Convert and Proxy Video

High quality, high speed shell script for converting and creating files for use
in video editing software.

- Losslessly converts video files to the .mkv container for compatibility with
  video editing software.

- Additionally creates lower resolution proxy files to use for editing to save
  CPU for replacement on final render.

Some video editing software does not like certain file formats (like .MTS), and
often you need to create much lower resolution versions of your source video to
be able to edit without the CPU overloading. Some software automatically
generates these 'proxy' files, and others, like Reaper, does not.

Tested for use in [Reaper](https://www.reaper.fm/) using FFmpeg as video
decoder.

## Dependencies

Requires [FFmpeg ](https://ffmpeg.org/) installed and available on the command
line.

## Usage

```
cpv.sh [options] [filename]

Optional arguments:

-c  specify container (defaults to .MTS)
-i  specify input file
-a  proccess all files in the directory

Examples:

cpv -i test.MTS     convert file to .mkv
cpv -c .mp4 -a      convert all files with .mp4 extensions in current directory
cpv -a              convert all files in current directory with default .MTS extension
```

## Editing proxy file defaults

You can edit this line of code in the script:

```
local video_settings="libx264 -preset ultrafast -crf 0 -vf scale=480:-1"
```

`-crf 0` lossless encoding for speed/low CPU use, but very large file
[FFmpeg H.264 Video Encoding Guide](https://trac.ffmpeg.org/wiki/Encode/H.264)

`-vf scale=480:-1` reduce resolution to 480p preserving aspect ration
[FFmpeg Filters Documentation](https://ffmpeg.org/ffmpeg-filters.html#scale-1)
