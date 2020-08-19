## Implementation for Camera based 2D feature Tracking

### Data Buffer
* A ring data buffer was implemented by simply removing the first element using erase if the buffer size is maximum and then using push back to add the new element at the back of the buffer.

### Keypoint Detection and keypoint removal
* Detectors FAST, BRISK, ORB, AKAZE and SIFT were created using the OpenCV library. A separate function was implemented for HARRIS detector. First edges are detected using cornerHarris() function, then the edges are normalized and converted to an absolute scale. If the keypoints do not overlap the maximum value then the keypoint is added to the detection. 
* The Keypoints were reduced to focus on the specific car in front for better performance of the methods

### Descriptors
* Descriptors BRIEF, ORB, FREAK, AKAZE and SIFT were implemented using the OpenCV library. Optimal input parametes were predefined for BRISK and SIFT descriptors.
* FLANN matching method was implemented using the flann based Descriptor matching class in OpenCV.
* Descriptor distance ratio test was implemented using the KNN matching method. If the distance between source and target keypoints is less than the product of the distance ratio and the distance of the target and source keypoints then the keypoints are added to matches. The distance ratio was set to 0.8.

### Performance
* The number of keypoints, matched keypoints and the time taken for keypoint detection and descriptor extraction on the preceding vehicle for all 10 images were noted.
* Based on the data collected and considering the process time along with number of matched keypoints, the following 3 combinations can be recommended:
1. FAST detector and ORB descriptor
    - FAST detects on an average 1750 keypoints in about 1 
    - Time for descriptor extraction averages 1 sec
    - Matching Keypoints averages to 150 matches
2. FAST detector and BRIEF descriptor
    - FAST detects on an average 1750 keypoints in 1 sec
    - Time for descriptor extraction averages 1.25 secs
    - Matching Keypoints averages to 150 matches
3. ORB detector and BRIEF descriptor
    - ORB detects on an average 500 keypoints in 7 secs
    - Time for descriptor extraction averages 0.85 secs
    - Matching Keypoints averages to 110 matches
4. Shitomasi detector and BRIEF descriptor
    - Shitomasi detects on an average 1300 keypoints in 15 secs
    - Time for descriptor extraction averages 1.25 secs
    - Matching Keypoints averages to 110 matches

The performance evaluation for all the combinations of Detectors and Descriptors can be found in the spreadsheet.