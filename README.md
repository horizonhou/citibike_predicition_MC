# Predict Citi Bike Availability Using Markov Chains

In this project, we used the stochastic model Markov Chains to predict the availability for Citi Bike of stations Broadway & W 25 St, Central Park S & 6 Ave, and Broadway & E 21 St in New York City.

### Method 1
#### Preprocessing 
In order to ensure adequate data, we first chose the three stations with the most bikes being ridden away as the object of our analysis, which are Broadway & W 25 St, Central Park S & 6 Ave, and Broadway & E 21 St. We defined daytime as 7am to 3pm and nighttime as 3pm to 11pm, keeping only the data from these two time periods and splitting them into two groups. In addition, we stripped out the weekend data, leaving only the weekday data (21 days in total).

#### Transition Matrix

We adopt the 10 minutes discrete time block, implying 48 time blocks for each daytime and nighttime data. Based on each time block, for example, the time block from 07:00 to 07:10, calculate its net flow by subtracting the bicycle flow in from the bicycle flow out. (Where flow in is the number of bikes that have an end time in this time period and flow out is the number of bikes that have a start time in this time period). Then put all the net flows into a list and compute the probability of each net flow. Build 2d net flow metrics for all time periods. For instance, if there are 19 docks at the station, a 20x20  matrix is generated with row and columns representing the number of cars from 0 to 19. Then fill the probability of net flow in, say the probability of -2 (net flow out) is 0.25, then the probability of the number of bicycles available at the station swift from 19 to 17, 18 to 16, and so on, are 0.25. Then, sum up this row and divide each element in the row by this sum to ensure that the probability transition always adds up to 1.  We get 6 transition matrices in total.
#### New method:
We attempted to use a new approach to estimate the transition matrix. We tried to model the transition probability matrix for each time interval, and then do matrix multiplication to all of these matrices to get the transition probabilities from each start of the morning/evening to end of the morning/evening. However, this method does not work well because our data set is not large enough to support such small segmentation of time.

