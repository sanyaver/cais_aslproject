Sanya Verma <br />
sanyaver@usc.edu <br />
In one or two sentences, present your project to us! <br />
<br />
=> I used the ASL Dataset to train the Computer Vision Multiclass Classification model on the 29 different types of characters available: A-Z, DELETE, NOTHING and SPACE. This would do the work of translating and communicating for deaf or mute people. <br />
<br />
**Dataset:** Indicate the dataset you chose to use, any preprocessing steps that were applied, as well as the reasoning behind these choices. <br />
<br />
=> I used the ASL Dataset from kaggle (https://www.kaggle.com/datasets/grassknoted/asl-alphabet) with 29 test jpegs and 87000 training jpegs sorted into 29 different classes <br />
=> ImageDataGenerator is a preprocessing class which helps us augment our training example images by randomly transforming them and making it such that the same image is never repeated. This helps prevent overfitting and the model can generalize better. It allows us to configure random transformations and operations on image data during training. <br />
=> Tf.keras.applications.mobilenet.preprocess_input is the preprocessing function which scales input pixels between -1 and 1 which standardizes the input. It is also necessary to have image pixels between -1 and 1 for the MobileNet model we will use.<br />
Other parameters are validation_split=0.2 - 20% of images are used for validation. horizontal_flip = True which randomly flips it horizontally, brightness_range=(0.75, 1.3): which shifts the brightness level and zoom_range=0.2 which zooms into the image by 20%. The images are all also resized to 224 x 224 pixels. <br />
=> So we first created dataframes, preprocessed training images and then split them into training and validation into an 80-20 split. <br />
<br />
**Model Development and Training:** Discuss your model implementation choices, the training procedure, the conditions you settled on (e.g., hyperparameters), and discuss why these are a good set for your task. <br />
<br />
=> The MobileNet model being used is pre-trained on the ImageNet dataset which has 1.4M images and over a 1000 classes. It uses the feature extractor portion of the pre-trained model and has a bottleneck layer which retains features best. It doesn’t update the weights, just like Approach #1 in Lecture_4 of Curriculum. <br />
=> It has a Top-1 or conventional accuracy of about 70% and a Top-5 accuracy of about 90% generally. Also it didn’t take as much time as some other models I tried like ResNet50. <br />
=> The relu activation function used is quite fast as well and doesn’t have the vanishing gradient problem very often. We then use the softmax activation function on the output because it’s better for multiclass classification compared to the Sigmoid function. <br />
=> In compilation, the Adam optimizer is used which is computationally efficient, has little memory requirement, and is well suited for problems that are large in terms of data/parameters. The binary cross-entropy loss is very useful for multi-class classification. It doesn’t penalize less confident correct guesses as hard as a hinge loss function for example. <br />
=> There are only 2 epochs as there are so many training images and I was trying to be more efficient with time <br />
<br />
**Model Evaluation/Results:** Present the metrics you chose and your model evaluation results. <br />
=> 3989s 4s/step - loss: 0.1042 - accuracy: 0.9667 - val_loss: 0.0668 - val_accuracy: 0.9783 <br />
![alt text](https://github.com/sanyaver/cais_aslproject/blob/main/download.png?raw=true)

=> These are all standard metrics to use as I was prioritizing accuracy. I got an accuracy of 96.67% with a validation accuracy of 97.83%. <br />
<br />
**Discussion:** <br />
How well does your dataset, model architecture, training procedures, and chosen metrics fit the task at hand? <br />
=> It does a pretty good job overall as it was able to pretty accurately predict the right character for most images. It was also not too slow, which was a priority of mine for efficiency and to ensure the model worked before I can finetune it further. <br />
Can your efforts be extended to wider implications, or contribute to social good? Are there any limitations in your methods that should be considered before doing so? <br />
=> Absolutely, it is invaluable for not only the hard of hearing/mute community but also for the people around them to be able to communicate with them better. It’s not 100% accurate so far so there would certainly be mistranslations. Another limitation is that ASL is a very complex language and this only helps with letter reading, but not words or sentence structures. <br />
If you were to continue this project, what would be your next steps? <br />
=> I would like to focus on being able to real-time translate videos as well as on figuring out how to translate more complex ASL words/phrases. There hasn’t been a lot of work in NLP for ASL as it is quite different from other traditionally spoken or written languages so it could be interesting to combine this with an NLP project <br />
<br />
=> used: https://www.kaggle.com/code/raanaramadan/asl-training + https://www.tensorflow.org/tutorials/images/transfer_learning + https://www.kaggle.com/code/aminesnoussi/american-sign-language-recognition




