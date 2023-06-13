# mldrones
Machine learning for drones about energy consumption
Data Collected with Package Delivery Quadcopter Drone

For this work, Data Collected with Package Delivery Quadcopter Drone database is used. Data are collected from Carnegie Mellon University and Amazon and describe drone flights from 2019-04-07 to 2019-10-24. It also consists of different variables:

A. Name: flight

       Description: an integer that represents the code of the flight performed. A flight is defined as the data set recorded from the take-off to landing in a predefined route.

B. Name: time

Description: Time elapsed in flight in seconds (s).

C. Name: wind_speed

Description: airspeed provided by the anemometer in meters per second (m/s).

D. Name: wind_angle

Description: angle in degrees (deg) of the air flowing through the anemometer with respect to the north.

E. Name: battery_voltage

Description: system voltage in Volts (V) measured immediately after the battery.

F. Name: battery_current

Description: system current in Ampere (A) measured immediately after the battery.

G. Name: position_x

Description: longitude of the aircraft in degrees (deg).

H. Name: position_y

Description: latitude of the aircraft in degrees (deg).

I. Name: position_z

Description: altitude of the aircraft in meters (m) with respect to the sea-level.

J. Name: orientation_x; _y; _z; _w

Description: aircraft orientation in quaternions.

K. Name: velocity_x; _y; _z

Description: velocity components of ground speed in meters per second (m/s).

L. Name: angular_x; _y; _z

Description: angular volocity components in radians per second (rad/s).

M. Name: linear_acceleration_x; _y; _z

Description: ground acceleration in meters per squared second (m/s^2).

N. Name: speed

Description: programmed horizontal ground speed during cruise in meters per second (m/s).

O. Name: payload

Description: mass of the payload attached to aircraft in grams (g). The payload used was confined in a standard USPS Small Flat Rate Box.

P. Name: altitude

Description: predefined altitude in meters (m). The aircraft takes off vertically until it reaches the preset altitude.

Q. Name: date

Description: when the flight was conducted in the YYYY-MM-DD format

R. Name: local_time

Description: local time when the flight started in the 24:00-hour format.

S. Name: route

Description: A predefined path followed by the aircraft. Routes R1 to R7 indicate flights where the drone completed a cruise movement. The differences among routes R1 to R7 reflect variations on the starting point or variations on the altitude during cruise. The differences among routes can be assessed by plotting variables position_x, position_y and position_z. Routes A refer to ancillary ground tests where the drone remained on the ground and did not take off. Route A1 refers to a test with the drone running with no propellers and no motor movement; Route A2 to a test with the drone running with no propellers and minimum motor movement; and Route A3 to a test with the drone running with propellers and minimum motor movement. Route H refers to a test with the drone hovering with no horizonal movement. In summary:

	R1 to R7 = full flights completing a cruise movement.

	A1 = Ancillary ground test with no propellers and no motor movement.

	A2 = Ancillary ground test with no propellers and minimum movement.

	A3 = Ancillary ground test with propellers and minimum movement.

	H = Hover test with no horizontal movement.

The dataset consists of Number of 257,896 rows. And There is no missing data. For this approach we decided to use Python to help us in our results.

Descriptive statistics

First to help measure the results we changed the values of S. Name: route column, the values from R1 to R7 change it from 1 to 7, A1 to 8, A2 to 9, A3 to 10 and H to 11.

In the table below we have a boxplot for Battery voltage and as we can most of our values are between 22 and 23.

We then create a new column called “power” by multiplying battery current and battery voltage.

Following we have correlations of our data. We try to find which variable correlates more with energy. As we can see the first one is with position z with 0.50 then wind speed follows with 048 and the third one is velocity y with 0.34.

We then try to make comparison of the three most correlated variables on a monthly basis.

RESULTS

First, we use all the independent variables using SVM with rbf kernel and minmax scaler to make some predictions. We split the data into training (80%) and testing (20%) set and here are the results.

Predicting on the training data Model accuracy: 0.8778 Mean squared error: 0.0067. Predicting on the test data

Model accuracy: 0.8771 Mean squared error: 0.0068.

After that we tested SVM with linear kernel, the results were even better. Model accuracy for training: 0.9513 Mean squared error: 0.0027 and Predicting on the test data Model accuracy: 0. 9512 Mean squared error: 0.0027. As we mentioned earlier the three that correlate most with power is position_z, wind_speed and velocity_y so let’s use only those three and energy for our analysis. Predicting on the training data Model accuracy: 0.5960 Mean squared error: 0.0220 Predicting on the test data.

Model accuracy: 0.5913 Mean squared error: 0.022.

We will now test our data using Standard Scaler. Our results are almost perfect. Predicting on the training data Model accuracy: 0.9982 Mean squared error: 0.0018 Predicting on the test data Model accuracy: 0.9974 Mean squared error: 0.0026.

As we can see the original data and our predictions are close.

After that we tried RobustScaler

Predicting on the training data

Model accuracy: -0.0498 Mean squared error: 0.38966

Predicting on the test data

Model accuracy: -0.051688 Mean squared error: 0.393435

As we can see from the results RobustScaler is not suitable for with our data.

We will now use the Linear with min max Scaler model to make predictions.

The results are perfect. Predicting on the training data

Model accuracy: 1.0 Mean squared error:

2.9844925651351705e-31 Predicting on the test data

Model accuracy: 1.0 Mean squared error:

2.976794988611205e-31

So linear model is the right algorithm for this dataset.

Last, we use Random Forest Regressor to see if it matches the linear model.

training data: Model accuracy: 0.999999 Mean squared error: 5.7811599.

test data: Model accuracy: 0.999999 0 Mean squared error: 9.721559.
