<h1 align="center">Speech Emotion Recognition </h1>
<p align="center"> <img width="200px" heigth="600px" src="imagens/divertidamente_logo.png">
</p>

## Links

- Google Colab Notebook - [Reconhecimento de Emoções na Voz.ipynb]([GOOGLE_COLAB]_Speech_Emotion_Recognition_Project.ipynb)

## Data Source: emoUERJ

The emoUERJ database was developed at the State University of Rio de Janeiro (UERJ) with the primary goal of creating Speech Emotion Recognition (SER) models in Portuguese, as there are few databases in this language. In emoUERJ, you can find:

- 377 audio files (total size: 105.1 MB)
- The database contains 8 actors, equally divided between genders

Ten phrases were provided, and actors had the freedom to choose the phrases for audio recording.

Target emotions and total audios:

- Happiness: 91
- Anger: 94
- Sadness: 100
- Neutral: 92

Below are the 10 phrases used in this dataset:

- Não importa quem está certo. (It doesn't matter who is right.)
- Você perde tempo demais com a Internet. (You spend too much time on the Internet.)
- A garrafa está na geladeira. (The bottle is in the refrigerator.)
- Eu estou me sentindo doente hoje. (I am feeling sick today.)
- Eu estou um pouco atrasado. (I am a little late.)
- Nos fins de semana, eu sempre ia para a casa dele(a). (On weekends, I would always go to his/her house.)
- De quem são essas malas que estão debaixo da mesa? (Whose bags are these under the table?)
- Ele volta na quarta-feira. (He comes back on Wednesday.)
- Já chega! Eu vou tomar um banho e ir para a cama. (Enough! I am going to take a shower and go to bed.)
- Você poderia arrumar a mesa, por favor? (Could you set the table, please?)

Each database file corresponds to a phrase recorded by an actor expressing one of the four emotions and was named as follows:

- Position 1: gender of the actor ('m' for male or 'w' for female)
- Positions 2 and 3: actor's ID (from 01 to 04)
- Position 4: emotion (h: happiness, a: anger, s: sadness, n: neutral)
- Positions 5 and 6: recording identification
- 
For example, the file 'w04a11' was the eleventh audio recorded by actress 04 expressing the emotion of anger.

Source: https://zenodo.org/record/5427549#.ZDI6jnbMLrf

## Visualizing the Distribution

Observing the quantity of files for each class, it is evident that we have a reasonably balanced dataset.
<p align="center"> <img width="800px" heigth="500px" src="imagens/bar_plot.png">
 
## MFCC Spectrograms (Mel-Frequency Cepstral Coefficients)

Spectrograms are a fundamental part of our application because through them, we can observe the audio in three domains:

- Time
- Frequency
- Amplitude
  
<p align="center"> <img width="800px" heigth="500px" src="imagens/MFCC.png">
 
The spectrogram is nothing more than a set of features extracted from the audio, and through these features, we can visualize the above graph.

When considering Machine Learning applications focused on audio, the mel scale is very relevant as it mimics the unique characteristics perceptible to the human ear. For example, it is much easier for us to identify the difference between 100Hz-200Hz than 10,100Hz-10,200Hz.

Now that we understand what a spectrogram is and what the mel scale does, we can conclude that spectrograms are nothing more than images. Therefore, we can train a convolutional neural network to learn to classify different types of sounds based on the differences in MFCC spectrograms.

## STFT spectrograms (Short Time Fourier Transform)

<p align="center"> <img width="800px" heigth="500px" src="imagens/STFT.png">
 
 ## Model: Convolutional Neural Network (CNN)

The spectrograms extracted from the audio files resemble 2D images, allowing us to employ image classification techniques on them specifically, Convolutional Neural Networks (CNN).

The architecture of this neural network was defined based on several tests conducted to achieve the desired outcome. The structure can be freely adjusted and compared to the results of this particular configuration.

 * Parameters:
  * `Sequential`, This is the class used to create the neural network since a neural network is essentially a sequence of layers (input layer, hidden layers, output layer);  
  * `kernel_size`, The size of the convolutional kernel (matrix);
  * `activation`, Activation function;
  * `input_shape`, In the first layer, this represents the size of the input data;
  * `MaxPooling1D` layer, This layer extracts the main features;
  * `Conv1d` layer, A convolutional neural network layer that performs convolution along only one dimension;
  * `Flatten` layer, This layer transforms the matrix into a vector;
  * `Dense` layer, This layer connects one neuron from a layer to all other neurons in other layers;
  * `Dropout`, A regularization technique to reduce overfitting;
  * `padding='same'`, This indicates that a new column composed of only 0s (zeros) is added, using the entire image;
 
 ## Confusion Matrix
 
 <p align="center"> <img width="600px" heigth="300px" src="imagens/confusion_matrix.png">
  
Upon observing the confusion matrix, we can draw the following conclusions:
- 16 phrases were correctly classified in the Happiness class.
- 15 phrases were correctly classified in the Neutral class.
- 17 phrases were correctly classified in the Anger class.
- 18 phrases were correctly classified in the Sadness class.
- 1 phrase that should have been classified in the Happiness class but was classified in the Anger class.
- 1 phrase that should have been classified in the Neutral class but was classified in the Happiness class.
- 1 phrase that should have been classified in the Neutral class but was classified in the Sadness class.
- 4 phrases that should have been classified in the Anger class but were classified in the Happiness class.
- 1 phrase that should have been classified in the Anger class but was classified in the Neutral class.
- 2 phrases that should have been classified in the Sadness class but were classified in the Neutral class.
  
 ## Classification Report
  
 We can observe that the model performed well and achieved an accuracy of 87%.
  
 <p align="center"> <img width="600px" heigth="300px" src="imagens/classification_report.png">
 
Visualizing the accuracy rate for each of the classes, we can observe that:

- A recall of 94% for the Happiness class indicates that the model can correctly classify 94% of the phrases in the Happiness class, and when this happens, it has a precision of 76%.
- An 88% recall for the Neutral class indicates that the model can correctly classify 88% of the phrases in the Neutral class, and when this happens, it has an 83% precision.
- A 77% recall for the Anger class indicates that the model can correctly classify 77% of the phrases in the Anger class, and when this happens, it has a 94% precision.
- A 90% recall for the Sadness class indicates that the model can correctly classify 90% of the phrases in the Sadness class, and when this happens, it has a 95% precision.
  
 ## Next Steps
- Creation of an API with Flask that utilizes the model.
 
