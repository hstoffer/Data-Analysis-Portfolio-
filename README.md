I used a crowdsourced dataset "Housing", prepared by me and other graduate students. We leveraged Zillow data to build the dataset. It was a project intended to work with real, messy data and approach various methods of data cleansing as well as careful modeling using validation techniques to make predictions accurate, all while using R. My objective was to construct an insightful analysis on the Greater Cincinnati Housing Market. 

Ten variables were connected in the dataset: Address, Zip Code, Sold Price, Sold Date, # of Bedrooms, # of Bathrooms, Year Built, sqft, Lot Size (in sqft), and # of Parking Spots. 

My key objective was to extract meaningful insights to help Greater Cincinnati housing buyers make informed decisions on purchasing houses, leveraging the available variables to answer self-constructed key questions:
1. How does location impact housing prices?
2. How does the time of year impact housing prices? (Seasonal affects)
3. How do specific amenities impact housing prices?

Sample Size: 1561 observations *The sample size was originally 1642 observations. The 1561 is after a data-cleansing process.
Independent Variables Used: # of Bedrooms, # of Bathrooms, Year Built, Season Sold, Month Sold
Response Variable: Price Sold
Tools: R

Data Cleansing Process:
1. Removal of Duplicates utilizing R's "dplyr" library

2. Handling Excessive Missing, Irrelevant, Inaccurate and Messy Data:
• Removed Student Contributor Name Variable: Irrelevant to analysis goals
• Removed Address Variable: Can use Zip Code Variable instead
• Removed Number of Parking Spot Variable: Excessive Missing Data
• Removed Lot Size Sqft Variable: Excessive Missing Data
• Zip Code Variable:
• Filtered out date-formatted values
• Number of Bedrooms Variable:
• Convert missing data and alphabetic data to
‘na’; change to numeric datatype
• Remove rows with missing values
• Number of Bathrooms Variable:
• Shorten name to “Number.of.Bathrooms”
• Price Sold Variable:
• Standardized data abbreviated with “M” in Price Sold to unabbreviated number; • Removed non-numeric characters
• Changed the variable to datatype numeric.
• Removed values that were ‘0’
• Removed row with value 7500000 – likely accurate however skews model
• Removed row with value 245 as likely data entry error.
• Removed rows with values <20000 as risk for inaccuracy and skews model
-Removed Lot Size sqft 

3. Data Transformation:
• Transformed Zip Code to County
• Poor distribution of each county’s representation in sample; ultimately removed this variable to avoid overfitting.
• Transformed Date Sold to Season
• Transformed Date Sold to Month

4. Did a Visual Inspection Using Visual PAIRS (in pdf attached) 

Key Questions:
1. HOW DOES LOCATION AFFECT HOUSE PRICES?
To solve for this, I created ‘County’ variable from Zip Code variable using R package zipcodeR.
Checking the County summary data, it was clear there was an unequal distribution in the data among the counties. If used as a factor, this bad distribution creates high risk of overfitting.
Data that could have been significant to answer this question would be determining location based upon school districts, or distance to shopping centers. This data was not available.
I ended up removing the County variable from the dataset and did not pursue this further.

WHAT TIME OF YEAR AFFECTS HOUSE PRICES?
Season Sold variable created and based on Date Sold variable. 
Month Sold variable created and based on Date Sold variable. Distribution okay.
Created 4 experimentation models - Model 1, 2, 3 have too low R-squared. Model 4 has only one category with a p-value < .05. Only one category with significance is not useful.
Unable to answer this question.
(For more details check out the pdf file in this project)

Key Question #2 HOW DO AMENITIES AFFECT HOUSING PRICES?

Created this model: Amenity Model Experimentation #1
model_2a <- lm(Price.Sold ~ Number.of.Bedrooms + Number.of.Bathrooms + Year.Built + Squared.Feet, data = housing)
Adjusted R-Squared: 54.61%
Coefficient & Intercept p-values all < .05 
Number.of.Bedrooms std. error: -24.87% 
Number.of.Bathrooms std. error: 9.44% 
Year.Built std. error: 15.57% 
Squared.Feet std. error: 5.28% 
F-statistic: 469.5
No zero in independent variables confidence intervals.

The pdf attached has screenshots of major visualizations and much more detail on how I came to an unconclusive result. I used residual analysis, Cook's Distance, Log Versions and Polynomial Versions, p-values, R-Squared. 

Eventually the summary was there was the dataset was not strong enough to provide predictions and recommendations on how these variables impact house pricing. While at times there seemed to be a sure significance, the biggest takeaway is to test and validate before presenting any model to organizational leadership. It is a high-stake situation, and integrity in the data and conclusions has to be maintained for leadership to made good decisions utilizing data.
