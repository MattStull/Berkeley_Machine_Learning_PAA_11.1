# Berkeley_Machine_Learning_PAA_11.1

Jupyter Notebook Link

https://github.com/MattStull/Berkeley_Machine_Learning_PAA_11.1/blob/main/prompt_II.ipynb

Business Understanding

For the project of determining what drives the used price of a call, interviews with sales teams and management teams is necessary.  The following are questions that should drive the process of understanding the data.

The goal of this project is to identify the major factors that contribute to the changes in used car sales prices and provide recommendations as to which vehicles to target to help drive the profitability of the used cars sales business.

1.  How have gas prices and unemployment rates affected used car prices?
2.  Do interest rates / or payment amounts affect prices?
3.  Demographics / credit scores affect purchase prices?
4.  Which vehicles typically have the highest margins to seek ways to maximize profitability.
5.  Can the VIN numbers be searched in a 3rd party database to bring back vehicle specific information to improve forecasting.
6.  Which vehicles have the highest repairs and maintenance that could be used to create future revenue opportunities for the service department.
7.  Unemployment data and past due rates on vehicle types could also be used to predict excess supply that could affect prices.

Data Understanding and Preparation

A review of the data found a lot of cleaning needed to be done to be able to effectively analyze used car prices.  Here is a list of items that were found and performed:

1.  The data table contained numerous duplicate VIN numbers.  In addition, number duplicates to vehicles that had null VIN numbers were removed.
2.  After researching VIN numbers, after 1981, the worldwide standard is 17 digits.  From the VIN number, important features can be derived.  These features were added to the dataframe.  See this link for info: https://en.wikipedia.org/wiki/Vehicle_identification_number.
3.  Model names appeared to be freeform and too difficult to clean into categorical features that wouldn't result in a high number of features after running one-hot-encoder.  As a result, used the model from the VIN number.
4.  Excluded vehicles that were older than 25 years as they were antique vehicles.
5.  Converted sales prices to a lognormal distribution and filtered out outliers so data wasn't skewed.
6.  Excluded vehicles that had mileages over 250,000 miles as many were freightliners and wouldn't fit the typical used car category.
7.  Excluded vehicles with missing titles, were for parts or had a condition of new as these were not typical "used car" sales types.

Modeling

Ran PCA and used 14 principal components.  Used onehotencoder, PolynomialFeatures and TargetTransformer using Ridge() regression.

Evaluation

There were a lot of duplicate values that had to be removed to improve the quality of the data.  VIN numbers were missing for a
lot of vehicles.  If I just look at a list of cars that had 17 digit VIN numbers, the R2 of the model was 59%.  If I only look at vehicles that have VIN numbers and no missing values in the condition column and assign -1 to missing values in the other features, R2 goes up to 75%.  The test data showed similar results with an R2 of 72%.  

To make this model even more accurate, the VIN detailed data needs to be connected to a 3rd party API to improve accuracy of data scraped and to provide more granularity on trim levels.  In addition, that information could be used to populate the values the source of this data came from and there appeared to be freeform responses in many columns (model especially).

Results

When looking at the principle component loadings, the data shows that vehicle values are positively influenced by the following characteristics:

1.  Newer
2.  Low miles
3.  Front wheel drive
4.  Sedans
5.  Japanese made - Toyota and Honda
6.  Excellent condition
7.  Made by GM, specifically Chevrolet brands.

Note:  A very useful metric would be the dealership incorporating gross margins in with this data to determine the most
profitable vehicle model to sell.
