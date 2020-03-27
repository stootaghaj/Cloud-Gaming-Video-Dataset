# Cloud-Gaming-Video-Dataset
 

All the dataset material can be found in the following link: 
Link: https://drive.google.com/open?id=1wfiuShlLcbpjMkQ3ZkIlJAYcZeEwlifl 

**It has to be noted that some videos are not publicly available due to unclear copy-right state. 

The dataset has four folders as follows:

1.	Subject Ratings: subjective ratings together with additional pre/post-game ratings. Raw subjective rating will be realized upon acceptance of the paper. 

2.	MOS information: The Mean Opinion Score (MOS) information is provided together with some plots lined to MOS ratings. Below you can find the abbreviations of scales in the shared excel file. 
   - Video Quality in 7-point continues scale (VQ_EC), Video Fragmentation in 7-point continues scale (VF_EC),	Video Unclearness in 7-point continues scale (VU_EC),	Video Discontinuety in 7-point continues scale (VD_EC),	Acceptance of condition in 7-point continues scale (after averaging binary individuale values and scaled it up) (AC_EC), 	Video Quality in 5-point continues scale (VQ_ACR),	Video Fragmentation in 7-point continues scale (VF_ACR),	Video Unclearness in 7-point continues scale (VU_ACR),	Video Discontinuety in 7-point continues scale (VD_ACR),	Acceptance of condition in 7-point continues scale (after averaging binary individuale values and scaled it up) (AC_ACR)

3.	Plots and Metrics: the results of objective metrics are provided in frame level as well video level together with some scatter plots of each metric and subjective results. The plot and frame-level information of metrics will be uploaded in few days. 

4.	Materials: the raw reference sequence in YUV format together with encoded videos in mp4 format at spatial resolutions are provided in this folder.

In order to encode the video we used the following command on ffmpeg:

ffmpeg -y -r ${framerate} -s:v 1920x1080 -i ${file} -r ${framerate} -c:v h264_nvenc -rc cbr_ld_hq -preset llhq -zerolatency 1 -forced-idr 1 -pixel_format yuv420p -b:v $bitrate$'k' -minrate $bitrate$'k' -maxrate $bitrate$'k' -bufsize $bitrate$'k' ${file%.*}_${encodingresolution}_${framerate}_${bitrate}_${codec}.mp4

In order to rescale the videos to 1080p we used bilinear method as follows:

ffmpeg -y -i ${file%.*}.mp4 -filter:v scale=1920:1080 -sws_flags "bilinear" -vcodec rawvideo -pix_fmt yuv420p -f rawvideo PATH/${file%.*}.yuv
