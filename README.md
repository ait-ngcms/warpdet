CWDET Installation & Use
============================
*The cropping and warping error detection tool*

Installation Guide
------------------

### Requirements

To install you need:

* Python 2.7
* Python libraries cv2, numpy, scipy, matplotlib, math, PIL e.g. install pythonXY
* Git if you download it from the github
* PyCharm editor can support you by project editing and configuration

### Download

| Version | Size   | SHA1                                                    |                      |
|---------|--------|---------------------------------------------------------|----------------------|
| v2.7.3.0| 117 MB |                                                         |[download] https://code.google.com/p/pythonxy/wiki/Downloads  

### Installing CWDET

#### Use the command line or PyCharm to execute Python project.
1. Copy project files in your working directory or check out project sources from github e.g. using TortoiseGit
2. Install necessary Python libraries e.g. pythonXY

Using CWDET
--------------

Execute the main Python script 'warping-demo.py'  

Use laptop camera or another camera to scan documents clicking 'blank' button on your keyboard. Press 'enter' if your collection is completed. 
Follow descriptions on the current page e.g. press 'enter' again to start analysis. In order to escape the program - press 'Esc' button.

For working with existing collection without demo and camera - use warpingDetection.py script. Upload your document collection in the folder 'samples' and uncomment lines having key word 
'warp-debug' in comments. Execute the script warpingDetection.py from the command line. Results are stored in associated subfolder of the folder 'res'.

### Basic Workflows

#### Warping and Cropping Error Detection

The cropping and warping error detection algorithm is summarized as follows:

In order to detect documents with warping and cropping errors we aggregate digital text document speciﬁc data (text block position and dimension) using MSER features and 
expert knowledge about expected text block. In the first workflow step the image is loaded in RGB colour format. In the next step RGB image is converted to the greyscale 
format in order to improve computation performance comparing to colour format. In subsequent steps we analyse the greyscale image and calculate region of interest (text block) 
employing MSER algorithm. Detected letters are marked by the green rectangles. In the third step we filter rectangles by their size (δxi for width and δyi), mean value μ 
(with minimal smin and maximal coefficient smax) and border relation bi considering them for text regions. Additionally, in the fourth step we check that detected letters have 
neighbouring letters and are not single. In further steps we analyse detected letters and calculate corners of a text block and most distant points, marked by red and orange lines accordingly. 
For reasoning on aggregated data, we analyse angles αj between text corners and position of the most distant points (e.g. RU{X,Y} for the right upper corner and 
LMD{X,Y} for the left most distant point are the coordinates of the lowest text region on the left side). The i is a number of green small rectangle elements.

Several constants were required for accurate computation: B stands for the border offset from X and Y axis with respect to the image width W and height H. 
A stands for the acceptable αj threshold. The blue rectangle bounds the text region around the text corners and the hell blue rectangle bounds the text region around the most distant points. 
Subsequently, we employ different parameters like expected border distances and maximal allowed shift angle of the text area on the X and Y axes for the image in order to infer conclusion 
about scan correctness. This supports the human expert to infer an informed evaluation of the scan quality of image candidates that could be mis-cropped or warped and evaluate whether 
these images are in fact affected by the indicated error and to perform necessary actions.  

The presented tool is working on a greyscale representation of the image data and is configured with relative measures. 
The initial configurations should be set by a digital preservation expert who is familiar with the material of a particular institution and the type of document collection.

Command line use
----------------

### Sample usage

	warping-demo.py

### Output of cropping and warping error detection script is a list of documents marked by the red strip if it is an error candidate or by the green strip if it is assumed that
this document is correct. 

## Features and roadmap

### Version 1.0

* Cropping and warping error detection in a digital document collection



