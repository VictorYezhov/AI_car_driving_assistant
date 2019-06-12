# AI_car_driving_assistant
Course work for AI course at UCU. Car driving assistant


First approach: classical computer vision with OpenCV.

For line detection, we used OpenCV’s HoughLines line detector. As an input, it received original image that was processed by Canny edge detector. 
![Image: canny edge detection](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/img/edges.png)
(Image: canny edge detection)

This approach performed well, but it was slow in real time.

We tried to optimize it, by cropping every frame of the video and selecting a region of interest (ROI). This has sped up detection(an increase in around 5 fps), however, accuracy was lost, because of the static region, and non-static video (for example when a car turns, lines on the video could leave ROI, and line detector fails to detect lines because the image is cropped).

![Image: interest area ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/img/info_field.png)
(Example image: only the yellow area will have image info. The rest is empty)

For car detection, we used HOG – histogram of oriented gradients. A trained model performed well, but again, it was too slow to work in real time.

![Image: HOG](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/img/hog.png)

Second approach: Neural networks 

Now for line detection, we use a trained model. But before prediction, we determine a square of interest. We divide frame on half horizontally and our square of interest is down part of the frame. 
Then we make a prediction with a neural network. Add lane prediction to list for averaging. Only using the last five for average. Then we calculate average detection. Generate fake R & B color dimensions, stack with G.
Resize to match the original image and return green square which we will superimpose onto the original image (frame).

![Image: GREEN ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/img/green_area.png)

Example of that green square




For object detection we used YOLO. YOLO stands for “You Only Look Once”.

The algorithm applies a neural network to an entire image. The network divides the image into an S x S grid and comes up with bounding boxes, which are boxes drawn around images and predicted probabilities for each of these regions.

The method used to come up with these probabilities is logistic regression. The bounding boxes are weighted by the associated probabilities. For class prediction, independent logistic classifiers are used.

![Image: YOLO ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/img/YOLO.png)

Network architechture

![Image: YOLO ARCH ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/img/YOLO_ARCHITECHTURE.png)


Results:
![Image: YOLO ARCH ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/result_img/first.png)

![Image: YOLO ARCH ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/result_img/second.png)

![Image: YOLO ARCH ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/result_img/3.png)

![Image: YOLO ARCH ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/result_img/4.png)

![Image: YOLO ARCH ](https://github.com/VictorYezhov/AI_car_driving_assistant/blob/master/result_img/5.png)

In a repository you could find full video
