# Development of Image Processing for Welding Torch Position Based on The Thickness of Irradiation Container
This research is about the utilization of image processing for the application of measurement and determination of welding points based on thickness for irradiation container. Accuracy in the welding process of irradiation capsule parts is very necessary because considering the need for irradiation capsule specifications in the form of airtight and watertight to maintain the safety of nuclear reactors for the activation process of materials into radioisotopes. Measurements are made using *edge detection* to measure the thickness of the irradiation capsule parts and then from the measurement results, calculations are made to determine the weld point.

# Programming Requirements
This program uses the Python programming language version 3.11 written in JupyterLab. This program is developed in Windows 8 operating system.

Here is the link to [*install* Anaconda](https://www.anaconda.com/download). Install the required library namely ``OpenCV``, ``matplotlib``, ``numpy``, ``glob``, and ``pandas`` in Anaconda Prompt with the command below.
```
conda install opencv matplotlib numpy glob pandas
```
Make sure the library is installed by looking at the *packages in environment* list with the command.
```
conda list
```

# Stages of using the program
There are 3 steps before measuring and determining the weld point, namely camera calibration, camera set-up, and pixel calibration. If all stages have been carried out, the program for measuring and determining the weld point can be carried out.

## Camera Calibration
Camera calibration is done to eliminate lens distortion on the camera used. Lens distortion that occurs if left unchecked will affect the measurement results, therefore image correction is needed from the results obtained. To perform camera calibration, a set of chessboard images is required. The camera calibration performed only applies to the type of camera used and the focal length setting used.

<p align="center">
<img src="/image-markdown/algoritmKalibrasiKamera.png" width=30% align="center">
</p>

## Camera Set-up
The set-up aims to capture the desired image in the same state as the object whose image is to be processed. Image capture is performed by positioning the camera vertically perpendicular to the surface of the irradiation capsule. The position was taken to avoid geometric distortion. The camera used was a 5-50 mm 720p focal length industrial camera with a USB connection. The image capture scheme is shown below

<p align="center">
<img src="/image-markdown/skemakamera.png" width=30% align="center">
</p>

This stage will produce an image of the irradiation container as shown below.

<p align="center">
<img src="/Dataset/A1.jpg" width=70% align="center">
</p>

## Pixel Calibration
Pixel calibration is performed to convert pixel units to millimeter units. Pixel calibration is performed by detecting an image of a box with a background contrast whose physical dimensions are known. The box image is obtained by taking an image as schematized in the camera set-up stage. The box image is processed to obtain its dimensions in pixels. With the dimensions in pixels and length in millimeters known, the calibration factor can be found by calculating with the equation below.

$$\text{Pixel Calibration Factor}=\frac{\text{Object Width (mm)}}{\text{Number of Pixels (pixel)}}$$

<p align="center">
<img src="/image-markdown/algoritmKalibrasiPiksel.png" width=30% align="center">
</p>

## Pengolahan Citra Pengukuran dan Penentuan Titik las
The captured image of the irradiation container will be processed to obtain 2 ROI (Region of Interest), namely the ROI of the lid and the ROI of the tube. The thickness of the irradiation container is measured from the ROI obtained. The measurement is done by calculating the length of each thickness of each degree. The length of the line can be calculated with the equation below.

$$\text{Line Length}=\sqrt{(x_{1}-x_{2})^{2}+(y_{1}-y_{2})^{2}}$$

From the measurement results of each part per degree, then calculate the position of the weld point with the equation below.

$$\text{Point Weld}=\frac{\text{Cap Thickness}+\text{Tube Thickness}}{2}$$

Image processing of irradiation containers is performed with the flowchart below.

<p align="center">
  <img src="/image-markdown/algoritmprogramta.png" width=50% align="center">
</p>

# Result
In the process of separating the irradiation container parts, the program performs circle detection with Hough transform. It takes 3 circles to separate each part of the irradiation capsule so as to produce the ROI of the lid and the ROI of the tube. The result of circle detection can be seen in the figure below.

<p align="center">
  <img src="/image-markdown/7.B2-Circle.jpg" width=30% align="center">
</p>

The segmentation results will affect the measurement results and weld point determination. the following are the segmentation results for the cap and tube.

<p align="center">
  <img src="/image-markdown/8.B2-Cap.jpg" width=30% alt="ROI Tutup"> <img src="/image-markdown/9.B2-Tube.jpg" width=30% alt="ROI Tabung">
</p>

The next step is to measure the thickness of the irradiation container section every degree from edge to edge. The measurement results will then determine the weld point. The results of measuring the thickness of the lid and tube of the irradiation container as well as the weld point were obtained in the form of a graph.

<p align="center">
  <img src="/image-markdown/hasiltutup.png" width=60%>
  <img src="/image-markdown/hasiltabung.png" width=60%>
  <img src="/image-markdown/hasiltitiklas.png" width=60%>
</p>
