### yt-dlp commands 

##### Download a Video or playlist
yt-dlp <video_url>
yt-dlp <playlist_url>

##### Download a video in a custom name or in a specific directory
yt-dlp -o 'Abdul Kalam Wings of Fire Autobiography' https://www.youtube.com/watch?v=t5b20oLaIaw
yt-dlp -o '~/Downloads/Abdul Kalam Biography' https://www.youtube.com/watch?v=t5b20oLaIaw

##### Display all available video or playlist formats
yt-dlp -F https://www.youtube.com/watch?v=t5b20oLaIaw

##### Download Videos in best Quality 
yt-dlp -f best https://www.youtube.com/watch?v=t5b20oLaIaw
yt-dlp -f bestaudio https://www.youtube.com/watch?v=t5b20oLaIaw
yt-dlp -f bestvideo+bestaudio https://www.youtube.com/watch?v=t5b20oLaIaw

##### Download Videos in lowest quality
yt-dlp -f worstvideo <URL>

##### Download videos using format ID
yt-dlp -f 247 https://www.youtube.com/watch?v=t5b20oLaIaw
yt-dlp -f 22 https://www.youtube.com/watch?v=t5b20oLaIaw

##### Download audo only from video (-x)
yt-dlp -x https://www.youtube.com/watch?v=t5b20oLaIaw

##### Download audio only from video (with format: mp3)
yt-dlp -x --audio-format mp3 "https://www.youtube.com/watch?v=rjRV0G6qWgw"

##### To make yt-dlp always give you an MP4 container file with MPEG video and audio:
-------------
yt-dlp -S res,ext:mp4:m4a --recode mp4 "https://www.youtube.com/watch?v=rjRV0G6qWgw"

----------
This command takes a YouTube playlist link as input, then uses the previously-mentioned -x --audio-format mp3 option
to convert each file to MP3 format. Then it sets the YouTube video's thumbnail image as the album artwork, the video 
title as the song title and filename, and the channel name as the artist. After it's done, I can import those songs 
into my music library, and all the metadata is already there.

yt-dlp -i -x --audio-format mp3 --embed-thumbnail --add-metadata --metadata-from-title "%(title)s" --parse-metadata "title:%(title)s" --parse-metadata "uploader:%(artist)s" --output "%(title)s.%(ext)s" "https://www.youtube.com/playlist?list=PL3i9BHIRvTES0rAWLTOImQE6T1Rix1b5P"


