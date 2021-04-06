# Action Recognition from video

### Abstract

### Problem solved

### Methodology

### Steps

The jetson xavier will be mounted on the dash of the car. The USB cam on the xavier will stream in the video feeds and the pre-trained model will predict if there is a 'pedestrian approaching' or a 'cyclist approaching' in the view of the camera. Note: this is different than just detecting if there is a pedestrian in the frame, while driving on the streets, there will be predestrians in the view, our approach here is to detect when the pedestrain is dangerously close to the vehicle or moving in a way that could potenially mean them intercepting the path of the moving vehicle. It's easy for humans to detect such situations since we have plethora of experiences detecting when a situation may develop with the slightest of the hints. Our attempt is to teach the model detect such situations. 
This model may have applications in self driving cars, however, when trained on other types of actions such as detecting the type of visitors walking in into a gated community and classifiying the objective of the visitor such as 'food delivery', 'guest', 'courier', 'housekeeping', 'residents' etc. helps automatic cataloging of entries that are today mostly manual or not present at all. This also has applications in the areas of retail where we can potentially detect customers picking up items from shelves, returning them to shelves, approaching the billing counter, window shopping, showing interest in products in a particular aisle etc.

In the current scope of the project where we are detecting 'clueless prdestrains' or 'cyclists', we have a few options on how to interact with the environment upon detection:

- Sound an alarm (can be done on the xavier itself, but we would need a buzzer etc.)
- Save the video clip where the action was detected
- Stream the live feed to an App on the phone or a web application and highlight when a potential action is detected


##### Detection from live feed

The frames recieved from the camera are buffered on the Jetson via a sliding window approach. Each frame initiates a new queue that keeps adding frames until a specified number of frames are collected. e.g. if we are going to do inference on a 3 second clip, assuming we are getting 15 fps from the usb cam on the jetson, we will have 45 frames in a queue, which will then be used for inference and then the frames will be discarded. Every second a new queue will be created, which means every 15 frames a new queue is created, at the end of 3 seconds we have 3 queues which the first queue having 45 frames, the 2nd one with 30 frames and the 3rd one with 15 frames. That is the maximum number of frames we will have in memory at a given time. As soon as a queue has 45 frames, we run the prediction and drop the frames.


##### Conecting to the Jetson on board a vehicle

Create a Wifi network on the Jetson. The Jeton will lose connectivity to the internet which is OK since we don't need it to talk to anything but the camera.
A web app running on a mobile device e.g. a phone or may be even a laptop will connect to a web server running on the Jetson over this Wifi network.

