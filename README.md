# Audio-Deep-Learning-Made-Simple-Sound-Classification
**Audio Deep Learning Made Simple: Sound Classification, Step-by-Step.**
(An end-to-end example and architecture for audio deep learning’s foundational application scenario.)

Sound Classification is one of the most widely used applications in Audio Deep Learning. It involves learning to classify sounds and to predict the category of that sound. This type of problem can be applied to many practical scenarios e.g. classifying music clips to identify the genre of the music, or classifying short utterances by a set of speakers to identify the speaker based on the voice.

In this project, we will walk through a simple demo application so as to understand the approach used to solve such audio classification problems. My goal throughout will be to understand not just how something works but why it works that way.

We will start with sound files, convert them into spectrograms, input them into a CNN plus Linear Classifier model, and produce predictions about the class to which the sound belongs.
![image](https://github.com/user-attachments/assets/6deb9f9e-520a-4c25-a6f0-17d5972b1824)
Audio Classification application

There are many suitable datasets available for sounds of different types. These datasets contain a large number of audio samples, along with a class label for each sample that identifies what type of sound it is, based on the problem you are trying to address.

These class labels can often be obtained from some part of the filename of the audio sample or from the sub-folder name in which the file is located. Alternately the class labels are specified in a separate metadata file, usually in TXT, JSON, or CSV format.

**Example problem — Classifying ordinary city sounds**

For our demo, we will use the Urban Sound 8K dataset that consists of a corpus of ordinary sounds recorded from day-to-day city life. The sounds are taken from 10 classes such as drilling, dogs barking, and sirens. Each sound sample is labeled with the class to which it belongs.

You can download the dataset from this link:

https://urbansounddataset.weebly.com/urbansound8k.html

After downloading the dataset, we see that it consists of two parts:

**Audio files** in the ‘audio’ folder: It has 10 sub-folders named ‘fold1’ through ‘fold10’. Each sub-folder contains a number of ‘.wav’ audio samples eg. ‘fold1/103074–7–1–0.wav’

**Metadata** in the ‘metadata’ folder: It has a file ‘UrbanSound8K.csv’ that contains information about each audio sample in the dataset such as its filename, its class label, the ‘fold’ sub-folder location, and so on. The class label is a numeric Class ID from 0–9 for each of the 10 classes. eg. the number 0 means air conditioner, 1 is a car horn, and so on.

The samples are around 4 seconds in length. Here’s what one sample looks like:

![image](https://github.com/user-attachments/assets/ff77a4a4-5354-4fd5-96ed-781a710dda1f)

Sample Rate, Number of Channels, Bits, and Audio Encoding

The recommendation of the dataset creators is to use the folds for doing 10-fold cross-validation to report metrics and evaluate the performance of your model. However, since our goal in this article is primarily as a demo of an audio deep learning example rather than to obtain the best metrics, we will ignore the folds and treat all the samples simply as one large dataset.

**Prepare training data**
As for most deep learning problems, we will follow these steps:

![image](https://github.com/user-attachments/assets/94019b50-a33c-4440-8562-a053b6b1c59d)

Deep Learning Workflow 

The training data for this problem will be fairly simple:

**The features (X) are the audio file paths
**

**The target labels (y) are the class names
**

Since the dataset has a metadata file that contains this information already, we can use that directly. The metadata contains information about each audio file.

![image](https://github.com/user-attachments/assets/03889fe7-c4bb-43c2-ac5b-61f3836545f9)


Since it is a CSV file, we can use Pandas to read it. We can prepare the feature and label data from the metadata.
