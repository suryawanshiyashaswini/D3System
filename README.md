# D3System 
Driver's Drowsiness Detection System
With an average number of 1.4 Billion vehicles hitting the road worldwide, the saturation rate has been increased by
around 18 percent per year globally. With this number of vehicles, a normal man commuted for at least 15 to 20km per day
worldwide. Also, due to the increased use of roadways in Business like Logistics transport, the commute distance may increase to
thousands of KMs per day increasing the traffic level on highways worldwide. With all these aspects in mind, there is a huge
chance that Drivers in the city/country must drove over time and over distance. Resulting in spreads of Drowsiness among the
drivers. To overcome this situation and to avoid any Human casualty in the future, I have tried to set up a small mechanism to
alert the driver and their respected loved ones whenever any driver goes drowsy while driving.
Driver Drowsiness system (D3S) is a mechanism that reads the facial expression of an individual sitting in the driver's seat and
detects whether a driver is sleeping or about to sleep. On the determination of his/her expression, the system generates a loud
alarm which makes the driver awake and avoids any mishaps on road.
Keywords: Face Detection, Eye Detection, Blink Detection, Yawn Detection, Flask.

A. Face Detection
Have used an approach namely the Viola-Jones algorithm for object detection that minimizes computation time whereas achieving
high detection accuracy. The approach was used to construct a face detection system that is approximately fifteen times quicker than
any previous approach.
Face detection mainly follows below stages:
1) Haar Features: Viola-Jones algorithmic rule uses a 24x24 window as the base window size to start evaluating these features in
any given image. If we consider all features into mind then there will be 160,000+ features in this window.
2) Integral Image: In integral image ,Rectangle features are computed very rapidly using an intermediate representation.
3) Ada Boost: As stated previously there can be approximately 160,000+ feature values within a detector at 24x24 base resolution
which needs to be calculated. But it is to be understood that only a few sets of features will be useful among all these features to
identify a face. Ada-boost is a machine learning algorithm that helps in finding only the best features among all these 160,00+
features. After finding features, a weighted combination of all these features is used in evaluating and deciding that any given
window has a face or not.
4) Cascade: The basic principle of the Viola-Jones face detection algorithm is to scan the detector many times through the same
image –each time with a new size. Even if an image should contain one or more faces, it is obvious that an excessively large
amount of the evaluated sub-windows would still be negatives (non-faces). So, the algorithm should concentrate on discarding
non-faces quickly and spend more time on probable face regions. Hence a single strong classifier formed out of the linear
combination of all best features is not good to evaluate on each window because of computation cost.Therefore, a cascade
classifier is used which is composed of stages.Where the job of each stage is used to determine whether a given sub-window is
not a face or maybe a face. A given sub-window is immediately discarded as not a face if it fails in any of the stages.
![image](https://user-images.githubusercontent.com/67435373/123995210-b7da2180-d9eb-11eb-8b70-c7dac58ba53a.png)


B. Eye & Lips Region Extraction
Once the face is detected, now comes the task to detect the facial landmarks in the face using the dlib’s landmark predictor. The
landmark predictor returns 68 (x, y) coordinates representing different regions of the face, namely - mouth, left eyebrow, right
eyebrow, right eye, left eye, nose, and jaw. For sure, I do not need all the landmarks, here I need to extract only the eye and the
mouth region landmarks.
Steps
1) Load shape predictor
2) Map facial landmarks

![facial-landmark](https://user-images.githubusercontent.com/67435373/123995503-0982ac00-d9ec-11eb-82bb-b917f8fd4780.jpg)

C. Eye-Blink & Yawn Detection
After extracting mouth and eye coordinates from facial landmark the next task is to detect blink and yawn and this is done with the
help of EAR(Eye Aspect Ratio) and MAR(Mouth Aspect Ratio).The eye region is marked by 6 coordinates. These coordinates can
be used to find whether the eye is open or closed if the value of EAR is checked with a certain threshold value.
E.g.
EAR = (A + B) / (2.0 * C)
EAR < = 0.2 ,Blink is detected
In the same way, MAR is calculated to detect if a person is yawning. Although, there is no specific metric for calculating this, so
have taken for points, 2 each from the upper and lower lip and calculated the mean distance between them as:
MAR = (A + B + C) / 3.0
MAR>14,Yawn is detected.
D. Alarm Generation
Once the EAR and MAR ratios detected above and below their threshold ,the alarms are blown.

This system determines the state of the driver in Day as well as Night conditions at runtime using an IR camera with an experimental result of 84% accuracy. Face and Eyes detection are implemented based on facial landmark and dlib.


