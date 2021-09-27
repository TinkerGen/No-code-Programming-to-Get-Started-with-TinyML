# Lesson 03 Gestures Recognition by using built-in Light sensor

## Project Overview

This model uses the Wio Terminal to recognize hand gestures: rock, paper and scissors using  built-in Light sensor.

![L03-01.png](/Lesson-03/images/L03-01.png)

It is quite hard to accomplish using rule-based programming because gestures are not performed the same way all the time.  Trying to solve this problem using traditional Programming requires hundred of different rules for each mode of action. Even if we consider an idealized situation, we still miss a lot of motions such as speed, angle, and direction. A slight change in these factors requires a new set of rules to be defined but machine learning can handle these variations very easily.
A well-known possibility is to use camera sensors combined with machine learning to recognize gestures. Using a light sensor is equivalent to using only a one-pixel point of the camera to recognize gestures which is a completely different level of challenge. Let's meet the challenge with this project.

### Expected results

In the figure below, Wio Terminal displays the current results of gesture recognition in real-time. One of rock, scissors, and paper.

![scissors](/Lesson-03/images/L03-02.png) ![rock](/Lesson-03/images/L03-03.png) ![paper](/Lesson-03/images/L03-04.png)

### Material Preparation

Hardware requirements: Wio Terminal
Connection method:

![L03-05.png](/Lesson-03/images/L03-05.png)

## Theory

In this lesson, we are going to train and deploy a simple neural network for classifying rock-paper-scissors gestures with just a **single light sensor.**

![L03-06.png](/Lesson-03/images/L03-06.jpeg)

The working principle of this project is quite trivial. Different gestures being moved above the light sensor will block certain amount of light for certain periods of time. For example, for rock, we will have high values at first (nothing above sensor) but lower values when "rock" passes above the sensor and then high values again. For paper, we will have high-low-high-low-high-low-high-low values when each of the fingers in "paper" passes above the sensor.

- Paper

![Paper](/Lesson-03/images/L03-07-paper.png)

- Rock

![Rock](/Lesson-03/images/L03-08-rock.png)

- Scissors

![Scissors](/Lesson-03/images/L03-09-scissors.png)
​
There is a high variance in speed and amplitude of the values from the sensor which makes a great case for using machine learning model instead of a hand-crafted algorithm for the task.

## Practice

### Project Steps

1. Creating and Selecting Models
1. Data Acquisition
1. Training and Deployment
1. Programming

### Step 1. Create and select models

#### 1.1 Create a "Gesture Recognition (Built-in Light Sensor)" model

Click on "Create and select model", click on " Gesture Recognition (Built-in Light Sensor)", as shown in steps 1 and 2 below.

![L03-10.png](/Lesson-03/images/L03-10.png)

Enter a NAME according to the requirements.

![L03-11.png](/Lesson-03/images/L03-11.png)

Click Ok and it will automatically jump to the Data Acquisition interface.

### Step 2. Acquisition of data

#### 2.1 Default label

![L03-12.png](/Lesson-03/images/L03-12.png)

![L03-13.png](/Lesson-03/images/L03-13.png)

#### 2.2 Connect the device and upload default data acquisition program in Codecraft

When the Wio Terminal is connected, in the Codecraft surface, click![Upload](/Lesson-03/images/L03-14.png) as shown in the figure. This action will upload the default data acquisition program.

![L03-15.png](/Lesson-03/images/L03-15.png)

Usually it takes 10 seconds to upload.  Once the program is uploaded,  "Upload Successful"  window will appear on the screen shown below. This is shown in the image below.

![L03-16.png](/Lesson-03/images/L03-16.png)

Click "Roger" to close the upload success pop-up window above and return to the programming screen.

#### 2.3 Acquisition of data

In the upper right hyperlink, you will find a step-by-step introduction to data acquisition. Follow the instructions to collect data.
![L03-17.png](/Lesson-03/images/L03-17.png)

Attention:

- Wio Terminal button location.
- Animated gif has been accelerated, the actual action can slightly slow down.
- Please notice the red tips.
- Point the curser over Description Texts for more detailed content.

![L03-18.png](/Lesson-03/images/L03-18.png)

![L03-19.png](/Lesson-03/images/L03-19.png)

Wio Terminal will be displayed during the collection process.
Start and end collecting data according to the Wio Terminal screen.

![being collected](/Lesson-03/images/L03-20.png) Indicates the data is being collected
![OK](/Lesson-03/images/L03-21.png) Indicates the Data collection is complete

Now, the data acquisition is finished.

![L03-22.png](/Lesson-03/images/L03-22.png)

Click on "Training & Deployment"

![L03-23.png](/Lesson-03/images/L03-23.png)

### Step 3. Training and deployment

#### 3.1 Set neural network and parameters

Select the suitable neural network size: one of small, medium and large
Set parameters, number of training cycles (positive integer), learning rate (number from 0 to 1) and minimum confidence rating(number from 0 to 1).
The interface provides default parameter values.
In this case we are using MEDIUM. It will take quite a long time.

![L03-24.png](/Lesson-03/images/L03-24.png)

#### 3.2 Start training the model

Click "Start training".

