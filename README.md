## AR Tag Detection, Decoding and Imposition

The first part of the project involves detecting and decoding the AR tag code. The second part of the project involves imposing an 2-D image and 2-D cube onto the AR tag.

The project focuses on detecting a custom AR Tag (a form of fiducial marker), that is used for obtaining a point of reference in the real world, such as in augmented reality applications. The two aspects to using an AR Tag: detection and tracking, has been implemented in this project. Following are the 2 stages:

Detection: Involves finding the AR Tag from a given image sequence
Tracking: Involves keeping the tag in “view” throughout the sequence and performing image processing operations based on the tag’s orientation and position (a.k.a. the pose).

Prior to the implementation of image processing on the image sequence, the video is split into its image frames using cv2.VideoCapture, and once the operations are performed on each of the frames, it is appended into an array. This image array is then used to get the video back using cv2.VideoWriter

Edge Detection of AR tag

AR Tags facilitate the appearance of virtual objects, games, and animations within the real world. The analysis of these tags can be done as followed.

 The tag has been decomposed into an 8*8 grid of squares, which includes a padding of 2 squares width along the borders. This allows easy detection of the tag when placed on white background.
 
    
The inner 4*4 grid (i.e. after removing the padding) has the orientation depicted by a white square in the lower-right corner. This represents the upright position of the tag. This is different for each of the tags provided in the different image sequences.

Lastly, the inner-most 2*2 grid (i.e. after removing the padding and the orientation grids) encodes the binary representation of the tag’s ID, which is ordered in the clockwise direction from least significant bit to most significant. So, the top-left square is the least significant bit, and the bottom-left square is the most significant bit.

The process of the edge and corner detection has been implemented in the following way:

   The video stream is first converted into image frames.
    Detection is performed on each of the frames and then taking the fps as 25, the video is formed again.
    In the code, the function Edgedetecion has been scripted which takes in the image, the old corners that can been computed and returns the new coordinates of the detected corners. This is repeated for each image frame.
    The Computer Vision methods made use of in the above implementation are:
        cv2.cvtColor
        cv2.medianBlur
        cv2.threshold
        cv2.findContours
        cv2arcLength
        cv2.approxPolyDP
        cv2.contourArea
        cv2.isContourConvex
    Once the Corners are successfully detected, the perspective transformation of the Tag is performed. The function perspective for tag has been scripted to get the transformed and resized tag image. The methods used for the transformation are:
        cv2.findHomography
        cv2.warpPerspective
        cv2.resize
    After the above successful transformation the ID of the tag is obtained, the corners of the tag as well as its ID with respect to its original orientation i.e compensated for any camera rotation is obatined.
    The above process has been written in Python using several functionalities of Computer Vision such as Contours and Corner Detection algorithms.


# Dependencies: 
Pytho3 

OpenCV-Python

Numpy

# AR tag:
![Reference AR Tag to be detected and tracked](data/reference_images/ref_marker.png)

# AR tag grid:
![Reference AR Tag in grid](data/reference_images/ref_marker_grid.png)

# Detection: 
Involves finding the outer corners of the AR tag from a video.
# Decoding:
Involves finding the AR code based on inner 2x2 grid of the AR tag.

# Imposing:
Involves superimposing Lena image and a virual 3-D cube onto the AR tag.

![Lena image](data/reference_images/Lena.png)

# Steps for finding the AR tag id:
```
cd code
python3 detection.py
```
# Sample output for AR tag detection:
Output shown in the video frame:

<a href="https://imgflip.com/gif/3qf8dw"><img src="https://i.imgflip.com/3qf8dw.gif" title="made at imgflip.com"/></a>

<a href="https://imgflip.com/gif/3qf8ig"><img src="https://i.imgflip.com/3qf8ig.gif" title="made at imgflip.com"/></a>

<a href="https://imgflip.com/gif/3qf8mv"><img src="https://i.imgflip.com/3qf8mv.gif" title="made at imgflip.com"/></a>

![Output from Tag1 video](report/images/tag_id_outputvideo0.JPG)

Output shown in the AR tag with respect to orientation:

![Output from Tag1 video](report/images/warping_opencv.JPG)

# Steps for superimposing Lena image onto the AR tag
```
cd code
python3 imposing.py
```
# Sample output:

![Output from Tag1 video](report/images/Tag0_videooutput.JPG)

<a href="https://imgflip.com/gif/3qf5ez"><img src="https://i.imgflip.com/3qf5ez.gif" title="made at imgflip.com"/></a>

<a href="https://imgflip.com/gif/3qf5wq"><img src="https://i.imgflip.com/3qf5wq.gif" title="made at imgflip.com"/></a>

<a href="https://imgflip.com/gif/3qf602"><img src="https://i.imgflip.com/3qf602.gif" title="made at imgflip.com"/></a>

# Steps for superimposing virtual 3-D onto the AR tag
```
cd code
python3 virtual_cube_projection.py
```
# Sample output:
![Output from Tag2 video](report/images/Tag2_cube.JPG)

<a href="https://imgflip.com/gif/3qf6dl"><img src="https://i.imgflip.com/3qf6dl.gif" title="made at imgflip.com"/></a>

<a href="https://imgflip.com/gif/3qf6h0"><img src="https://i.imgflip.com/3qf6h0.gif" title="made at imgflip.com"/></a>

<a href="https://imgflip.com/gif/3qf6j8"><img src="https://i.imgflip.com/3qf6j8.gif" title="made at imgflip.com"/></a>

