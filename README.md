#  Audio Classification

PROJECT LINK:
https://colab.research.google.com/drive/1gfNWs3u3BsvTVfdM1z7jLP1J5AhzBBn_?usp=sharing

# Abstract

Our project utilizes a dataset of 7000 audio files of 4 voice actors saying sentences in one of five emotions: neutral, angry, sleepy, amused, and disgusted. Our goal was to explore neural networks, clustering algorithms, and supervised learning methods in order to  determine which models can be used to predict the sentiment of the audio file. Our use of LSTMs and RNNs resulted in very inaccurate results as did our clustering approaches. On the other hand, the supervised learning methods such as kNN and Decision tree performed with consistently moderate results ranging from about 60 - 80% accuracy after hypertuning with grid search. In addition, our work with CNNs produced results with a fairly high classification accuracy for the amount of data that we provided.

# Introduction / Motivation

Our project idea has 2 primary goals. First is a more theoretical one - understand the problem space of audio classification, tools used, and techniques the tools rely upon to effectively classify audio. This would involve some research, comparison, and study. Second is a more practical goal - using the best practices and tools to successfully perform the audio classification and use our theoretical understanding to help us experiment with the techniques to get best results. 

We chose the EmoV-DB dataset that had ~7000 audio files consisting of clips of 4 voice actors, 2 male and 2 female, with an American accent. Each voice actor said the same few sentences in 5 different emotions: angry, disgusted, amused, neutral, and sleepy. This dataset doesn’t seem to have published results with our specified approach, seems quite obscure, and has no tangible resources that are directly related to it (e.g. Kaggle notebooks). We wanted to work with a dataset that would come with challenges and unknown setbacks as opposed to using a popular dataset that has been worked with substantially more. 

# Experimental Setup

For each of our ~7000 audio files we extracted global features, sequential features, and an image representation of the audio wave. The global features included metrics such as Energy, Tempo, Zero Crossing Rate, and MFFC (average). Essentially, these features were numbers that summarized the audio file as a whole. These global values were used for all of our supervised learning methods (KNN and Decision Tree Classifier) and Clustering (PCA, tSNE, k-Means Clustering). These global values resulted in having 23 features representing each audio file. 

Here’s a brief description of the features used:
   - Energy: Total magnitude of the signal aka how loud the signal is
   - Tempo: The rate at which the signal changes from positive to negative or back
   - Zero Crossing Rate: Speed of the audio file’s contents in Beats Per Minute (BPM)
   - MFFC (Average): The Mel-frequency cepstral coefficient represents phonemes (distinct units of sound) as the shape of the vocal tract (which is responsible for sound generation) is manifest in them. (20 numbers)

The sequential features extracted values such as the spectral centroid, spectral rolloff, and spectral bandwidth were values that were collected for each of the 567 time frames in each audio file. Along with these numbers, we collected 20 MFCC values for each of the 567 time frames in the audio file. As this data represented the audio file in terms of sequences this data would be most appropriate for our RNNs. We had a total of 23 features for each of the 567 time windows which resulted in a total of 11,340 features per audio file.

Here’s a brief description of the features used:
- Spectral Centroid: Indicates where the ”center of mass” for a sound is located and is calculated as the weighted mean of the frequencies present in the sound
- Spectral Rolloff: Variance from the spectral centroid
- Spectral Bandwidth: The measure of the shape of a signal
- MFCC: Represent phonemes (distinct units of sound) as the shape of the vocal tract (which is responsible for sound generation) is manifest in them.

We also transformed our audio files into a 1000 x 380 pixel image representing the spectrogram of the wave. We then used this data for a CNN that could classify emotion based on the spectrogram of the wave.
