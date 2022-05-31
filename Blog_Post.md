<img src=https://parade.com/wp-content/uploads/2021/06/healthy-starbucks-drinks.jpg width="600" height="400"/>

### Table of Contents

1. [Introduction](#intro)
2. [Project Motivation](#motivation)
3. [Metrics](#metrics)
4. [Exploratory Data Analysis](#eda)
5. [Cleaning and Rearranging](#clean)
6. [Hyperparamter tuning](#hyper)
7. [Results](#results)
8. [Conclusions/Reflection](#conclusion)
9. [Improvements](#improvements)

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
![grafik](https://user-images.githubusercontent.com/96918132/170886384-588fc6fa-9b7f-4c49-9266-f6cd31c1789a.png)
<br>
It shows us that 'transcript' has no missing data and that there is an equal amount of missing data in profile['age'] and profile['income'].
If we take a close look with: <br>
![grafik](https://user-images.githubusercontent.com/96918132/171104934-f8410492-8671-4cfc-9a7b-96a16b8791d5.png)
<br>
we will see that all rows with missing data look the same and therefore we can drop it.
The distribution of those two columns now looks like this:<br>
![grafik](https://user-images.githubusercontent.com/96918132/171105105-d72f6b75-b2ed-44c3-ad72-77d542922285.png)
<br>

### Cleaning and Rearranging <a name="clean"></a>

For the prediction model we have to clean and rearrange the datasets. <br>
As a first step I am encoding the id's of the users and the offers using a function provided by <br>
the Udacity-team.<br>
![grafik](https://user-images.githubusercontent.com/96918132/171105772-969ad628-b228-4f7c-ba7d-ddd58352b033.png)
<br>
Next I am creating a binary matrix out of transcript['event'] and combine the rows with the same offer id and user id.
The dataset will look like this then: <br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170278168-e6ef1c43-df62-44e3-b0d3-689631b2525f.png)

At this point I will add the column 'Relevant_Offer' to distinguish between relevant and inrelevant user.
A inrelevant user is someone who either doesn't complete an offer or completes it without seeing the offer first. 
In the end the dataset is conctruceted like this:<br>

![grafik](https://user-images.githubusercontent.com/96918132/170278035-e0b25600-070b-4c74-8b9c-f7a9bdfb85d5.png)


<br>
For the upcoming prediction we also have to change all the columns into numeric values. 
I changed 'female' into '1', 'male' into '2' and 'other' into '3'.
The column 'Became_Member_On' with the datetime-format has been changed into 'Member_for_x_years' with a float-format.
The dataset will then be combined with the transcript dataset and look like this:<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170284379-f36ae1a2-a24c-4ac4-9f0d-6f9d31207301.png)
<br>

With this we can also take a look at the ditribution of the offers.<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/171128709-c0dd7d90-475b-45f7-936a-39c1743b6b92.png)
<br>

Something I didn't notice before is the failing-rate of Offer 3 and 8. <br>
Those two offers are of the type informational ann therefore can't be completed. So we will drop them. <br>
Offer 1,2,5 and 10 are more likely to be not completed.<br>

### Hyperparameter tuning <a name="hyper"></a>
