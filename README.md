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





























