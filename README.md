# youtubeClone

Build a rough skeleton of YouTube where the core functionality of YouTube is implemented. Requirements include:

- users can sign in and out using their Google account
- users can upload videos while signed in
- videos should be transcoded to multiple formats (ex: 360p, 720p)
- users can view a list of uploaded videos (signed in or not)
- users can view individual videos (signed in or not)

This project builds upon the fullstack course provided by [NeetCode.io](https://neetcode.io/). 

___

***All source code is commented and own design diagrams are included to demonstrate independent understanding. Additional features are also added (enhanced UI, video titles, comment section, reaction bar)***

## Tech Stack
- TypeScript
- Next.js
- Express.js
- Docker
- FFmpeg
- Firebase Auth, Functions, Firestore
- Google Cloud Storage, Pub/Sub, Run

## High Level Design

Video Storage: Google Cloud Storage used to host raw and processed videos.

Video Upload Events: when a video is uploaded, publish a messaged to a Cloud Pub/Sub topic. Allos for a durability layer for video upload events and asynchrnous video processing.

Video Processing Workers: when a video upload event is published, a video processing worker received a message from Pub/Sub and transcodes the video.

Video Metadata: after a video is processed, store the metadata in Firestore. This allows for processed videos to be displayed in the web client along with other relevant info (ex: title, description, etc)

Video API: use Firebase Functions to build a simple API that allows users to upload videos and retrieve video metadata.


Web Client: use Next.js to build a simple web client that will allow users to sign in and upload videos. Web client hosted on Cloud Run.

Authentication: use Firebase Auth to handle user authentication. Allows for easy integration with Goolge Sign In.
