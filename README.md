# Module 3 Final Project

## Summary

For the Flatiron Data Science course's Module 3 (formerly Module 2) Project, I analyzed a provided subset of the Northwind Database.

I was assigned one hypothesis to test, and created and tested three others for significance. The four hypotheses and their conclusions are as follows:
1. If a product had a discount, it was ordered in a significantly larger quantity. The size of the discount did not significantly affect how much was ordered.
2. When comparing freight costs during meteorological winter to freight costs during the rest of the year, there was no significant difference.
3. When comparing freight costs for the three different shipping companies, two (#2 and #3) were not significantly different from each other and both were significantly different from the other company (#1). In the dataset, the higher freight costs were with companies #2 and #3.
4. The total amount paid for an order varies very little when the products contained therein are out of stock or discontinued.

The PNG schema of the dataset is as follows:
![Diagram of the Northwind dataset's SQL tables](https://raw.githubusercontent.com/bronwencc/Module-3-Project/master/Northwind_ERD.png)


### Hypothesis 1:

First, I use SQL to get the table OrderDetail, put it into a Pandas dataframe `ordDetdf` and save it in files/OrderDetail.csv.

Null hypothesis: discounted `Quantity` has a lower or the same mean as nodiscount `Quantity`

Alternative hypothesis: discounted `Quantity` has a higher mean than nodiscount `Quantity`

The Discount column (possible values 0, 0.05, 0.1, 0.15, 0.2, 0.25) is converted to dummy columns and added to a new dataframe `disc_df` saved in files/DiscountDummies.csv.

The `Quantity` values are not normally distributed according to a histogram, Seaborn `distplot`, Scipy `kstest`, and statsmodels `qqplot`. To calculate effect size with Cohen's d, it needs to be in a normal distribution. I wrote a resample/bootstrap function to get normally distributed lists of sample means and use `scipy.stats.norm.rvs` to get a random sample of the normal continuous random variable.

I wrote Welch's t test, one-tail t test, and effective degrees of freedom functions to calculate the p-value comparing discounted and non-discounted quantity values, which was 5e-11. This is less than 0.05 so there is a significant difference and therefore the discounted mean for `Quantity` is higher.

Then, I wrote a function `Cohen_d` to figure out the magnitude of the difference between two groups. It found a large effect size between discounted and non-discounted samples.

For the different levels of discount (5, 10, 15, 20, 25), I did pairwise t tests with `stats.ttest_ind` to check for significance. No p-values were less than 0.05 so I concluded there was no significant difference between the possible values for discounts. 


### Hypothesis 2:

Null hypothesis: Freight costs in winter have a mean that is the same or lower as freight costs during the rest of the year.

Alternative hypothesis: The mean freight costs in winter are higher than freight costs during the rest of the year.

Using SQL, I selected certain columns from the Order table, after renaming it to "Orders", and saved that information in a dataframe `ordersdf` and as the Orders.csv file. After looking at the `ShipRegion` column, I added a new column `Hemisphere` to indicate whether the order was shipped in the Northern or Southern Hemisphere. I wrote a function to make this determination based on the `ShippedDate` and `ShipRegion` and mapped it with a list comprehension to create the `Season` column. I used meteorological seasons rather than astronomical; so winter in the Northern Hemisphere was from December 1 to the end of February and in the Southern Hemisphere from June 1 to August 31.

I created a new dataframe `shipdf` with Freight, Season and ShipVia (categorical variable of shipping company) columns and saved the dataframe as Ship.csv. I then split Freight into two lists, one each for winter and the rest of the year. When looking at histograms, most values were under 200. As such, I normalized the two lists of Freight values by takimg the logarithms of all of them.

The values need to be normalized before being compared with Cohen's d.

### Hypothesis 3:

Null hypothesis: The mean cost of freight is not different depending on the three different companies.

Alternative hypothesis: One or two of the three companies' mean freight costs are higher or lower than the other(s).

I used some of the same information I had selected from the database for the previous hypothesis; namely, the Freight and ShipVia columns. The database also contained the names of the companies that corresponded to the numbers in the ShipVia column.

I first compared all three companies' freight costs to each other and found two of the three companies to have little difference between them. I then combined their freight costs into the same list and compared, with an appropriately-scaled histogram, to the other shipping company's freight costs.

### Hypothesis 4:

Null hypothesis:

Alternative hypothesis:


## Repository Contents:

This repository contains the dataset itself, a PNG file of the diagram schema of the tables in the dataset, presentation slides and a Jupyter notebook of the analysis. The notebook uses SQL queries to access the data tables and then Pandas dataframes to test hypotheses. It saves transformed data along the way in CSV files, such as after feature engineering, so they can be accessed to conduct analysis at certain points without starting over completely from the beginning.
* [student.ipynb](https://github.com/bronwencc/Module-3-Project/blob/master/student.ipynb) is the Jupyter notebook containing code that tests four hypotheses
* Northwind_small.sqlite is the dataset provided by Flatiron for this analysis
* [Module2-Final-Project.pdf](https://github.com/bronwencc/Module-3-Project/blob/master/Module2-Final-Project.pdf) contains the slide presentation explaining the project and analysis
* CONTRIBUTING contains information for contributing to The Flatiron School's respositories
* LICENSE contains the licensing information for The Flatiron School's materials

In the ["files" folder](https://github.com/bronwencc/Module-3-Project/tree/master/files), there are seven .CSV files of data that can be read into the Jupyter notebook to review analysis for each hypothesis without starting from the beginning with the Northwind_small.sqlite file.

In the ["graphs" folder](https://github.com/bronwencc/Module-3-Project/tree/master/graphs), there are five .PNG files with charts comparing differences that were tested in hypotheses.
