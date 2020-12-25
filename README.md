# Resolume Streamer

Easy set up to feed video stream from Resolume to a video wall made of Raspberry PIs.


## Streaming Tools

* Resolume: generates video feed and sends video via NDI
* OBS-Studio: captures NID signal and sends video via RTMP
* NGINX Streaming server: receives RTMP and provides HLS
* Javascript Webpage: reads HLS and puts media source in a HTML5 video element


## Resolume

* Download and install Resolume
* Download and install NDI Tools
* Resolume Toolbar > Output > Network Streaming (NDI)

> More detailed [HERE](https://resolume.com/support/en/streaming)


## OBS-Studio

* Download and install [OBS-Studio](https://obsproject.com/download)
* Download and install [NDI plugin](https://obsproject.com/forum/resources/obs-ndi-newtek-ndi%E2%84%A2-integration-into-obs-studio.528/)
* Select NDI source (maybe needs restart after install) and use '<FOOBAR.LOCAL> (Arena - Composition)' as source name
* Open 'Settings' and choose 'Stream' and fill it e.g.:
    ```
    Service:    Custom
    Server:     rtmp://<your server ip>/live
    Stream Key: mystream
    ```


## Streaming Server

Set up taken from [HERE](https://hub.docker.com/r/jasonrivers/nginx-rtmp) to build a streaming server.

build it:                   `$ docker build -t rtmp-server . --target=rtmp-server`
run in development with:    `$ docker run -p 1935:1935 -p 8080:8080 rtmp-server`


## Website

Contains a little express (JS) server that servers a website containing the video element.

set up node server:      `$ npm install`
run in development with: `$ npm run devStart`
