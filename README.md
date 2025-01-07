# hand-gesture-tracker
Hand Gesture Tracking
 Aaron Zheng
 Daniel Xiao

 Problem Definition:
 The problem is to create a hand gesture tracking system that is able to receive a live feed from a
 webcam and recognize hand gestures in that live feed. The results are useful because the gesture
 classifications can then be used to control systems, or even train ML-based algorithms.
 Method and Implementation:
 Step 1:
 The camera data is captured using the default webcam on the device running the Jupyter
 Notebook. On macOS devices, it utilizes Apple’s Continuity Camera feature which allows for
 your phone to be the webcam for the laptop, simplifying the process of capturing a hand against
 a clean background while being able to monitor results. This was used for the demo video.
 Step 2.
 The camera feed is spliced into individual frames, for each of which steps 3-6 are performed
 using the process_frame function, then converted from BGR to RGB color space and displayed
 for the user using the show_array function. The get_video function performs the above primary
 loop and acts as the program’s main function, and is called by creating a thread.
 Step 3. We use a canny edge detection algorithm incorporating the OpenCV dilation and
 gaussian blur for noise filtering, then the skin color detection algorithm as demonstrated in class
 and lab for the detection of the hand edges. The OpenCV findContours function finds the
 contours in the mask.
 Step 4.
 The convex hull of the skin boundaries defined by the largest contour is found using OpenCV’s
 convexHull algorithm, which is based on the Sklansky algorithm for finding convex hulls.
 Step 5.
 The number of convexity defects (i.e cavities/holes in the outer edges of the convex hull but not
a part of the contour mask representing your hand itself) are counted, and then filtered using
 cosine theorem to ensure the angle of the defect is small enough to conceivably be shaped like
 the spaces between your fingers. This is what is ultimately used to detect the gesture.
 Step 6. The number of convexity defects are counted and the 5 hand gestures recognizable by
 this program are displayed. (Palm, 4 fingers up, 3 fingers up, 2 fingers up, 1 finger up/fist)
 Experiments:
 Wetested the program using me and my project partner’s hands, running the code individually
 on our machines.
 Results
 The result for my testing can be seen in the demo video, where the program exhibits exceptional
 (90%<) accuracy when fingers are evenly spaced out in a natural manner, and the front or back
 of the hand can be entirely and clearly visible in frame with a black background. Certain
 scenarios can cause false positives, as outlined below.
 Confusion Matrix:
 This matrix is generated via a total of 50 trials performed under a variety of conditions including
 different backgrounds and webcams, with 25 trials performed per project partner, 5 per gesture
 per participant and 10 total. .


 Program Strengths:
 Reliable operation and a simple algorithm, with relatively high tolerance for environmental
 factors such as different lighting conditions, skin color and exceptional accuracy for certain
 gestures, given a clean background.
 Program Limitations:
 Lower tolerance for messy backgrounds and high chance of misclassification if skin or near skin
 color objects are present in the frame.
 Since this program counts the number of spaces between your fingers, it cannot distinguish
 between 1 finger up and a fist, as they both have no convexity defects <90 degrees. Furthermore,
 if you close your fingers when showing your palm, the palm may be recognized as a fist. This
 could potentially be solved using a moment of inertia and/or template based tracking algorithm,
 but that includes its own set of possibly stronger limitations, including hand orientation, shape,
 and specific gesture/motion and we were unable to produce satisfactory results when initially
 trying template based tracking.
 This program is also unable to distinguish between different hand gestures involving orientation
 or the use of different fingers. It only recognizes the number of spaces between fingers, and
 gestures that can be recognized via this method.
 Conclusion:
 This skin color + convexity defect based gesture tracking system has solid reliability in certain
 scenarios with a clean, high contrast background, but struggles to work when the background
 isn't clean or the fingers aren’t spaced out

 
 Credits and Bibliography
 Convex Hull algos:
 https://en.m.wikipedia.org/wiki/Convex_hull_algorithms
 Simplest Convex Hull Algo:
 https://en.m.wikipedia.org/wiki/Gift_wrapping_algorithm
Examples where Sklansky algo can fail:
 http://cgm.cs.mcgill.ca/~athens/cs601/Sklansky2.html
 HowContours and Convex Hulls and Defects work:
 Contours and Convex Hull in OpenCV Python | by Dhruv Pandey | Analytics Vidhya | Medium

