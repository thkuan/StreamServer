# StreamServer

## Getting Started
[**ffserver**](https://www.ffmpeg.org/ffserver.html)
[**ffmpeg**](https://www.ffmpeg.org/ffmpeg.html)

![Behavior Description](./ffserver%20and%20ffmpeg.png)

## Check webcam devices

### Device Check
List all webcam devices we had
``` sh
lsusb
```
It would show like this: 
```
Bus 001 Device 007: ID 046d:081b Logitech, Inc. Webcam C310
```

### Support Format 
List available formats and exit
``` sh
ffplay -f video4linux2 -list_formats all /dev/video0
```
It would show like this:
```
[video4linux2,v4l2 @ 0x7f5f98000920] Raw       :     yuyv422 :           YUYV 4:2:2 : 640x480 160x120 176x144 320x176 320x240 352x288 432x240 544x288 640x360 752x416 800x448 800x600 864x480 960x544 960x720 1024x576 1184x656 1280x720 1280x960
[video4linux2,v4l2 @ 0x7f5f98000920] Compressed:       mjpeg :          Motion-JPEG : 640x480 160x120 176x144 320x176 320x240 352x288 432x240 544x288 640x360 752x416 800x448 800x600 864x480 960x544 960x720 1024x576 1184x656 1280x720 1280x960
/dev/video0: Immediate exit requested
```

### Functional Test 
Try to record a video and then display 
``` sh
ffmpeg -f video4linux2 -input_format mjpeg -i /dev/video0 out.mpeg
```

## Running the test

### Start ffserver by using designated configuration file
``` sh
ffserver -f ffserver.conf
```

### Encode live video/audio stream to ffserver
``` sh
ffmpeg -f video4linux2 -pixel_format bgr24 -video_size vga -i /dev/video0 http://localhost:8090/webcam.ffm
```

## Browse and view the stream
```
http://$(dev_ip):$(dev_port)/facstream.mjpeg
```
