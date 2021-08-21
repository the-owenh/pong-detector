This is (partial) program for a research project with Northwestern University's Prof. Wing Kam Liu. It was originally intended 
to track a ping pong ball and determine its spin. However, it can be easily modified to identify any object (it just takes a 
some extra steps). We first use a convolutional neural network to track a ball, then a physics based approach to determine the 
rotation vector of the ball. 

To use the code to track your own (singular) object in a video, follow the procedure (exactly) below. We assume basic knowledge of neural networks. 

A. Obtaining Data

1. Once you have decided on what object you want to track, take a multiple videos of it (we used 1080p @ 60fps for about 20-30 seconds total)*
2. Take a separate video as your validation dataset. 

* For a more robust CNN, try to take pics/videos with varying backgrounds, sizes, clarity. 


B. Prepare your data for training

1. ensure that your anaconda environment has openCV version >= 3.4.2, matplotlib, cvxpy. Open jupyter notebook.
2. download all files from the repo and place into a folder named "objTrack".
3. create a new folder inside the folder above named "images".
4. move the video you want to analyze to "objTrack".
5. open vidToImgs.ipynb and write the name of your video file on line 4. run the program. 
6. ensure that the video frames are inside the images file you created in step 3. 
7. open www.makesense.ai on your browser. select "Get Started". 
8. upload all images from image file. press "Object Detection". Aim to have over 1000 pictures for an accurate model. 
9. make a label for whatever object you'd like to track. 
10. start drawing bounding boxes for each video frame. make sure you select your label on the right-hand side. after about 3 pictures, 
    it will autoselect. 
11. click "Actions" > "Export Annotations" > "Single CSV File" > "Export". Place the .csv file in objTrack
12. open csv_to_yolotxt and insert the name of your .csv file at the bottom. run the program. 
13. check the "images" file and make sure it is populated now with both image files and .txt files. 
14. send the "images" file to a zip folder. 

C. Training your model

1. open google drive and create a new folder named "yolov3"
2. import images.zip to the folder. 
3. start a new Google Colab project, and open Train_YoloV3.ipynb. You may do this outside of the yolov3 folder. 
4. Click Runtime > Change Runtime Type > Hardware Accelerator > GPU > Save. Run the first block to ensure the GPU is enabled. 
5. Run the second block of code and follow instructions to link your Google Drive. 
6. Go to Runtime > Run All 
7. The training has begun. Scroll to the bottom to see it in progress. The longer you allow the model to train the better (Google Colab maxes out at 
   12 hours. Leave it until then if you can).
8. Go back to the yolov3 folder on google drive. There should be file named yolov3_training_last.weights. Download it to objTrack. 


D. Running the neural network 

1. create an empty file named "val" in objTrack
2. move your validation video to objTrack
2. run vidToImgs.ipynb again, but with the validation video. Follow the comments to make sure the frames are stored in another file. 
3. open yolo_TT_final.ipynb and run all code except for the final block
4. open the image console and admire the beauty of machine learning
