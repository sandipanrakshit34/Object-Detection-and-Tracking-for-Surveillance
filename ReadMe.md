# CCTV Surveillance for Traffic Dense Environment -- Object Detection and Tracking Using YOLOV3

<h2>Introduction :</h2>

Deep learning has gained a tremendous influence on how the world is adapting to Artificial Intelligence since past few years. Some of the popular object detection algorithms are Region-based Convolutional Neural Networks (RCNN), Faster-RCNN, Single Shot Detector (SSD) and You Only Look Once (YOLO). Amongst these, Faster-RCNN and SSD have better accuracy, while YOLO performs better when speed is given preference over accuracy. Deep learning combines SSD and Mobile Nets to perform efficient implementation of detection and tracking. This algorithm performs efficient object detection while not compromising on the performance.

<h2>Our Vision and Mission :</h2>

* Creating a Custom Data-set of desired classes and labeling the Images.
* Detecting moving objects of specified classes in a Traffic heavy Environment using Deep learning.
* Track down the detected Objects using Deep Learning based algorithm Deep-SORT.
* Implementing our solution for any specific surveillance related problems to those detected and tracked Objects.

E.g: 
    1. Velocity Estimation of a Vehicle, 
    2. Distance between Two or more Tracked Down Objects  etc.                                                         

<h2>Dataset Creation and Labeling :</h2>

* We used images from Google’s OpenImagesV6 dataset, publicly available online. It is a very big dataset with more than 600 different categories of an object. The dataset contains the bounding box, segmentation, or relationship annotations for these objects.

* We collected images of 8 classes.  **“Person”**, **“Motorbike”**, **“Traffic light”**, **“Car”**, **“Bus”**, **“Truck”**, **“Bicycle”** and **“Umbrella”**.

* We used LebelImg to label each and every Image for collecting dimensions of anchor boxes.


<h2>Object Detection :</h2>

* Object Detection is a common Computer Vision problem which deals with identifying and locating object of in the image.(Object Recognition recognise what kind of object they are : class labels)

* Interpreting the object localisation can be done in various ways, including creating a bounding box around the object or marking every pixel in the image which contains the object (called segmentation).
* With the need of real time object detection, many one-step object detection architectures have been proposed, like YOLO, YOLOv2, YOLOv3, SSD, RetinaNet etc. which try to combine the detection and classification step.
* In our project we will use YOLOv3 for training our object detection model.

**YOLO v3 :**

You only look once (YOLO) is an object detection system targeted for real-time processing.YOLO is able to perform object detection and recognition at the same time.It is a detector applying a single neural network which -

                                     * Predict bounding boxes
                                     * Multilabel classification
                                   
Grid cell:

* YOLO divides the input image into an S×S grid. Each grid cell predicts only one object. 
* For example, the yellow grid cell below tries to predict the “person” object whose center (the blue dot) falls inside the grid cell.Each grid cell predicts a fixed number of boundary boxes. In this example,the yellow grid cell makes two boundary box predictions(blue boxes) to locate where the person is.

 
</p>
<h3> Bounding Boxes </h3>
<br>
<p align="center">
<img src = "https://github.com/Arupsau/CCTV-surveillance-for-traffic-dense-environments/blob/main/Images/YOLO.jpg">
</p>

**Benefits of YOLO :**

* Fast. Good for real-time processing.
* Predictions (object locations and classes) are made from one single network. Can be trained end-to-end to improve accuracy.
* YOLO is more generalized. It outperforms other methods when generalizing from natural images to other domains like artwork.
* Region proposal methods limit the classifier to the specific region.YOLO accesses to the whole image in predicting boundaries. With the additional context, YOLO demonstrates fewer false positives in background areas.
* YOLO detects one object per grid cell. It enforces spatial diversity in making predictions.

**Custom YOLO v3 object detection model :**

<h5>Configuring files for training YOLOV3 custom model:</h5>

