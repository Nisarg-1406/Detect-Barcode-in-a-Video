# Detect-Barcode-in-a-Video
To Detect the Barcode in a Video

## Table of Contents - 
* [About Project](#about-project)
* [Detailed Explanation about Project](#detailed-explanation-about-project)
* [About Me](#about-me)

## About Project
This project aims for the detecting the barcode in a video and then scanning the barcode and detect the object for the barcode detected. The code is executed in python language in Jupyter Notebook.

## Detailed Explanation about Project
* First install necessary libraries. 
  1) `from imutils.video import VideoStream` - Importing VideoStream for Video Processing. 
  2) `import argparse` - For parsing command line arguments. For Video Processing, time module is Important. 
  3) `import time` - This module provides various time-related functions.
  4) `import cv2` - OpenCV. 
  
* Then if the video path was not supplied, we use the command `vs = VideoStream(src=0).start()` to start the Web Camera to detect the barcode, Here we use `time.sleep()` which tells the number of seconds for which the code is required to be stopped so that code executes in efficient ways, Else we load the Video with the help of this command - `cv2.VideoCapture(args["video"])`. 
    ```
    if not args.get("video", False):
      vs = VideoStream(src=0).start()
      time.sleep(2.0)
    else:
      vs = cv2.VideoCapture(args["video"])
    ```

* Now we start looping over the frames of our video — this loop will continue to run until the video runs out of frames or we press the letter `q` key on our keyboard and break from the loop. Then we query our `vs`, which returns a 2-tuple in the output using `frame = vs.read()`, and then with the help of `frame = frame[1] if args.get("video", False) else frame`, we would decide if we are using VideoStream  or cv2.VideoCapture. If we are completed by taking all the frames, we break of the loop. 
    ```
    frame = vs.read()
    frame = frame[1] if args.get("video", False) else frame
    if frame is None:
		  break
    ```
  
* Next is we would find the bounding bax, and if bounding box is found, then to draw the counters. To draw the counters - `cv2.drawContours` function is used. It can also be used to draw any shape provided you have its boundary points. Its first argument is source image, second argument is the contours which should be passed as a Python list, third argument is index of contours (useful when drawing individual contour. To draw all contours, pass -1) and remaining arguments are color, thickness etc. and then we would be showing the frame if the user presses a key, then when `q` is pressed we stop the loop. This can be achieve with - `cv2.waitKey(0) & 0xFF` i.e means `cv2.waitKey()` returns a 32 Bit integer value (might be dependent on the platform). The key input is in ASCII which is an 8 Bit integer value. So you only care about these 8 bits and want all other bits to be 0. For more details for this, you can refer this - `https://stackoverflow.com/questions/35372700/whats-0xff-for-in-cv2-waitkey1`. 
    ```
    if box is not None:
      cv2.drawContours(frame, [box], -1, (0, 255, 0), 2)
    cv2.imshow("Frame", frame)
    key = cv2.waitKey(1) & 0xFF

    # if the 'q' key is pressed, stop the loop
    if key == ord("q"):
      break
    ```
    
  
