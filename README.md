# Final Project

Kasidech Tantipanichaphan, ktantipa@ucsd.edu

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/Cover.png" width="50%">

## Abstract

Nowadays, police sketches are nevertheless a routine part of law enforcement investigations. In other words, visualization plays an important role important towards the criminal investigation. Because the picture of the criminal is not available, this requires us to draw a brief sketch. Clearly, this is not enough for the officers to speculate. Notice that sometimes we cannot clearly visualize the image of the criminal by the sketch that the sketch-artist has drawn. According to the Physical Security statistics, some researchers suggest that facial sketches or composite pictures of suspected criminals are useful less than 20% of the time. Other studies put the percentage even lower – maybe as low as 8%. That means that at least 80% of the time, the time and effort spent creating and circulating these pictures are worthless.

The goal of this project is to gather what we’ve explored in the context of this class and to help formulate a more efficient way in producing a facial composite of the criminal. There are two methods that I decided to use. The first method is using the CycleGAN to produce a better face composition of the criminal from the police sketches. Maybe the criminal face could not be thoroughly visualized. The CycleGAN will select a new loss function to generate more sharp and realistic images. Another element is to produce text to face the result. The idea is to use StackGAN and ProGAN to synthesize faces of the criminal based on the textual description from the victim. The reason why is because sometimes it takes time to sketch the faces of the criminal based on the victim’s description. By using machines to generate the face could be an efficient way of doing so. The presentation on Wednesday will be present in the form of powerpoint.

## Project Report

The Project Report is in this github.

## Model/Data

There are three main datasets that I used for the first part of the project: FERET dataset, CUHK dataset, and MUCT Face database. According to the website, FERET database is a dataset used for facial recognition system evaluation as part of the Face Recognition Technology (FERET) program. The database contains a total of ~14,125 images pertaining to 1199 individuals along with 365 duplicate sets of images that were taken on a different day. The FERET dataset is needed to be requested from the National Institute of Standards and Technology (.gov) website. Similarly, the MUCT Face database also contains lots of people's faces, with the exception that it contains color images instead of gray-scale. Another dataset that I use is called CUHK Face Sketch dataset. Basically, this dataset is for research on face sketch synthesis. This includes 1194 persons, with different lighting variation and a sketch with shape exaggeration drawn by an artist. The second part of the project I use Face2Text dataset (however this project is performing a reverse) which contains 400 facial images and textual captions for each of them. 

## Code

The codes are in this Github.

## Results

#### Sketch-to-face results (Method 1)
Translating police face sketch into actual face of the criminal as much as possible.

Example using Feret Dataset

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/sketch2face.png" width="60%">

Example using MUCT Face Database

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/sketch2face_1.png" width="50%">

#### Text-to-face results (Method 2)
Synthesize the face of the criminal based on the textual description from the victims.

*Example from UCSD Timely Report Crime Email*

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/text2face_1.png" width="100%">

Input strings:

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/text2face_2.png" width="90%">

Generated result:

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/text2face_5.png" width="75%">

*More Generated Examples*

I include the relevant informations such as their race, age, gender, hairstyles, and some of them I also include the emotion as well. And below are my generated outputs based on the input strings. 

<img src="https://github.com/ucsd-ml-arts/ml-art-final-kasidech-t-1/blob/master/Images/text2face.png" width="90%">


## Technical Notes

There are two parts for my project, sketch-to-face and text-to-face. There are three techniques that I decided to use: StackGAN, ProGAN, and CycleGAN. In this implementation, I use the CycleGAN model to generate the results. After we got the FERET and CUHK dataset. It is time to use cycleGAN to train these images. The trainA is the sketches images from CUHK dataset and the trainB is the actual face images from FERET dataset. Adding more images, the data becomes more and more accurate (roughly about 1000+). During the experiment, I adjusted several parameters as well as the number of epochs. The epochs that are greater 100 achieve more satisfying results. The cycle took about 2-3 hours to achieve the best result.

The second part of the project, I use StackGAN and ProGAN to synthesize faces from textual descriptions. This process took 3-4 hours to train the model. This process requires PyTorch framework. For this part of the project, I installed *PyTorch version 0.4.0*. What I did was that I generated the StackGAN which sketches the primitive shape and colors of the object based on the given textual description. The textual description is encoded into a summary vector using an LSTM network. Along with StackGAN, I also use ProGAN. To explain the concept of ProGAN, it has two networks, which are generator and discriminator. The generator creates “fakes”, and the discriminator attempts to distinguish these “fake” samples from the “real” ones. Both networks start out performing quite poorly at their tasks, but when training goes well, they improve in tandem until the generator is producing convincing fakes. This was used to both kind of speed the training up as well as stabilize it. 


## Reference


[1] CycleGAN: https://junyanz.github.io/CycleGAN/

[2] StackGAN: https://github.com/hanzhanggit/StackGAN

[3] ProGAN: https://github.com/akanimax/pro_gan_pytorch

