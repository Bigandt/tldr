# ffmpeg

> Video conversion tool.
> More information: <https://ffmpeg.org>.

- Extract the sound from a video and save it as MP3:

`ffmpeg -i {{video.mp4}} -vn {{sound}}.mp3`

- Convert frames from a video or GIF into individual numbered images:

`ffmpeg -i {{video.mpg|video.gif}} {{frame_%d.png}}`

- Combine numbered images (frame_1.jpg, frame_2.jpg, etc) into a video or GIF:

`ffmpeg -i {{frame_%d.jpg}} -f image2 {{video.mpg|video.gif}}`

- Quickly extract a single frame from a video at time mm:ss and save it as a 128x128 resolution image:

`ffmpeg -ss {{mm:ss}} -i {{video.mp4}} -frames 1 -s {{128x128}} -f image2 {{image.png}}`

- Trim a video from a given start time mm:ss to an end time mm2:ss2 (omit the -to flag to trim till the end):

`ffmpeg -ss {{mm:ss}} -to {{mm2:ss2}} -i {{video.mp4}} -codec copy {{output.mp4}}`

- Convert AVI video to MP4. AAC Audio @ 128kbit, h264 Video @ CRF 23:

`ffmpeg -i {{input_video}}.avi -codec:audio aac -b:audio 128k -codec:video libx264 -crf 23 {{output_video}}.mp4`

- Remux MKV video to MP4 without re-encoding audio or video streams:

`ffmpeg -i {{input_video}}.mkv -codec copy {{output_video}}.mp4`

- Convert MP4 video to VP9 codec. For the best quality, use a CRF value (recommended range 15-35) and -b:video MUST be 0:

`ffmpeg -i {{input_video}}.mp4 -codec:video libvpx-vp9 -crf {{30}} -b:video 0 -codec:audio libopus -vbr on -threads {{number_of_threads}} {{output_video}}.webm`

- Make video into a slideshow

(https://stackoverflow.com/questions/12100072/how-to-extract-slides-from-a-video-using-python)
(https://www.linux.com/training-tutorials/how-sort-and-remove-duplicate-photos-linux/)
(http://manpages.ubuntu.com/manpages/impish/man1/findimagedupes.1p.html)
(https://askubuntu.com/questions/246647/convert-a-directory-of-jpeg-files-to-a-single-pdf-document)

`ffmpeg -i Undervisning_1.mp4 -vsync 0 -vf select="eq(pict_type\,PICT_TYPE_I)" -s 1280x720 -f image2 slide-%04d.jpg`

`findimagedupes -t 98% . > dup.txt`

```
# https://askubuntu.com/questions/344407/how-to-read-complete-line-in-for-loop-with-spaces
#!/bin/bash

videoName='0_Undervisning_2.mp4'

ffmpeg -i $videoName -vsync 0 -vf select="eq(pict_type\,PICT_TYPE_I)" -s 1280x720 -f image2 ./slides/slide-%04d.jpg

cd ./slides

findimagedupes -t 98% . > duplicates.txt

IFS=$'\n'       # make newlines the only separator
COUNTER=0
for f in $(cat duplicates.txt) 
do
	i="1"
	IFS=$' \t\n'
	COUNTER=$[$COUNTER +1]
	echo "Deleting duplicate $COUNTER"
	for file in $f 
	do
		if [[ "$i" -eq "1" ]]
		then
			i="0"
		else 
			rm $file
		fi	
	done	
done
```

```
ls -1 ./*jpg | sort -z | xargs -L1 -I {} img2pdf {} -o ./{}.pdf
```

```
# https://medium.com/@akhileshjoshi123/merge-pdfs-with-python-d4d3bfbdbd3b

from PyPDF2 import PdfFileMerger
from os import listdir


input_dir = "C:/Users/jeab/git/eco/ae/slides/" #your input directory path

merge_list = []

for x in listdir(input_dir):
    if not x.endswith('.pdf'):
        continue
    print(x)    
    merge_list.append(input_dir + x)

merger = PdfFileMerger()

for pdf in merge_list:
    merger.append(pdf)

merger.write("C:/Users/jeab/git/eco/ae/0_Undervisning_2.pdf") #your output directory
merger.close()
```