![L03-25.png](/Lesson-03/images/L03-25.png)

When you click "Start training", the interface displays "Loading...".

![L03-26.png](/Lesson-03/images/L03-26.png)
​
The duration of "Loading.." varies depending on the size of the selected neural network (small, medium and large) and the number of training cycles. Larger is the network size and number of training cycles, the longer it takes.

You can also infer the waiting time by observing the "Log". In the figure below, "Epoch: 68/500"  indicates the total number of training rounds is 500 while 68 rounds have been trained.

![L03-27.png](/Lesson-03/images/L03-27.png)

#### 3.3 Observe the model performance to select the ideal model

In the "Model Training Report" window, you can observe training results including the accuracy, loss and performance of the model.
If the training results are not satisfactory, you can go back to the first step of training the model, select another size of the neural network or adjust the parameters and train it until you get a model with satisfactory results.

![L03-28.png](/Lesson-03/images/L03-28.png)

#### 3.4 Deploy the ideal model

In the "Model Training Report"  window, click ![Model deployment](/Lesson-03/images/L03-28-2.png)

![L03-29.png](/Lesson-03/images/L03-29.png)

Once the deployment is completed, Click "Ok" to jump to the Programming window

![L03-30.png](/Lesson-03/images/L03-30.png)

### Step 4. Use and programming

#### 4.1 Write the program for using the model

In the "Programming" interface, click on "Use Model" to use the deployed model.

![L03-31.png](/Lesson-03/images/L03-31.png)

Try to use your model by writing the following programme.

![L03-32.png](/Lesson-03/images/L03-32.png)

#### 4.2 Upload the program to Wio Terminal

Click the "Upload" button.

![L03-33.png](/Lesson-03/images/L03-33.png)

The first upload time is usually long and it increases with the complexity of the model. The upload time for smaller models is about 4 minutes or longer(depending on the performance of your machine).

![L03-34.png](/Lesson-03/images/L03-34.png)

![L03-35.png](/Lesson-03/images/L03-35.png)

#### 4.3 Wio Terminal test model

Make a gesture "scissors" to see whether Wio Terminal's screen show "scissors". Try other gestures, and see whether the Wio Terminal recognizes your gestures.
​

**Congratulations! You have completed your TinyML model, I believe you are familiar with your input(dataset and labels) and know your output. A good score of "Accuracy" leads you to draw a conclusion that your model is working perfectly but it is not enough for you to evaluate the performance of your model. So, let's take a look at the output.**

## ML Theory(understand your output)

### Output (the training performance)

- ACCURACY
- LOSS
- Confusion matrix
- F1 SCORE

![L03-36.png](/Lesson-03/images/L03-36.png)

#### 1. Accuracy

Accuracy is a method of measuring the performance of a classification model. It is typically expressed in percentage value. Accuracy is the count of predictions where the predicted value is **equal to the true value**. It is binary (true/false) for a particular sample. Accuracy is often graphed and monitored during the training phase though the value is often associated with the overall or final model accuracy. Accuracy is easier to interpret as compared to the loss.

Machine learning model accuracy is the measurement used to determine which model is best at identifying relationships and patterns between variables in a dataset based on the input, or training, data.  It is typically expressed in percentage value. Accuracy is the count of predictions where the predicted value is equal to the true value and is simple to calculate. You can check the accuracy of your model by simply dividing the number of correct predictions by the total number of predictions.

#### 2. Loss

A **loss function** determines the probability or uncertainty of a prediction based on how much prediction **varies from the true value**. This gives us a more nuanced view of how well the model is performing.

Unlike accuracy, loss is not a percentage. It is a summation of the errors occurred for each sample in training or validation sets. Loss is often used in the training process to find the "best" parameter values for the model (e.g. weights in a neural network). During the training process, the goal is to minimize this value.

##### Relationship Between Accuracy and Loss

Most of the time we observe that accuracy increases with the decrease in loss but this is not always the case. Accuracy and loss have different definitions and they measure different parameters. They often appear to be inversely proportional but there is no mathematical relationship between these two metrics.

Accuracy and loss appear to be inversely proportional, as we can often observe that accuracy increases with the decrease in loss, but in reality, there is no mathematical relationship between the two. Accuracy and loss have different definitions and they measure different parameters. when the loss decreases the accuracy also decreases.

#### 3 Confusion Matrix

![L03-37.png](/Lesson-03/images/L03-37.png)

![L03-38.png](/Lesson-03/images/L03-38.png)

#### 2.4 F1 SCORE

The F1-score is a measure of a model's accuracy on a dataset.

![L03-39.png](/Lesson-03/images/L03-39.png)

![L03-40.png](/Lesson-03/images/L03-40.png)

## Summarization

1. Theroy:

- Light sensor

2. TinyML practice

![L03-41.png](/Lesson-03/images/L03-41.png)

3. ML theory (Output/the training performance)

- Accuracy: A method of measuring the performance of a model.
- Loss: A loss function, also known as a cost function determines the probability or uncertainty of a prediction based on how much prediction varies from the true value.
- Confusion Matrix: A matrix that lays out the performance of a learning algorithm
- F1 Score: 
![L03-42.png](/Lesson-03/images/L03-42.png)
