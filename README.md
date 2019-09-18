# ffmpeg cheat sheet
frequently used command

***

## [ffmpeg](https://www.ffmpeg.org/)  - frequently used command:
ffmpeg tools: **ffmpeg**, **ffplay**, **ffprobe**

***

### windows: 
cmd -> ffmpeg\bin\ffmpeg.exe

### video converter
`ffmpeg -i path\input.mov -acodec copy -vcodec copy path\output.mp4`

### key frame extraction from video
`ffmpeg -i path\input.mov -vf select='eq(pict_type\, I)' -vsync 2 -f image2 path\keyframe_%03d.jpg`

### video split
`ffmpeg -ss 00:00:00 -t 00:30:00 -i input.avi -vcodec copy -acodec copy output1.avi`\
`ffmpeg -ss 00:30:00 -t 00:30:00 -i input.avi -vcodec copy -acodec copy output2.avi`\
`ffmpeg -ss 01:00:00 -t 00:30:00 -i input.avi -vcodec copy -acodec copy output3.avi`

-ss stands for start time\
-t is the length of final clip\
-vcodec is the video codec used to encode the output file. 'copy' means we're using the same codec as the input file\
-acodec is the audio codec. Like the video codec, we'll be using the same audio codec as the input file

### change the framerate without changing the video length
`ffmpeg -i path\input.mov -r 30 -c:v libx264 -y path\output.mov`

### rotating a video
`ffmpeg -i path\input.mov -vf "transpose=1" -r 30 -sameq -acodec copy path\output.mov`  
transpose parameter use  
0 = 90CounterCLockwise and Vertical Flip (default)  
1 = 90Clockwise  
2 = 90CounterClockwise  
3 = 90Clockwise and Vertical Flip  
`-vf "transpose=2,transpose=2"` = 180 degrees  

### display your media file details
`ffmpeg -i video.mp4`  

### removing audio from a media file
`ffmpeg -i path\input.mp4 -an path\output.mp4`  

### removing video from a media file
`ffmpeg -i path\input.mp4 -vn path\output.mp3`  

### joining multiple files (same type) 
`ffmpeg -f concat -safe 0 -i path\mylist.txt -c copy output_file.format`  
`-safe 0` above is not required if the paths are relative  
mylist.txt will be like below  

file '/path/to/file1.format'  
file '/path/to/file2.format'  
file '/path/to/file3.format'    
