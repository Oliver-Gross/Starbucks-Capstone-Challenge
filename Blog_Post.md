<img src=https://parade.com/wp-content/uploads/2021/06/healthy-starbucks-drinks.jpg width="600" height="400"/>

### Table of Contents

1. [Introduction](#intro)
2. [Project Motivation](#motivation)
3. [Metrics](#metrics)
4. [Exploratory Data Analysis](#eda)
5. [Hyperparamter tuning](#hyper)
6. [Results](#results)
7. [Conclusions/Reflection](#conclusion)
8. [Improvements](#improvements)

## Introduction <a name="intro"></a>
### There can be economy only where there is efficiency <sub>~ Benjamin Disraeli</sub>

Like the quote states, efficiency is mandatory for a company. So for this challenge I want to look into the dataset from Starbucks, which <br>
contains simulated data that mimics customer behavior on the Starbucks rewards mobile app.<br>
Here they send their offers to every user, which also includes user who complete an offer without even seeing it first. <br>
It would be inefficient to send those users offers and therefore I want to design a prediction model which gives out a list of <br>
offers a certain user will most likely complete.<br>

### Introduction of the dataset:
Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). Some users might not receive any offer during certain weeks.

Not all users receive the same offer, and that is the challenge to solve with this data set.
This data set is a simplified version of the real Starbucks app because the underlying simulator only has one product whereas Starbucks actually sells dozens of products. Every offer has a validity period before the offer expires. As an example, a BOGO offer might be valid for only 5 days. You'll see in the data set that informational offers have a validity period even though these ads are merely providing information about a product; for example, if an informational offer has 7 days of validity, you can assume the customer is feeling the influence of the offer for 7 days after receiving the advertisement.

You'll be given transactional data showing user purchases made on the app including the timestamp of purchase and the amount of money spent on a purchase. This transactional data also has a record for each offer that a user receives as well as a record for when a user actually views the offer. There are also records for when a user completes an offer. 
#### portfolio.json

    id (string) - offer id
    offer_type (string) - type of offer ie BOGO, discount, informational
    difficulty (int) - minimum required spend to complete an offer
    reward (int) - reward given for completing an offer
    duration (int) - time for offer to be open, in days
    channels (list of strings)

#### profile.json

    age (int) - age of the customer
    became_member_on (int) - date when customer created an app account
    gender (str) - gender of the customer (note some entries contain 'O' for other rather than M or F)
    id (str) - customer id
    income (float) - customer's income

#### transcript.json

    event (str) - record description (ie transaction, offer received, offer viewed, etc.)
    person (str) - customer id
    time (int) - time in hours since start of test. The data begins at time t=0
    value - (dict of strings) - either an offer id or transaction amount depending on the record


### Metrics <a name="metrics"></a>

To grade the result we will look at the accuracy, precision and the F-score.

### Exploratory Data Analysis <a name="eda"></a>

To get a better understanding of our data sets we will use a few pandas functions.<br>
With the df.head() function we get a impression of the formats.
![grafik](https://user-images.githubusercontent.com/96918132/170886071-d4ced702-f6ea-43bb-8167-7da630e4ff03.png)
<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170886179-1687d3c3-0131-4311-8f43-550d0e0c9c5a.png)
<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170886195-f3a41b32-ff29-4bff-819b-7304a1893ca7.png)
<br>

With df.info() we get the data types of the columns and also a glimpso amount of missing data.
<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170886323-bab57d2f-6582-43fc-a7c6-f45f44a8c309.png)
<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170886334-b293b3e5-585a-4e13-a787-530beef3d455.png)






### Cleaning and Rearranging the datasets

As a first step I am encoding the used id's of the users and the offers.<br>
Next I am creating a binary matrix out of the column 'event' and combine the rows with the same offer id and user id.
The dataset will look like this then: <br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170278168-e6ef1c43-df62-44e3-b0d3-689631b2525f.png)

At this point I will distinguish between relevant and inrelevant user.
A inrelevant user is someone who either doesn't complete an offer or completes it without seeing the offer first. 
In the end the dataset is conctruceted like this:<br>

![grafik](https://user-images.githubusercontent.com/96918132/170278035-e0b25600-070b-4c74-8b9c-f7a9bdfb85d5.png)

#### profile.json

The raw dataset is shown in the following image:<br>

It is noticable that some rows contain no valid data (gender = 'None', age = 118, income = NaN).
So I am dropping them and also encode the user id.
The histogram will look like this:<br>
![grafik](https://user-images.githubusercontent.com/96918132/170283127-a440a755-081e-4488-9d99-c7e3c55cb878.png)

<br>
For the upcoming prediction I have to change all the columns into numeric values. 
I changed 'female' into '1', 'male' into '2' and 'other' into '3'.
The column 'Became_Member_On' with the datetime-format has been changed into 'Member_for_x_years' with a float-format.
The dataset will then be combined with the transcript dataset and look like this:<br>

![grafik](https://user-images.githubusercontent.com/96918132/170284379-f36ae1a2-a24c-4ac4-9f0d-6f9d31207301.png)
<br>

I am going to which offer should be send to a certain user.
As an example I predicted the offers for a male person who is 50 years old, who earns 112000$ per year and has been a member for 5 years.
As a result I get:<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170725916-9d17b7fd-fbfd-4851-95e3-09bcbd4a579d.png)
<br>


