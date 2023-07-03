# import the necessary libraries
import numpy as np
import pandas as pd

# for visuals
import seaborn as sns
import matplotlib.pyplot as plt
import squarify

uc = pd.read_csv(r'Unicorn_Companies.csv')
uc

# Data Inspection and Manipulation

uc.rename(columns = {'Select Investors':'Select_Investors'}, inplace = True)

# view the shape of the data
uc.shape

# view info about the data
uc.info()

uc.columns

# view the summary statistics of the dataset
uc.describe()

# checking for missing values
uc.isnull().sum()

uc[uc.City.isnull()]

# How many uniqe Company dont have no City
len(uc[uc.City.isnull()].Company.unique())

# What Companies have with no Cities and how many records are affected?
uc[uc.City.isnull()].Company.value_counts()

# Checking the number of records that will be affected

print('Total number of records: ', uc.shape[0])
print('Number of records with missing City: ', uc[uc.City.isnull()].shape[0])
print('Number of records without missing City: ', uc[uc.City.notna()].shape[0])

# Number of rows with descriptions
num_missing = uc[uc.City.isnull()].shape[0]

# number of rows in all the dataset
num_all = uc.shape[0]

# percentage of rows with missing description
round((num_missing / num_all) * 100, 2)

# Records that are not NaN: notna()
uc = uc[uc.City.notna()]
uc

# What are the rows with NaN values
uc.isnull().sum()

uc.dtypes

uc[uc.Select_Investors.isnull()]

len(uc[uc.Select_Investors.isnull()].Company.unique())

uc[uc.Select_Investors.isnull()].Company.value_counts()

print('Total number of records: ', uc.shape[0])
print('Number of records with missing City: ', uc[uc.Select_Investors.isnull()].shape[0])
print('Number of records without missing City: ', uc[uc.Select_Investors.notna()].shape[0])

num_missing = uc[uc.Select_Investors.isnull()].shape[0]
num_all = uc.shape[0]
round((num_missing / num_all) * 100, 2)

uc = uc[uc.Select_Investors.notna()]
uc

uc.columns

uc.isnull().sum()

# Visualizing missing values 
plt.figure(figsize = (10, 5))
plt.title('Visualizing missing values')
sns.heatmap(uc.isnull(), cbar = True, cmap = 'magma_r')
plt.show()

# Total types of industires

Tyes_Indus = uc['Industry'].value_counts().sort_values()
Tyes_Indus

Tyes_Indus = Tyes_Indus.plot(kind = 'barh', figsize = (10, 5), title = 'Total types of Industires', xlabel = 'Nos_Industires', 
                       ylabel = 'Industires', legend = False)
Tyes_Indus.bar_label(Tyes_Indus.containers[0], label_type = 'edge')
Tyes_Indus.margins(y = 0.1)
plt.show()

# Observation.

- Fron the graph above, Fintech has the highest count of companies in the industry with 218 companies   and  artificial intelligence with least count of companies in the industry with 11 companies in the industry


# Top 5 Countries for investors funding

Top5_Contries = uc['Country'].value_counts().sort_values().tail(5)
Top5_Contries

Top5_Contries = Top5_Contries.plot(kind = 'bar', figsize = (8, 4), title = 'Top 5 Countries for investors funding', xlabel = 'Country', 
                       ylabel = 'Nos of Fundings', legend = False)
Top5_Contries.bar_label(Tyes_Indus.containers[0], label_type = 'edge')
Top5_Contries.margins(y = 0.1)
plt.show()

# Observation.
USA has the highest count of funding with a total of 562 investors funding, followed by China with 172 count of investors funding.

uc.dtypes

uc.info()



uc['Funding'] = uc['Funding'].astype(int)


uc.dtypes

uc.info()

# Bottom 4 countries with minimun funding by investors
Country_Funding = uc['Funding'].groupby(uc.Country).min().sort_values().tail(4)
Country_Funding

# Visualize using pie chat the top 3 price
explode = (0.1, 0, 0)
plt.pie(Country_Funding, labels = Country_Funding.index, autopct = '%2.2f%%', shadow = True, startangle = 130)
plt.title('Top 3 location by price')
plt.show()

# Which country has the minimun funding 
Country_Valuation = uc['Valuation'].groupby(uc.Country).max().sort_values().tail(4)
Country_Valuation

