# Module 3 Final Project

For the Flatiron Data Science course's Module 3 (formerly Module 2) Project, I analyzed a provided subset of the Northwind Database.

This repository contains the dataset itself, a PNG file of the diagram schema of the tables in the dataset, presentation slides and a Jupyter notebook of the analysis. The notebook uses SQL queries to access the data tables and then Pandas dataframes to test hypotheses. It saves transformed data along the way in CSV files, such as after feature engineering, so they can be accessed to conduct analysis at certain points without starting over completely from the beginning.

I was assigned one hypothesis to test, and created and tested three others for significance. The four hypotheses and their conclusions are as follows:
1. If a product had a discount, it was ordered in a significantly larger quantity. The size of the discount did not significantly affect how much was ordered.
2. When comparing freight costs during meteorological winter to freight costs during the rest of the year, there was no significant difference.
3. When comparing freight costs for the three different shipping companies, two (#2 and #3) were not significantly different from each other and both were significantly different from the other company (#1). In the dataset, the higher freight costs were with companies #2 and #3.
4. The total amount paid for an order is varies very little when the products contained therein are out of stock or discontinued.

The PNG schema of the dataset is as follows:
![Diagram of the Northwind dataset's SQL tables](https://raw.githubusercontent.com/bronwencc/Module-3-Project/master/Northwind_ERD.png)

In the main part of the repository:

* [student.ipynb](https://github.com/bronwencc/Module-3-Project/blob/master/student.ipynb) is the Jupyter notebook containing code that tests four hypotheses
* Northwind_small.sqlite is the dataset provided by Flatiron for this analysis
* [Module2-Final-Project.pdf](https://github.com/bronwencc/Module-3-Project/blob/master/Module2-Final-Project.pdf) contains the slide presentation explaining the project and analysis
* CONTRIBUTING contains information for contributing to The Flatiron School's respositories
* LICENSE contains the licensing information for The Flatiron School's materials

In the "files" folder, there are seven .CSV files of data that can be read into the Jupyter notebook to review analysis for each hypothesis without starting from the beginning with the Northwind_small.sqlite file.

In the "graphs" folder, there are five .PNG files with charts comparing differences that were tested in hypotheses.