1. We edit the yolov3.cfg to fit our needs based on our object detector by updating

* batch = 64,
* subdivisions = 16,
* max_batches = 16000,
* classes= 8
* filters = 39  // filters = (classes + 5) * 3

2. In obj.data we set

 * Classes=8
 
3. In obj.names we edit names of our 8 required classes:

“Person”, “Motorbike”, “Traffic light”, “Car”, “Bus”, “Truck”, “Bicycle” and “Umbrella”.

<h3>Training YOLO v3 custom model :</h3>

* To train our model we take the help of Google Colaboratory which is an amazing tool that lets us build and execute an outstanding data science model and provides us with an opportunity to document our journey.
* First, we take help of Darknet framework and download pre-trained weights for the convolutional layers.

* We store our last trained weights in backup folder for future reference and continue training from that checkpoint.

<h3>Testing YOLO v3 custom model :</h3>

First, we need to make some updates to our yolov3_testing.cfg file
* Batch = 1
* Subdivision=1
Now, we can test our Custom Object Detector by running command on a sample photo file:
</p>
<h3> Object Detection Output </h3>
<br>
<p align="center">
<img src = "https://github.com/Arupsau/CCTV-surveillance-for-traffic-dense-environments/blob/main/Images/Detection_Output.jpg">
</p>
<br>


<h2>Object Tracking :</h2>

It is the process of locating moving objects over time in videos.
It involves-
* Taking an initial set of object detection
* Creating unique ID for each of the detection
* Tracking the object over time
* Maintaining the ID assignment

**Difference between Object Detection and Tracking :**

* Object detection is simply about identifying and locating all known objects in a scene.
       Object tracking is about locking onto a particular moving object(s) in real-time.
* Object detection can occur on still photos while object tracking needs video feed.
       Object detection can be used as object tracking if we run object detection every
       frame per second.                                                                                          
* Running object detection as tracking can be computationally expensive and it can only track known objects.
Thus object detection requires a form of classification and localization.

**DeepSORT :**

The most popular and one of the most widely used, elegant object tracking framework is Deep SORT, an extension to SORT (Simple Real time Tracker).
Improves the matching procedures and reduces  the number of identity switches by adding visual appearance descriptor or appearance features.
It obtains higher accuracy with the use of

            1) Motion measurement
            2) Appearance features
            
It  applies Kalman Filtering, Hungarian method, Mean shift,Optical Flow,Feature Vector

<h3>Converting YOLO v3 weights to tensorflow Model :</h3>

* We will use our previously trained YOLOV3 weight for tracking objects.So we need to copy our trained yolov3_custom.weight to weight folder and also copy obj.names file to labels folder
* To apply this weight to Deep Sort first we need to convert the yolov3_custom.weight to Tensorflow model to work with Deep Sort.
* For this purpose we write a script load_weights.py and we  convert weights to yolov3_custom.tf format.

Now using the tensorflow model and with the help of Deep Sort we are able to track the objects which are previously detected by YOLOV3.



</p>
<h3> Object Tracking Output </h3>
<br>
<p align="center">
<img src = "https://github.com/Arupsau/CCTV-surveillance-for-traffic-dense-environments/blob/main/Images/Tracking.jpg">
</p>

<h2>Application of Object Detection and Tracking :</h2>

* Video surveillance
* Pedestrian detection
* Anomaly detection
* People Counting
* Self driving cars
* Face detection
* Security
* Manufacturing Industry

<h2>Challenges :</h2>

* Speed for real-time detection
* Limited data
* Class imbalance
* Illumination
* Multiple spatial scales and aspect ratios
* Positioning
* Rotation
* Dual priorities: object classification and localization
* Occlusion
* Mirroring

<h2>Future Work :</h2>
We will further try to improve this project by adding extra feature like -

1. Counting number of vehicle or person entered in a particular frame
2. We can use Density Map
3. In or Out of a Specific Zone



