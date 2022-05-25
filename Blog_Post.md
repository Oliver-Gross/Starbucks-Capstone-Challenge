<img src=https://user-images.githubusercontent.com/96918132/150175572-2937f3d3-8ec7-41dd-ba50-8ec1edb71da3.png width="600" height="400"/>

## Should I send my discount offers to every customer?

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
