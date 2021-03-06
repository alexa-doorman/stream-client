# alexa-doorman-streaming-client

## Description
This client needs to be installed on the device that will capture images. 

## Dependencies
1. Python 3.6
1. OpenCV 3
1. Flask

## Authentication

Included, `example.env`, is a file you need fill out and rename to `.env`. You can skip the following steps if you fill that file out. Git will ignore this file once it's renamed.

### Stream Auth (this server)

Notice these lines of code in `app.py`

```
USER_DATA = {
    os.environ['STREAM_ROOT_USERNAME']: os.environ['STREAM_ROOT_PASSWORD'],
    os.environ['STREAM_API_USERNAME']: os.environ['STREAM_API_PASSWORD']
}
```

This sets two users, one being root (you) and one for the API to use. Although this is basic, as long as your environment doesn't get compromised you should be fine.

Make sure to set `STREAM_ROOT_USERNAME`, `STREAM_ROOT_PASSWORD`, and `STREAM_API_PASSWORD` as two different passwords! Change them anytime to revoke access.


### Objection Detection Auth

`utils.py`

```
DETECT_API_CREDENTIALS = {
    'user': os.environ['DETECT_API_USERNAME'],
    'pass': os.environ['DETECT_API_PASSWORD']
}
```

## Usage 
1. **IMPORTANT** [debain based devices] Run `sudo modprobe bcm2835-v4l2` to enable pi camera to work with opencv video capture


## Docker Image Usage
1. Docker Image - https://hub.docker.com/r/doorman/stream-client/

### OpenCV
1. `sudo docker run --previleged -MAX_IO_RETRIES=5 -e -CAMERA=opencv -e DEBUG=True --volume "/home/pi/projects/stream-client:/src/app" -p 5000:5000 doorman/stream-client`

### ArduCam
1. `sudo docker run --previleged -e MAX_IO_RETRIES=5 -e CAMERA=arducam -e SERIAL_PORT=/dev/ttyACM0 -e DEBUG=True --volume "/home/pi/projects/stream-client:/src/app" -p 5000:5000 doorman/stream-client`



## Tested Platforms
1. Windows
1. Raspbian Stretch
2. Intel Edison/jubilinux


## Credits
Miguel Grinberg for the initial streaming section
http://blog.miguelgrinberg.com/post/video-streaming-with-flask