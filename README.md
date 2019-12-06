# webcam-express-server
NodeJs ExpressJs webcam streaming server so clients can connect via webstream

##Instructions
 - Run this webservice so that incoming data streams can be broadcast to clients.
```
npm run start
```
 - Get a video stream and point to 8081 of this service. As an example, you could use ffmpeg:
 ```
ffmpeg -loglevel info -f dshow -i video="Webcam C170" -vcodec mpeg1video -r 30 -g 60 -s 1024x768 -pix_fmt yuyv422 -f mpegts http://127.0.0.1:8081/[YOUR_PASSWORD]
ffmpeg -loglevel info -f dshow -i video="Integrated Webcam" -vcodec mpeg1video -r 30 -g 60 -s 1024x768 -pix_fmt yuyv422 -f mpegts http://127.0.0.1:8081/[YOUR_PASSWORD]
```
 - Attach clients to the feed by connecting on port 8082:
 ```html
<!DOCTYPE html>
<html>
<head>
    <title>JSMpeg Stream Client</title>
    <style type="text/css">
        html, body {
            background-color: #111;
            text-align: center;
        }
    </style>

</head>
<body>
<canvas id="video-canvas" style="width:1024px; height:768px"></canvas>
<script type="text/javascript" src="jsmpeg.min.js"></script>
<script type="text/javascript">
    var canvas = document.getElementById('video-canvas');
    var url = 'ws://127.0.0.1:8082/';
    var player = new JSMpeg.Player(url, {canvas: canvas});
</script>
</body>
</html>
```

##Useful FFMPEG Commands

 - List supported devices
```
ffmpeg -list_devices true -f dshow -i dummy
```

 - List supported options on selected device
```
ffmpeg -list_options true -f dshow -i video="Webcam C170"
ffmpeg -list_options true -f dshow -i video="Integrated Webcam"
```

 - Play the webcam in a new window
```
ffplay -f dshow -video_size 1280x720 -i video="Webcam C170"
ffplay -f dshow -video_size 1280x720 -i video="Integrated Webcam"
```
