# Serendeepia_DAICWOZ
Intership
# Depression analisys and diagnosis.
This project is property of Sereendepia Research (http://serendeepia.com/) and supervised by its team
of experts Jorge Muñoz (CEO), Javier Ordoñez (CIO) and Raul Arrabales (CBDO) who helped me to
develop this project as a Minimum Viable Product. I was able to work with this team of experts during
an internship in this company, as part of my Master's degree in Artificial intelligence in the International
University of La Rioja (UNIR).

## 1. Description of depression

Depression is a serious mood disorder. It causes severe symptoms that affect how you feel, think, and
handle daily activities, such as sleeping, eating, or working. Depression comes from the Latin word
“depressare”, meaning essentially the feeling of heaviness, in a general way it can be described as a
lowering of mood or spirits [1][2]. There are several forms of depression, each one is slightly different
and can be develop under unique circumstances, such as:

• Persistent depressive disorder

• Postpartum depression

• Psychotic depression

• Seasonal affective disorder

• Bipolar disorder

To measure the depression that a person can be suffering there is a scale we can apply and measure the
severity of the depressive disorder. The eight-item Patient Health Questionnaire depression scale (PHQ-
8) [3] is established as a valid diagnostic and severity measure for depressive disorders in large clinical
studies. Current depression is defined by either the DSM-IV based diagnostic algorithm (i.e., major
depressive or other depressive disorder) of the PHQ-8 or a PHQ-8 score ≥ 10 [3].

## 2. Aim of the project and database

The aim of this project is to detect depression traits analysing the voice of the subject, and ultimately
building a virtual robot that can detect this disorder and raised an alarm, that could be used for
example, to warn a healthcare agent.

In order to do this, I needed a database to extract the human voice and start analysing it. The DAIC-WOZ
(Gratch et al.,2014) is a good database to accomplish this task. It contains clinical interviews designed to
support the diagnosis of psychological distress conditions such as anxiety, depression, and posttraumatic
stress disorder. It includes 189 sessions of interactions between the animated virtual
interviewer called Ellie, controlled by a human, and the person interviewed.

## 3. Database analisys
The database contains 189 sessions of different people. The database also gives several data about each
participant like de ID, the PHQ-8 score in binary labels, the PHQ-8 score, gender…

There are several files for each participant, the most important ones for this project are:

• Audio file: this is the audio of the interview, most of them have low noise levels during the time
the interviewed person is speaking. These raw files are .wav and the representation of this files
is shown in the flowing picture (example):

![sin titulo](https://user-images.githubusercontent.com/43761341/51127981-1bc1fd00-1827-11e9-989f-1dbfb890b6cf.png)

Transcript file: this file provides the written interview of each participant, and the important
feature in this file is that it contains the timestamp in ms (start and finish) of each sentence said
by the interviewer and interviewed, for example:

                                        165.854 166.324 Ellie yeah3 (yeah)

## 4. Database processing

Before taking the .wav files into the AI system, a segmentation is needed because the raw .wav files
contains the interviewer audio and the interviewed. With this database there are 2 ways we can face
the problem of speaker diarization. The first one is by using an already trained system available in open
source code sites like GitHub. The second one is using the transcript for each participant. The transcript
states the timestamps of each participation of the person being interviewed, if we use this, we can
easily segment the .wav and create a new .wav that only contains the voice of the person. By doing this
we obtain .wav of various lengths, the smaller one being only 52 seconds of audio and the largest one being several minutes long.

We discovered that there is little data to feed into the predictive system. That’s why we create a kind of
data augmentation, where we define a sliding window that we move along the new segmented files.
This way we can create several samples for each participant. The picture below shows the concept of
this task.

![sin titulo - copia](https://user-images.githubusercontent.com/43761341/51127982-1bc1fd00-1827-11e9-99af-43538c09b694.png)

In this case we create 10 samples for each participant.

When we are finish with these tasks, we can start processing the samples. The most important change
to the raw data is the spectrogram which shows information about the sound in the frecuency domain,
showing the power for each frequency. We take each sample and apply a function extracted from the
librosa shelf (GitHub) to calculate the spectrogram. While the representation of the raw audio in the
time domain is not consider very attractive to use it in the AI system, the representation of the same
audio in the frequency domain could be used for the purpose we are looking for.

The spectrogram of 1 created sample is shown below.

![sin titulo3](https://user-images.githubusercontent.com/43761341/51127985-1c5a9380-1827-11e9-86fe-2183a7573c04.png)

The picture shown contains the amplitude of the human voice for that specific participant for each
frequency, as it can be seen in the left Y Axis (Hertz) and right Y Axis that states the energy (defined in
dBFs, in this case the scale is normalized between 0 and -1). From this spectrogram we can see the range
of the human voice, from 0 to 3400 Hz approximately.

We take the non-important data from this spectrogram, which is the frequencies above ~4096 Hz which
doesn’t give any information and with this task, we are finish with the database processing.

For the last step before defining the deep neural model we reshape the data. We will need to feed the
input data into a convolutional neural network and a recurrent neural network (specifically a LSTM
network. This kind of models have been selected because they have been proven to be useful in audio
learning and training.

## 5. Model definition

We define up to 2 different models to accomplish our project based on deep neural networks, an
convolutional neural network and a LSTM network.

The convolutional network is defined with Keras and Conv2D to sweep and learn the spectrogram
image.

![sin titulo - copia 2](https://user-images.githubusercontent.com/43761341/51127983-1c5a9380-1827-11e9-8d28-1a11a604bb68.png)

The LSTM network is defined with Keras and consists of 2 layers of Bidirectional LSTM net.

![sin titulo - copia 3](https://user-images.githubusercontent.com/43761341/51127984-1c5a9380-1827-11e9-8ec6-fa2f7ff7aaa8.png)

The total number of classes that the system is going to predict is 2, 0 for non-depressed and 1 for
depressed. The DAIC-WOZ database provides a Binary PHQ-8 score, which states that everything above
or equal to 10 is considered depressed so is defined as 1, and anything below will be 0.

For the training set we take 107 session and for the validation set we take 35. To balance the people
tagged as depressed and non-depressed we have reduced the session for training (remember that we
have the data augmentation for this problem) to 60 sessions, 30 depressed people and 30 nondepressed
people.

## 6. Training and validation

We train the system using 10 epochs. At the time of writing this summary of the project, I have
encountered a problem. The system gives a 64.57% of accuracy when the system is validated but the
system is not learning, so it predicts the same class for every validation sample. This can be checked by
showing the confusion matrix that has the prediction and the real validation data.

The next steps are evaluating why the system is not learning properly and fix the problems to obtain a
good predictive system that can set an alarm in case of the detection of the depression in a person.

## 7. Conclussion and future work

The future work will be about finishing the project and develop new ways to detect depression. My goal
is to create a correct model that can predict the depression traits using the voice.
8. References

[1] The Nature of Clinical Depression: Symptoms, Syndromes, and Behavior Analysis, Jonathan W
Kanter, Andrew M Busch, Cristal E Weeks, and Sara J Landes

[2] Simpson J, Weiner E, editors. Oxford English dictionary. Cary, NC: Oxford University Press; 1989.

[3] The PHQ-8 as a measure of current depression in the general population, KurtKroenkea, Tara
W.Strineb, Robert L.Spitzerc, Janet B.W.Williamsc, Joyce T.Berryd, Ali H.Mokdadb























