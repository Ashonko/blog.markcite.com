---
title: "How to Download Protected File From Google Drive"
date: 2021-10-24T12:30:24+06:00
featureImage: images/blog/tutorials/other/google-drive-download/feature-small.png
postImage: images/blog/tutorials/other/google-drive-download/feature-large.png
---
### Warning
This is solely for educational purposes. 

### My use case 
My wife wanted to enroll in an online course, but the deadline had passed. When she contacted the center, they informed her that they had recorded classes from the previous two days, and that she could join and catch up with the current batch if she so desired. However, they usually delete the recorded videos within 7 days. However, we decided to enroll in the course, but discovered that the watch hours of the recorded classes were too many to cover in a few days, and the files were protected, so there was no way to download and watch them later. So, here's how I easily got around the restrictions and downloaded the video files.

### Steps to Download Protected Video from Google Drive
- Play the video in Google Drive.
- Click **command** + **option** + **C** in Mac and **Ctrl** + **Shift** + **C** in Windows.
- Click on the video element with **Select an element** pointer. You'll find something like `<video tabindex="-1" ... src="https://rr2---sn-cvh76ned.c.drive.google.com/videoplayback?expire=163507218....20211019.01.00"></video>` code in it.
- Copy the link inside `src` and paste it in a new tab and the video file will start playing.
- Below in the lower-right corner, you'll find three dots where you'll get the option for downloding the video file.

Note that, the link is most porbably dynamic and should change within a few time. If the link changes, you'll not be able to download that file.