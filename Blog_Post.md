<img src=https://parade.com/wp-content/uploads/2021/06/healthy-starbucks-drinks.jpg width="600" height="400"/>

## Should I send my discount offers really to each and every customer?

In the eyes of a marketing department the answer will most likely be yes to pull in more customers. <br>
However if you want to send offers only to customers who wouldn't buy anything without it and not 
to those who buy anyway, then here is an approach to predict whether a customer should get an offer, or not.

As part of my project at [Udacity](https://www.udacity.com/) I am working witha predefined dataset from Starbucks, which 
contains simulated data that mimics customer behavior on the Starbucks rewards mobile app.
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

The dataset 'portfolio.json' contains the 

### Cleaning and Rearranging the datasets

#### transcript.json

The raw dataset is shown in the following image:<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170275047-d5368a67-da99-40d5-abbf-8fd2ea656cc2.png)

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
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170282117-5988abfa-261c-4b8b-b497-5144f55c9e94.png)

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
With the [AdaBoostClassifier](https://scikit-learn.org/0.15/modules/generated/sklearn.ensemble.AdaBoostClassifier.html#sklearn.ensemble.AdaBoostClassifier),which had the best accuracy out of 4 other classifier, 
I am going to which offer should be send to a certain user.
As an example I predicted the offers for a male person who is 50 years old, who earns 112000$ per year and has been a member for 5 years.
As a result I get:<br>
<br>
![grafik](https://user-images.githubusercontent.com/96918132/170725916-9d17b7fd-fbfd-4851-95e3-09bcbd4a579d.png)
<br>


