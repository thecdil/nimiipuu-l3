# migration notes

https://objects.lib.uidaho.edu/nimiipuu-l3/

https://docs.google.com/spreadsheets/d/1W7oJt1AUgAXwbF6ZKaGrCRXZdwOToAktIDeN_7fvWm0/edit?gid=0#gid=0

https://codebeautify.org/html-to-markdown

## ffmpeg rm to mp4

ffmpeg -i nimiipuu-l3-001.rm -c:v libx264 -preset slower -c:a aac nimiipuu-l3-001-slower.mp4

for file in *.rm; do ffmpeg -i "$file" -vcodec libx264 -preset slower -acodec aac "${file%.rm}.mp4"; done

## ffmpeg rm to mp3

simple:
for file in *.rm; do ffmpeg -i "$file" -vn "${file%.rm}.mp3"; done

set parameters:
for file in *.rm; do ffmpeg -i "$file" -vn -ar 44100 -b:a 192k "${file%.rm}.mp3"; done

just keep as mp4 for lossless copy:
for file in *.rm; do ffmpeg -i "$file" -vn -preset slower -acodec aac "${file%.rm}.mp4"; done

## ffmpeg generate thumbnails from video

timestamp:
for file in *.mp4; do ffmpeg -i "$file" -ss 00:00:05 -frames:v 1 "${file%.mp4}.png"; done

auto thumb:
for file in *.mp4; do ffmpeg -i "$file" -vf "thumbnail" -frames:v 1 "${file%.mp4}.png"; done
