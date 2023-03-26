Mouse Cursor Control Using Eye Movement
This HCI (Human-Computer Interaction) application in Python will allow you to control your mouse cursor with your eye movements, works with just your regular webcam. Its hands-free, no wearable hardware or sensors needed.


Working Example


Code Requirements

Numpy 
OpenCV 
PyAutoGUI 


Execution
Order of Execution is as follows:

Follow these installation guides - Numpy, OpenCV, PyAutoGUI, Dlib, Imutils and install the right versions of the libraries (mentioned above).
Make sure you have the model downloaded. Read the README.txt file inside the model folder for the link.
python mouse-cursor-control.py
Please raise an issue in case of any errors.

Usage
I definitely understand that these facial movements could be a little bit weird to do, especially when you are around people. Being a patient of benign-positional-vertigo, I hate doing some of these actions myself. But I hope to make them easier and less weird over time. Feel free to suggest some public friendly actions that I can incorporate in the project.


How It Works
This project is deeply centered around predicting the facial landmarks of a given face. We can accomplish a lot of things using these landmarks. From detecting eye-blinks [3] in a video to predicting emotions of the subject. The applications, outcomes and possibilities of facial landmarks are immense and intriguing.

Dlib's prebuilt model, which is essentially an implementation of [4], not only does a fast face-detection but also allows us to accurately predict 68 2D facial landmarks. Very handy.


Using these predicted landmarks of the face, we can build appropriate features that will further allow us to detect certain actions, like using the eye-aspect-ratio (more on this below) to detect a blink or a wink, using the mouth-aspect-ratio to detect a yawn etc or maybe even a pout. In this project, these actions are programmed as triggers to control the mouse cursor. PyAutoGUI library was used to control the mouse cursor.

Eye-Aspect-Ratio (EAR)
You will see that Eye-Aspect-Ratio [1] is the simplest and the most elegant feature that takes good advantage of the facial landmarks. EAR helps us in detecting blinks [3] and winks etc.


You can see that the EAR value drops whenever the eye closes. We can train a simple classifier to detect the drop. However, a normal if condition works just fine. Something like this:

if EAR <= SOME_THRESHOLD:
   EYE_STATUS = 'CLOSE'
Mouth-Aspect-Ratio (MAR)
Highly inspired by the EAR feature, I tweaked the formula a little bit to get a metric that can detect open/closed mouth. Unoriginal but it works.


Similar to EAR, MAR value goes up when the mouth opens. Similar intuitions hold true for this metric as well.

Prebuilt Model Details
The model offers two important functions. A detector to detect the face and a predictor to predict the landmarks. The face detector used is made using the classic Histogram of Oriented Gradients (HOG) feature combined with a linear classifier, an image pyramid, and sliding window detection scheme.

The facial landmarks estimator was created by using dlib's implementation of the paper: One Millisecond Face Alignment with an Ensemble of Regression Trees by Vahid Kazemi and Josephine Sullivan, CVPR 2014. And was trained on the iBUG 300-W face landmark dataset: C. Sagonas, E. Antonakos, G, Tzimiropoulos, S. Zafeiriou, M. Pantic. 300 faces In-the-wild challenge: Database and results. Image and Vision Computing (IMAVIS), Special Issue on Facial Landmark Localisation "In-The-Wild". 2016.


You can get the trained model file from http://dlib.net/files, click on shape_predictor_68_face_landmarks.dat.bz2. The model dat file has to be in the model folder.



References
[1]. Tereza Soukupova´ and Jan Cˇ ech. Real-Time Eye Blink Detection using Facial Landmarks. In 21st Computer Vision Winter Workshop, February 2016.

[2]. Adrian Rosebrock. Detect eyes, nose, lips, and jaw with dlib, OpenCV, and Python.

[3]. Adrian Rosebrock. Eye blink detection with OpenCV, Python, and dlib.

[4]. Vahid Kazemi, Josephine Sullivan. One millisecond face alignment with an ensemble of regression trees. In CVPR, 2014.

[5]. S. Zafeiriou, G. Tzimiropoulos, and M. Pantic. The 300 videos in the wild (300-VW) facial landmark tracking in-the-wild challenge. In ICCV Workshop, 2015.

[6]. C. Sagonas, G. Tzimiropoulos, S. Zafeiriou, M. Pantic. 300 Faces in-the-Wild Challenge: The first facial landmark localization Challenge. Proceedings of IEEE Int’l Conf. on Computer Vision (ICCV-W), 300 Faces in-the-Wild Challenge (300-W). Sydney, Australia, December 2013

[7]. Adrian Rosebrock. Imutils. https://github.com/jrosebr1/imutils.

