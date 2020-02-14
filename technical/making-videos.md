# Producing Videos

Your sweet new simulation just finished and you want to share it with the world, but all you have is a folder full of .pngs, how annoying.
Not to fear, ffmpeg is here!

## Prepare software

This process works for any string of images with a naming pattern, but Jay wrote this after making a Synchrono video from Chrono::Sensor output images.

You'll need the `ffmpeg` tool, available on both pacman (Arch) and yum (CentOS) under that name.
You might also need the H264 codecs which come bundled with the VLC movie player.
There are almost certainly other ways to get the codecs but I found installing VLC the most painless since VLC is a nice app to have anyways.

## String together the images

Go to the directory with your images and run the command:
    
    ffmpeg -r <fps> -f image2 -s <resolution> -i <path_to_images>/frame_%d.png -vcodec libx264 -crf 25  -pix_fmt yuv420p <output_name>.mp4

Where `fps` is the frames per second (e.g. 60) and `resolution` is something like 1920x1080.
The path you pass to the i flag is mostly a normal path except for the last part where you specify the naming pattern for your images.
Mine were called `frame_1.png`, `frame_2.png`, ... `frame_213.png`, etc... so you can see in the example above the `%d` specifier tells `ffmpeg` to look for an incrementing integer (it will complain about any gaps) at the end of the images names.
You can read about more complex filename patterns [on wikibooks](https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence#Filename_patterns).

## Add a Chrono Watermark

Good branding is important, so don't send out a video without a Chrono or SBEl watermark.
You can find a couple of options in the [Animations/Overlay](https://uwmadison.box.com/s/nnfg6vsupmydz0gbhqgbh5ta06dl75vw) folder on the Box.
You'll also use ffmpeg to add the watermark, I suppose it's possible there's a nifty one-step command to string the pngs and add a watermark all at once but walk before you run as they say.

    ffmpeg -i input.mp4 -i watermark.png -filter_complex "overlay=0:0" output.mp4

The options should be self-explanatory.
If your overlay isn't the same size as your video, you can use the `overlay=x:y` option to position it's top left corner properly (0, 0 is in the top left corner, with the positive direction being bottom right).
Many of the Chrono overlays are just as large as a typical video so 0:0 works just fine.

## Share the video

The Animations folder on Box is a good place for most images.