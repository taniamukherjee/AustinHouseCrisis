

```python
# Dependencies
import matplotlib.pyplot as plt
import matplotlib.patches as mpatches
import pandas as pd
import numpy as np
import scipy.stats as stats
from scipy.stats.stats import pearsonr
```


```python
# Files to Load - Population Data
population_2007 = "population data/2007.csv"
population_2008 = "population data/2008.csv"
population_2009 = "population data/2009.csv"
population_2010_2016 = "population data/2010 - 2016.csv"

# Files to Load - Employment Data
employment_hays = "employment data/Hays_County.csv"
employment_travis = "employment data/Travis_County.csv"
employment_williamson = "employment data/Williamson_County.csv"

# Files to Load - Wage Data
wage_hays = "wage data/hays_wages_revised.csv"
wage_travis = "wage data/travis_wages_revised.csv"
wage_williamson = "wage data/williamson_wages_revised.csv"

# Files to Load - Hays Data
hays_gross_income_percent = "hays_data/hays_gross_income_percent.csv"
hays_gross_rent = "hays_data/hays_gross_rent.csv"
hays_housing_tenure = "hays_data/hays_housing_tenure.csv"
hays_housing_value = "hays_data/hays_housing_value.csv"
hays_income_percent_with_mortgage = "hays_data/hays_income_percent_with_mortgage.csv"
hays_income_percent_without_mortgage = "hays_data/hays_income_percent_without_mortgage.csv"
hays_monthly_costs_with_mortgage = "hays_data/hays_monthly_costs_with_mortgage.csv"
hays_monthly_costs_without_mortgage = "hays_data/hays_monthly_costs_without_mortgage.csv"
hays_total_housing_units = "hays_data/hays_total_housing_units.csv"
hays_year_moved_in = "hays_data/hays_year_householder_moved_into_unit.csv"

# Files to Load - Travis Data
travis_gross_rent_percent = "Travis_County_Data/Gross Rent.csv"
travis_gross_rent = "Travis_County_Data/Gross.csv"
travis_housing_tenure = "Travis_County_Data/Housing_Tenure.csv"
travis_mortgage = "Travis_County_Data/Mortage_Status.csv"
travis_occupancy = "Travis_County_Data/Occupancy.csv"
travis_income_percent = "Travis_County_Data/Selected_Monthly_Percent.csv"
travis_housing_value = "Travis_County_Data/Values.csv"
travis_year_moved_in = "Travis_County_Data/Years_Moved_in.csv"

# Files to Load - Williamson Data
williamson_gross_rent_percent = "williamson_data/williamson_GRAPI.csv"
williamson_gross_rent = "williamson_data/williamson_gross_rent.csv"
williamson_housing = "williamson_data/williamson_housing.csv"
williamson_mortage_status = "williamson_data/williamson_mortage_status.csv"
williamson_mortgages = "williamson_data/smoc_with_mortgage.csv"
williamson_SMOCAPI = "williamson_data/williamson_SMOCAPI.csv"
williamson_tenure = "williamson_data/williamson_tenure.csv"
williamson_value = "williamson_data/williamson_value.csv"
williamson_year_built = "williamson_data/williamson_year_built.csv"
```


```python
# Read the data
population_2007_data_df = pd.read_csv(population_2007,thousands = ",")
population_2008_data_df = pd.read_csv(population_2008,thousands = ",")
population_2009_data_df = pd.read_csv(population_2009,thousands = ",")
population_2010_2016_data_df = pd.read_csv(population_2010_2016,thousands = ",")

employment_hays_data_df = pd.read_csv(employment_hays,thousands = ",")
employment_travis_data_df = pd.read_csv(employment_travis,thousands = ",")
employment_williamson_data_df = pd.read_csv(employment_williamson,thousands = ",")

wage_hays_data_df = pd.read_csv(wage_hays,thousands = ",")
wage_travis_data_df = pd.read_csv(wage_travis,thousands = ",")
wage_williamson_data_df = pd.read_csv(wage_williamson,thousands = ",")

hays_gross_income_percent_data_df = pd.read_csv(hays_gross_income_percent, thousands = ",")
hays_gross_rent_data_df = pd.read_csv(hays_gross_rent,thousands = ",")
hays_housing_tenure_data_df = pd.read_csv(hays_housing_tenure,thousands = ",")
hays_housing_value_data_df = pd.read_csv(hays_housing_value,thousands = ",")
hays_income_percent_with_mortgage_data_df = pd.read_csv(hays_income_percent_with_mortgage, thousands = ",")
hays_income_percent_without_mortgage_data_df = pd.read_csv(hays_income_percent_without_mortgage,thousands = ",")
hays_monthly_costs_with_mortgage_data_df = pd.read_csv(hays_monthly_costs_with_mortgage, thousands = ",")
hays_monthly_costs_without_mortgage_data_df = pd.read_csv(hays_monthly_costs_without_mortgage,thousands = ",")
hays_total_housing_units_data_df = pd.read_csv(hays_total_housing_units,thousands = ",")
hays_year_moved_in_data_df = pd.read_csv(hays_year_moved_in)

travis_gross_rent_percent_data_df = pd.read_csv(travis_gross_rent_percent)
travis_gross_rent_data_df = pd.read_csv(travis_gross_rent)
travis_housing_tenure_data_df = pd.read_csv(travis_housing_tenure)
travis_mortgage_data_df = pd.read_csv(travis_mortgage)
travis_occupancy_data_df = pd.read_csv(travis_occupancy)
travis_income_percent_data_df = pd.read_csv(travis_income_percent)
travis_housing_value_data_df = pd.read_csv(travis_housing_value)
travis_year_moved_in_data_df = pd.read_csv(travis_year_moved_in)


williamson_gross_rent_percent_data_df = pd.read_csv(williamson_gross_rent_percent,sep='\t',thousands = ",")
williamson_gross_rent_data_df = pd.read_csv(williamson_gross_rent,sep='\t',thousands = ",")
williamson_housing_data_df = pd.read_csv(williamson_housing,sep='\t',thousands = ",")
williamson_mortage_status_data_df = pd.read_csv(williamson_mortage_status,thousands = ",")
williamson_mortgage_df = pd.read_csv(williamson_mortgages,thousands = ",")
williamson_SMOCAPI_data_df = pd.read_csv(williamson_SMOCAPI,sep='\t', thousands = ",")
williamson_tenure_data_df = pd.read_csv(williamson_tenure,sep='\t',thousands = ",")
williamson_value_data_df = pd.read_csv(williamson_value,thousands = ",")
williamson_year_built_data_df = pd.read_csv(williamson_year_built)
```


```python
# Data Cleaning - drop rows
williamson_mortage_status_data_drop_df = williamson_mortage_status_data_df.drop(williamson_mortage_status_data_df.index[3:])
williamson_value_data_drop_df = williamson_value_data_df.drop(williamson_value_data_df.index[10:])
williamson_year_built_data_drop_df = williamson_year_built_data_df.drop(williamson_year_built_data_df.index[3:])
williamson_mortgage_clean_df = williamson_mortgage_df.drop(williamson_mortgage_df.index[7:])
```


```python
## NEED TO UPDATE - create dataframe & drop columns
williamson_mortage_status_data_drop_pd = pd.DataFrame(williamson_mortage_status_data_drop_df, columns=["MORTGAGE STATUS", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"])
williamson_value_data_drop_pd = pd.DataFrame(williamson_value_data_drop_df, columns=["VALUE", "2007", "2008", "2009", "2010", "2011", "2012", "2013", "2014", "2015", "2016"])
williamson_year_built_data_drop_pd = pd.DataFrame(williamson_year_built_data_drop_df, columns=["MOVE IN YEAR", "2013", "2014", "2015", "2016"])
```


```python
williamson_year_built_data_drop_pd
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>MOVE IN YEAR</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Occupied housing units</td>
      <td>161,887</td>
      <td>164,805</td>
      <td>170,987</td>
      <td>173,125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Moved in 2010 or Later</td>
      <td>61,540</td>
      <td>136,422</td>
      <td>89,612</td>
      <td>103,889</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Moved in 2000 to 2009</td>
      <td>69,134</td>
      <td>18,128</td>
      <td>52,657</td>
      <td>45,247</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Data Cleaning - drop NA's

hays_gross_income_percent_data_clean_df = hays_gross_income_percent_data_df.dropna(how = "any")
hays_gross_rent_data_clean_df = hays_gross_rent_data_df.dropna(how = "any")
hays_housing_tenure_data_clean_df = hays_housing_tenure_data_df.dropna(how = "any")
hays_housing_value_data_clean_df = hays_housing_value_data_df.dropna(how = "any")
hays_income_percent_with_mortgage_data_clean_df = hays_income_percent_with_mortgage_data_df.dropna(how = "any")
hays_income_percent_without_mortgage_data_clean_df = hays_income_percent_without_mortgage_data_df.dropna(how = "any")
hays_monthly_costs_with_mortgage_data_clean_df = hays_monthly_costs_with_mortgage_data_df.dropna(how = "any")
hays_monthly_costs_without_mortgage_data_clean_df = hays_monthly_costs_without_mortgage_data_df.dropna(how = "any")
hays_total_housing_units_data_clean_df = hays_total_housing_units_data_df.dropna(how = "any")
williamson_gross_rent_percent_data_clean_df = williamson_gross_rent_percent_data_df.dropna(how = "any")
williamson_gross_rent_data_clean_df = williamson_gross_rent_data_df.dropna(how = "any")
williamson_SMOCAPI_data_clean_df = williamson_SMOCAPI_data_df.dropna(how = "any")
williamson_SMOCAPI_data_clean_df = williamson_SMOCAPI_data_clean_df.reset_index()
williamson_tenure_data_clean_df = williamson_tenure_data_df.dropna(how = "any")
```


```python
# Merge Wage dataframes
wage_merge = wage_hays_data_df.append(wage_travis_data_df)
wage_merge_final = wage_merge.append(wage_williamson_data_df)
wage_merge_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GeoFips</th>
      <th>GeoName</th>
      <th>LineCode</th>
      <th>Description</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>48209</td>
      <td>Hays, TX</td>
      <td>3</td>
      <td>Per capita personal income (dollars) 2/</td>
      <td>32263</td>
      <td>33820</td>
      <td>32113</td>
      <td>32530</td>
      <td>34444</td>
      <td>33792</td>
      <td>34075</td>
      <td>36194</td>
      <td>38448</td>
      <td>38912</td>
    </tr>
    <tr>
      <th>0</th>
      <td>48453</td>
      <td>Travis, TX</td>
      <td>3</td>
      <td>Per capita personal income (dollars) 2/</td>
      <td>42972</td>
      <td>45947</td>
      <td>42529</td>
      <td>43924</td>
      <td>47750</td>
      <td>52582</td>
      <td>52938</td>
      <td>56090</td>
      <td>58221</td>
      <td>58700</td>
    </tr>
    <tr>
      <th>0</th>
      <td>48491</td>
      <td>Williamson, TX</td>
      <td>3</td>
      <td>Per capita personal income (dollars) 2/</td>
      <td>36963</td>
      <td>37874</td>
      <td>36299</td>
      <td>36912</td>
      <td>38308</td>
      <td>38656</td>
      <td>39067</td>
      <td>41429</td>
      <td>44036</td>
      <td>44679</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge Employment dataframes
employment_merge = employment_hays_data_df.append(employment_travis_data_df)
employment_merge_final = employment_merge.append(employment_williamson_data_df)
```


```python
employment_merge_final.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Period ID</th>
      <th>Period</th>
      <th>Area</th>
      <th>Adjusted</th>
      <th>Labor Force</th>
      <th>Employment</th>
      <th>Unemployment</th>
      <th>Unemployment Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2016</td>
      <td>0</td>
      <td>Annual</td>
      <td>Hays County</td>
      <td>Not Adj</td>
      <td>101898</td>
      <td>98498</td>
      <td>3400</td>
      <td>3.3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>0</td>
      <td>Annual</td>
      <td>Hays County</td>
      <td>Not Adj</td>
      <td>98153</td>
      <td>94786</td>
      <td>3367</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014</td>
      <td>0</td>
      <td>Annual</td>
      <td>Hays County</td>
      <td>Not Adj</td>
      <td>93897</td>
      <td>89887</td>
      <td>4010</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2013</td>
      <td>0</td>
      <td>Annual</td>
      <td>Hays County</td>
      <td>Not Adj</td>
      <td>90011</td>
      <td>85232</td>
      <td>4779</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2012</td>
      <td>0</td>
      <td>Annual</td>
      <td>Hays County</td>
      <td>Not Adj</td>
      <td>85818</td>
      <td>80810</td>
      <td>5008</td>
      <td>5.8</td>
    </tr>
  </tbody>
</table>
</div>



# Occupied vs. Vacant


```python
#use previous data frames to make data
data_for_merged_housing = { "Austin Housing" : travis_occupancy_data_df["HOUSING OCCUPANCY"],
                            "Hays County 2007" : hays_total_housing_units_data_clean_df["2007"],
                           "Travis County 2007" : travis_occupancy_data_df["2007"],  
                           "Williamson County 2007" : williamson_housing_data_df["2007"],
                           "Hays County 2008" : hays_total_housing_units_data_clean_df["2008"],
                           "Travis County 2008" : travis_occupancy_data_df["2008"],  
                           "Williamson County 2008" : williamson_housing_data_df["2008"],
                           "Hays County 2009" : hays_total_housing_units_data_clean_df["2009"],
                           "Travis County 2009" : travis_occupancy_data_df["2009"],  
                           "Williamson County 2009" : williamson_housing_data_df["2009"],
                           "Hays County 2010" : hays_total_housing_units_data_clean_df["2010"],
                           "Travis County 2010" : travis_occupancy_data_df["2010"],  
                           "Williamson County 2010" : williamson_housing_data_df["2010"],
                           "Hays County 2011" : hays_total_housing_units_data_clean_df["2011"],
                           "Travis County 2011" : travis_occupancy_data_df["2011"],  
                           "Williamson County 2011" : williamson_housing_data_df["2011"],
                           "Hays County 2012" : hays_total_housing_units_data_clean_df["2012"],
                           "Travis County 2012" : travis_occupancy_data_df["2012"],  
                           "Williamson County 2012" : williamson_housing_data_df["2012"],
                           "Hays County 2013" : hays_total_housing_units_data_clean_df["2013"],
                           "Travis County 2013" : travis_occupancy_data_df["2013"],  
                           "Williamson County 2013" : williamson_housing_data_df["2013"],
                           "Hays County 2014" : hays_total_housing_units_data_clean_df["2014"],
                           "Travis County 2014" : travis_occupancy_data_df["2014"],  
                           "Williamson County 2014" : williamson_housing_data_df["2014"],
                           "Hays County 2015" : hays_total_housing_units_data_clean_df["2015"],
                           "Travis County 2015" : travis_occupancy_data_df["2015"],  
                           "Williamson County 2015" : williamson_housing_data_df["2015"],
                           "Hays County 2016" : hays_total_housing_units_data_clean_df["2016"],
                           "Travis County 2016" : travis_occupancy_data_df["2016"],  
                           "Williamson County 2016" : williamson_housing_data_df["2016"],
                           
                            
    
}
```


```python
#make a total merged DF
total_merged_housing_df = pd.DataFrame(data_for_merged_housing)
```


```python
total_merged_housing_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total housing units</td>
      <td>49386.0</td>
      <td>51266.0</td>
      <td>53176.0</td>
      <td>59747.0</td>
      <td>61833.0</td>
      <td>64338.0</td>
      <td>67307.0</td>
      <td>70729.0</td>
      <td>72977.0</td>
      <td>...</td>
      <td>131173.0</td>
      <td>136951.0</td>
      <td>142237.0</td>
      <td>163264.0</td>
      <td>168523.0</td>
      <td>167203.0</td>
      <td>171144.0</td>
      <td>175673.0</td>
      <td>181000.0</td>
      <td>186975.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Occupied housing units</td>
      <td>44803.0</td>
      <td>47008.0</td>
      <td>48709.0</td>
      <td>54422.0</td>
      <td>56754.0</td>
      <td>57395.0</td>
      <td>60739.0</td>
      <td>63497.0</td>
      <td>67346.0</td>
      <td>...</td>
      <td>121899.0</td>
      <td>127842.0</td>
      <td>132992.0</td>
      <td>152739.0</td>
      <td>156738.0</td>
      <td>156215.0</td>
      <td>161887.0</td>
      <td>164805.0</td>
      <td>170987.0</td>
      <td>173125.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Vacant housing units</td>
      <td>4583.0</td>
      <td>4258.0</td>
      <td>4467.0</td>
      <td>5325.0</td>
      <td>5079.0</td>
      <td>6943.0</td>
      <td>6568.0</td>
      <td>7232.0</td>
      <td>5631.0</td>
      <td>...</td>
      <td>9274.0</td>
      <td>9109.0</td>
      <td>9245.0</td>
      <td>10525.0</td>
      <td>11785.0</td>
      <td>10988.0</td>
      <td>9257.0</td>
      <td>10868.0</td>
      <td>10013.0</td>
      <td>13850.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Homeowner vacancy rate</td>
      <td>1.5</td>
      <td>1.3</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.5</td>
      <td>2.4</td>
      <td>1.1</td>
      <td>3.0</td>
      <td>0.9</td>
      <td>...</td>
      <td>2.2</td>
      <td>1.7</td>
      <td>1.4</td>
      <td>1.6</td>
      <td>1.4</td>
      <td>2.1</td>
      <td>2.1</td>
      <td>0.6</td>
      <td>1.2</td>
      <td>1.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rental vacancy rate</td>
      <td>5.5</td>
      <td>3.0</td>
      <td>10.0</td>
      <td>2.0</td>
      <td>4.7</td>
      <td>3.7</td>
      <td>9.2</td>
      <td>8.0</td>
      <td>7.0</td>
      <td>...</td>
      <td>4.1</td>
      <td>6.9</td>
      <td>8.1</td>
      <td>7.0</td>
      <td>5.5</td>
      <td>5.2</td>
      <td>4.6</td>
      <td>8.2</td>
      <td>5.3</td>
      <td>8.6</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 31 columns</p>
</div>




```python
#prep to make merged rent data dataframe
#dropped unneeded row for consistency
hays_gross_rent_data_clean_df = hays_gross_rent_data_clean_df.drop(hays_gross_rent_data_clean_df.index[0])
hays_gross_rent_data_clean_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GROSS RENT</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Less than $200</td>
      <td>0.0</td>
      <td>30.0</td>
      <td>10.0</td>
      <td>389.0</td>
      <td>69.0</td>
      <td>99.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>898.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$200 to $299</td>
      <td>281.0</td>
      <td>290.0</td>
      <td>25.0</td>
      <td>298.0</td>
      <td>0.0</td>
      <td>370.0</td>
      <td>85.0</td>
      <td>129.0</td>
      <td>687.0</td>
      <td>12088.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$300 to $499</td>
      <td>2327.0</td>
      <td>1446.0</td>
      <td>828.0</td>
      <td>740.0</td>
      <td>669.0</td>
      <td>992.0</td>
      <td>561.0</td>
      <td>728.0</td>
      <td>831.0</td>
      <td>7416.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$500 to $749</td>
      <td>6274.0</td>
      <td>5444.0</td>
      <td>6043.0</td>
      <td>4959.0</td>
      <td>4659.0</td>
      <td>3871.0</td>
      <td>4138.0</td>
      <td>2630.0</td>
      <td>4340.0</td>
      <td>4100.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$750 to $999</td>
      <td>3328.0</td>
      <td>3911.0</td>
      <td>4368.0</td>
      <td>4574.0</td>
      <td>5686.0</td>
      <td>6297.0</td>
      <td>7274.0</td>
      <td>7924.0</td>
      <td>7190.0</td>
      <td>882.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>6</th>
      <td>$1,000 to $1,499</td>
      <td>1874.0</td>
      <td>3238.0</td>
      <td>2715.0</td>
      <td>3181.0</td>
      <td>4460.0</td>
      <td>5248.0</td>
      <td>4969.0</td>
      <td>6948.0</td>
      <td>7235.0</td>
      <td>109.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>7</th>
      <td>$1,500 or more</td>
      <td>322.0</td>
      <td>354.0</td>
      <td>1146.0</td>
      <td>849.0</td>
      <td>931.0</td>
      <td>2521.0</td>
      <td>1761.0</td>
      <td>2112.0</td>
      <td>3640.0</td>
      <td>0.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>8</th>
      <td>No rent paid</td>
      <td>1038.0</td>
      <td>818.0</td>
      <td>506.0</td>
      <td>773.0</td>
      <td>536.0</td>
      <td>495.0</td>
      <td>843.0</td>
      <td>517.0</td>
      <td>629.0</td>
      <td>536.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Median (dollars)</td>
      <td>667.0</td>
      <td>754.0</td>
      <td>778.0</td>
      <td>817.0</td>
      <td>847.0</td>
      <td>891.0</td>
      <td>910.0</td>
      <td>964.0</td>
      <td>960.0</td>
      <td>994.0</td>
      <td>1,074</td>
    </tr>
  </tbody>
</table>
</div>




```python
hays_gross_rent_data_clean_df = hays_gross_rent_data_clean_df.reset_index()
```


```python
#further cleaning of williamson df, drop unneeded rows
williamson_gross_rent_data_clean_df = williamson_gross_rent_data_clean_df.drop(williamson_gross_rent_data_clean_df.index[0])
williamson_gross_rent_data_clean_df = williamson_gross_rent_data_clean_df.drop(williamson_gross_rent_data_clean_df.index[3])
williamson_gross_rent_data_clean_df = williamson_gross_rent_data_clean_df.drop(williamson_gross_rent_data_clean_df.index[5])
williamson_gross_rent_data_clean_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GROSS RENT</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Less than $200</td>
      <td>197.0</td>
      <td>34.0</td>
      <td>189.0</td>
      <td>153.0</td>
      <td>129.0</td>
      <td>682.0</td>
      <td>18.0</td>
      <td>413.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$200 to $299</td>
      <td>559.0</td>
      <td>582.0</td>
      <td>189.0</td>
      <td>398.0</td>
      <td>421.0</td>
      <td>428.0</td>
      <td>166.0</td>
      <td>993.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$300 to $499</td>
      <td>756.0</td>
      <td>685.0</td>
      <td>303.0</td>
      <td>1105.0</td>
      <td>721.0</td>
      <td>763.0</td>
      <td>801.0</td>
      <td>268.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$500 to $749</td>
      <td>5487.0</td>
      <td>4555.0</td>
      <td>5038.0</td>
      <td>9144.0</td>
      <td>8951.0</td>
      <td>7295.0</td>
      <td>5362.0</td>
      <td>4423.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>$750 to $999</td>
      <td>11335.0</td>
      <td>11952.0</td>
      <td>13221.0</td>
      <td>16541.0</td>
      <td>15642.0</td>
      <td>14224.0</td>
      <td>16943.0</td>
      <td>18493.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>$1,000 to $1,499</td>
      <td>11532.0</td>
      <td>12808.0</td>
      <td>6829.0</td>
      <td>16972.0</td>
      <td>19685.0</td>
      <td>19652.0</td>
      <td>17111.0</td>
      <td>17265.0</td>
      <td>21276.0</td>
      <td>24810.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>$1,500 or more</td>
      <td>3056.0</td>
      <td>4349.0</td>
      <td>867.0</td>
      <td>6361.0</td>
      <td>5892.0</td>
      <td>7715.0</td>
      <td>7309.0</td>
      <td>10398.0</td>
      <td>32855.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>No rent paid</td>
      <td>870.0</td>
      <td>1919.0</td>
      <td>860.0</td>
      <td>1467.0</td>
      <td>626.0</td>
      <td>1163.0</td>
      <td>1433.0</td>
      <td>1838.0</td>
      <td>1423.0</td>
      <td>1599.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Median (dollars)</td>
      <td>963.0</td>
      <td>929.0</td>
      <td>1002.0</td>
      <td>970.0</td>
      <td>998.0</td>
      <td>1044.0</td>
      <td>1013.0</td>
      <td>1034.0</td>
      <td>1146.0</td>
      <td>1240.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
williamson_gross_rent_data_clean_df = williamson_gross_rent_data_clean_df.reset_index()
```


```python
#check travis df
travis_gross_rent_data_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GROSS RENT</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Less than $200</td>
      <td>1997</td>
      <td>1862</td>
      <td>1777</td>
      <td>1659</td>
      <td>601</td>
      <td>2676</td>
      <td>1889</td>
      <td>1950</td>
      <td>1003</td>
      <td>6273</td>
      <td>8045</td>
    </tr>
    <tr>
      <th>1</th>
      <td>$200 to $299</td>
      <td>1549</td>
      <td>1530</td>
      <td>1665</td>
      <td>1684</td>
      <td>2672</td>
      <td>2027</td>
      <td>1789</td>
      <td>1676</td>
      <td>2002</td>
      <td>68144</td>
      <td>55556</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$300 to $499</td>
      <td>8227</td>
      <td>7095</td>
      <td>5623</td>
      <td>5851</td>
      <td>5600</td>
      <td>4048</td>
      <td>4599</td>
      <td>4709</td>
      <td>4225</td>
      <td>92284</td>
      <td>94465</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$500 to $749</td>
      <td>56099</td>
      <td>54854</td>
      <td>47118</td>
      <td>46090</td>
      <td>45468</td>
      <td>42619</td>
      <td>34640</td>
      <td>25207</td>
      <td>21714</td>
      <td>34184</td>
      <td>41264</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$750 to $999</td>
      <td>53449</td>
      <td>54346</td>
      <td>56939</td>
      <td>61615</td>
      <td>62546</td>
      <td>64301</td>
      <td>59801</td>
      <td>65435</td>
      <td>57273</td>
      <td>8539</td>
      <td>10602</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$1,000 to $1,499</td>
      <td>32683</td>
      <td>34017</td>
      <td>43332</td>
      <td>48991</td>
      <td>57006</td>
      <td>61541</td>
      <td>64609</td>
      <td>72205</td>
      <td>83031</td>
      <td>2031</td>
      <td>3419</td>
    </tr>
    <tr>
      <th>6</th>
      <td>$1,500 or more</td>
      <td>10689</td>
      <td>11533</td>
      <td>15102</td>
      <td>15098</td>
      <td>19096</td>
      <td>22902</td>
      <td>28961</td>
      <td>32560</td>
      <td>40823</td>
      <td>2710</td>
      <td>2711</td>
    </tr>
    <tr>
      <th>7</th>
      <td>No cash rent</td>
      <td>3390</td>
      <td>3791</td>
      <td>871</td>
      <td>885</td>
      <td>3737</td>
      <td>5308</td>
      <td>4939</td>
      <td>3490</td>
      <td>4102</td>
      <td>4264</td>
      <td>5462</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Median (dollars)</td>
      <td>803</td>
      <td>816</td>
      <td>3581</td>
      <td>3492</td>
      <td>918</td>
      <td>918</td>
      <td>981</td>
      <td>1017</td>
      <td>1092</td>
      <td>1147</td>
      <td>1191</td>
    </tr>
  </tbody>
</table>
</div>




```python
#set the data for the complete merged dataframe
data_for_merged_rent_data = { "Austin Housing" : travis_gross_rent_data_df["GROSS RENT"],
                            "Hays County 2007" : hays_gross_rent_data_clean_df["2007"],
                           "Travis County 2007" : travis_gross_rent_data_df["2007"],  
                           "Williamson County 2007" : williamson_gross_rent_data_clean_df["2007"],
                           "Hays County 2008" : hays_gross_rent_data_clean_df["2008"],
                           "Travis County 2008" : travis_gross_rent_data_df["2008"],  
                           "Williamson County 2008" : williamson_gross_rent_data_clean_df["2008"],
                           "Hays County 2009" : hays_gross_rent_data_clean_df["2009"],
                           "Travis County 2009" : travis_gross_rent_data_df["2009"],  
                           "Williamson County 2009" : williamson_gross_rent_data_clean_df["2009"],
                           "Hays County 2010" : hays_gross_rent_data_clean_df["2010"],
                           "Travis County 2010" : travis_gross_rent_data_df["2010"],  
                           "Williamson County 2010" : williamson_gross_rent_data_clean_df["2010"],
                           "Hays County 2011" : hays_gross_rent_data_clean_df["2011"],
                           "Travis County 2011" : travis_gross_rent_data_df["2011"],  
                           "Williamson County 2011" : williamson_gross_rent_data_clean_df["2011"],
                           "Hays County 2012" : hays_gross_rent_data_clean_df["2012"],
                           "Travis County 2012" : travis_gross_rent_data_df["2012"],  
                           "Williamson County 2012" : williamson_gross_rent_data_clean_df["2012"],
                           "Hays County 2013" : hays_gross_rent_data_clean_df["2013"],
                           "Travis County 2013" : travis_gross_rent_data_df["2013"],  
                           "Williamson County 2013" : williamson_gross_rent_data_clean_df["2013"],
                           "Hays County 2014" : hays_gross_rent_data_clean_df["2014"],
                           "Travis County 2014" : travis_gross_rent_data_df["2014"],  
                           "Williamson County 2014" : williamson_gross_rent_data_clean_df["2014"],
                           "Hays County 2015" : hays_gross_rent_data_clean_df["2015"],
                           "Travis County 2015" : travis_gross_rent_data_df["2015"],  
                           "Williamson County 2015" : williamson_gross_rent_data_clean_df["2015"],
                           "Hays County 2016" : hays_gross_rent_data_clean_df["2016"],
                           "Travis County 2016" : travis_gross_rent_data_df["2016"],  
                           "Williamson County 2016" : williamson_gross_rent_data_clean_df["2016"],
                           
                            
    
}
```


```python
complete_merged_rent_data_df = pd.DataFrame(data_for_merged_rent_data)
```


```python
complete_merged_rent_data_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Less than $200</td>
      <td>30.0</td>
      <td>10.0</td>
      <td>389.0</td>
      <td>69.0</td>
      <td>99.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>898.0</td>
      <td>...</td>
      <td>197.0</td>
      <td>34.0</td>
      <td>189.0</td>
      <td>153.0</td>
      <td>129.0</td>
      <td>682.0</td>
      <td>18.0</td>
      <td>413.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>$200 to $299</td>
      <td>290.0</td>
      <td>25.0</td>
      <td>298.0</td>
      <td>0.0</td>
      <td>370.0</td>
      <td>85.0</td>
      <td>129.0</td>
      <td>687.0</td>
      <td>12088.0</td>
      <td>...</td>
      <td>559.0</td>
      <td>582.0</td>
      <td>189.0</td>
      <td>398.0</td>
      <td>421.0</td>
      <td>428.0</td>
      <td>166.0</td>
      <td>993.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$300 to $499</td>
      <td>1446.0</td>
      <td>828.0</td>
      <td>740.0</td>
      <td>669.0</td>
      <td>992.0</td>
      <td>561.0</td>
      <td>728.0</td>
      <td>831.0</td>
      <td>7416.0</td>
      <td>...</td>
      <td>756.0</td>
      <td>685.0</td>
      <td>303.0</td>
      <td>1105.0</td>
      <td>721.0</td>
      <td>763.0</td>
      <td>801.0</td>
      <td>268.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$500 to $749</td>
      <td>5444.0</td>
      <td>6043.0</td>
      <td>4959.0</td>
      <td>4659.0</td>
      <td>3871.0</td>
      <td>4138.0</td>
      <td>2630.0</td>
      <td>4340.0</td>
      <td>4100.0</td>
      <td>...</td>
      <td>5487.0</td>
      <td>4555.0</td>
      <td>5038.0</td>
      <td>9144.0</td>
      <td>8951.0</td>
      <td>7295.0</td>
      <td>5362.0</td>
      <td>4423.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$750 to $999</td>
      <td>3911.0</td>
      <td>4368.0</td>
      <td>4574.0</td>
      <td>5686.0</td>
      <td>6297.0</td>
      <td>7274.0</td>
      <td>7924.0</td>
      <td>7190.0</td>
      <td>882.0</td>
      <td>...</td>
      <td>11335.0</td>
      <td>11952.0</td>
      <td>13221.0</td>
      <td>16541.0</td>
      <td>15642.0</td>
      <td>14224.0</td>
      <td>16943.0</td>
      <td>18493.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$1,000 to $1,499</td>
      <td>3238.0</td>
      <td>2715.0</td>
      <td>3181.0</td>
      <td>4460.0</td>
      <td>5248.0</td>
      <td>4969.0</td>
      <td>6948.0</td>
      <td>7235.0</td>
      <td>109.0</td>
      <td>...</td>
      <td>11532.0</td>
      <td>12808.0</td>
      <td>6829.0</td>
      <td>16972.0</td>
      <td>19685.0</td>
      <td>19652.0</td>
      <td>17111.0</td>
      <td>17265.0</td>
      <td>21276.0</td>
      <td>24810.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>$1,500 or more</td>
      <td>354.0</td>
      <td>1146.0</td>
      <td>849.0</td>
      <td>931.0</td>
      <td>2521.0</td>
      <td>1761.0</td>
      <td>2112.0</td>
      <td>3640.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>3056.0</td>
      <td>4349.0</td>
      <td>867.0</td>
      <td>6361.0</td>
      <td>5892.0</td>
      <td>7715.0</td>
      <td>7309.0</td>
      <td>10398.0</td>
      <td>32855.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>No cash rent</td>
      <td>818.0</td>
      <td>506.0</td>
      <td>773.0</td>
      <td>536.0</td>
      <td>495.0</td>
      <td>843.0</td>
      <td>517.0</td>
      <td>629.0</td>
      <td>536.0</td>
      <td>...</td>
      <td>870.0</td>
      <td>1919.0</td>
      <td>860.0</td>
      <td>1467.0</td>
      <td>626.0</td>
      <td>1163.0</td>
      <td>1433.0</td>
      <td>1838.0</td>
      <td>1423.0</td>
      <td>1599.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Median (dollars)</td>
      <td>754.0</td>
      <td>778.0</td>
      <td>817.0</td>
      <td>847.0</td>
      <td>891.0</td>
      <td>910.0</td>
      <td>964.0</td>
      <td>960.0</td>
      <td>994.0</td>
      <td>...</td>
      <td>963.0</td>
      <td>929.0</td>
      <td>1002.0</td>
      <td>970.0</td>
      <td>998.0</td>
      <td>1044.0</td>
      <td>1013.0</td>
      <td>1034.0</td>
      <td>1146.0</td>
      <td>1240.0</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 31 columns</p>
</div>




```python
#prep to make a merged GRAPI dataframe
#do some extra cleaning, drop unnecessary rows
hays_gross_income_percent_data_clean_df = hays_gross_income_percent_data_clean_df.drop(hays_gross_income_percent_data_clean_df.index[0])
hays_gross_income_percent_data_clean_df = hays_gross_income_percent_data_clean_df.reset_index()
hays_gross_income_percent_data_clean_df

williamson_gross_rent_percent_data_clean_df = williamson_gross_rent_percent_data_clean_df.drop(williamson_gross_rent_percent_data_clean_df.index[0])
williamson_gross_rent_percent_data_clean_df = williamson_gross_rent_percent_data_clean_df.reset_index()
williamson_gross_rent_percent_data_clean_df

travis_gross_rent_percent_data_df = travis_gross_rent_percent_data_df.reset_index()
travis_gross_rent_percent_data_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>GROSS RENT AS A PERCENTAGE OF HOUSEHOLD INCOME</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Less than 15.0 percent</td>
      <td>21295</td>
      <td>20772</td>
      <td>21071</td>
      <td>21594</td>
      <td>18095</td>
      <td>19293</td>
      <td>21561</td>
      <td>20514</td>
      <td>22342</td>
      <td>25453</td>
      <td>22198</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>15.0 to 19.9 percent</td>
      <td>22719</td>
      <td>21280</td>
      <td>21928</td>
      <td>23792</td>
      <td>22731</td>
      <td>23749</td>
      <td>26093</td>
      <td>24761</td>
      <td>24298</td>
      <td>27415</td>
      <td>27494</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>20.0 to 24.9 percent</td>
      <td>22683</td>
      <td>22739</td>
      <td>23952</td>
      <td>24927</td>
      <td>21902</td>
      <td>28948</td>
      <td>24038</td>
      <td>28211</td>
      <td>27437</td>
      <td>30385</td>
      <td>31533</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>25.0 to 29.9 percent</td>
      <td>20316</td>
      <td>19709</td>
      <td>19939</td>
      <td>21304</td>
      <td>20230</td>
      <td>23040</td>
      <td>22844</td>
      <td>26757</td>
      <td>28288</td>
      <td>24531</td>
      <td>29373</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>30.0 to 34.9 percent</td>
      <td>10968</td>
      <td>14072</td>
      <td>14583</td>
      <td>15976</td>
      <td>19405</td>
      <td>18529</td>
      <td>17106</td>
      <td>17838</td>
      <td>19164</td>
      <td>19467</td>
      <td>19132</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>35.0 percent or more</td>
      <td>62404</td>
      <td>63354</td>
      <td>66395</td>
      <td>70094</td>
      <td>87062</td>
      <td>80673</td>
      <td>80667</td>
      <td>82495</td>
      <td>83157</td>
      <td>81353</td>
      <td>81637</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Not computed</td>
      <td>7698</td>
      <td>7102</td>
      <td>7269</td>
      <td>6793</td>
      <td>7301</td>
      <td>11190</td>
      <td>8918</td>
      <td>6656</td>
      <td>9487</td>
      <td>9825</td>
      <td>10157</td>
    </tr>
  </tbody>
</table>
</div>




```python
#set all the GRAPI data
data_for_combined_grapi_df = { "Austin Housing" : travis_gross_rent_percent_data_df["GROSS RENT AS A PERCENTAGE OF HOUSEHOLD INCOME"],
                            "Hays County 2007" : hays_gross_income_percent_data_clean_df["2007"],
                           "Travis County 2007" : travis_gross_rent_percent_data_df["2007"],  
                           "Williamson County 2007" : williamson_gross_rent_percent_data_clean_df["2007"],
                           "Hays County 2008" : hays_gross_income_percent_data_clean_df["2008"],
                           "Travis County 2008" : travis_gross_rent_percent_data_df["2008"],  
                           "Williamson County 2008" : williamson_gross_rent_percent_data_clean_df["2008"],
                           "Hays County 2009" : hays_gross_income_percent_data_clean_df["2009"],
                           "Travis County 2009" : travis_gross_rent_percent_data_df["2009"],  
                           "Williamson County 2009" : williamson_gross_rent_percent_data_clean_df["2009"],
                           "Hays County 2010" : hays_gross_income_percent_data_clean_df["2010"],
                           "Travis County 2010" : travis_gross_rent_percent_data_df["2010"],  
                           "Williamson County 2010" : williamson_gross_rent_percent_data_clean_df["2010"],
                           "Hays County 2011" : hays_gross_income_percent_data_clean_df["2011"],
                           "Travis County 2011" : travis_gross_rent_percent_data_df["2011"],  
                           "Williamson County 2011" : williamson_gross_rent_percent_data_clean_df["2011"],
                           "Hays County 2012" : hays_gross_income_percent_data_clean_df["2012"],
                           "Travis County 2012" : travis_gross_rent_percent_data_df["2012"],  
                           "Williamson County 2012" : williamson_gross_rent_percent_data_clean_df["2012"],
                           "Hays County 2013" : hays_gross_income_percent_data_clean_df["2013"],
                           "Travis County 2013" : travis_gross_rent_percent_data_df["2013"],  
                           "Williamson County 2013" : williamson_gross_rent_percent_data_clean_df["2013"],
                           "Hays County 2014" : hays_gross_income_percent_data_clean_df["2014"],
                           "Travis County 2014" : travis_gross_rent_percent_data_df["2014"],  
                           "Williamson County 2014" : williamson_gross_rent_percent_data_clean_df["2014"],
                           "Hays County 2015" : hays_gross_income_percent_data_clean_df["2015"],
                           "Travis County 2015" : travis_gross_rent_percent_data_df["2015"],  
                           "Williamson County 2015" : williamson_gross_rent_percent_data_clean_df["2015"],
                           "Hays County 2016" : hays_gross_income_percent_data_clean_df["2016"],
                           "Travis County 2016" : travis_gross_rent_percent_data_df["2016"],  
                           "Williamson County 2016" : williamson_gross_rent_percent_data_clean_df["2016"],
                           
                            
    
}
```


```python
#completed GRAPI combined DF
combined_grapi_df = pd.DataFrame(data_for_combined_grapi_df)
combined_grapi_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Less than 15.0 percent</td>
      <td>1412.0</td>
      <td>1379.0</td>
      <td>1400.0</td>
      <td>848.0</td>
      <td>1776.0</td>
      <td>965.0</td>
      <td>1623.0</td>
      <td>2225.0</td>
      <td>3339.0</td>
      <td>...</td>
      <td>4005.0</td>
      <td>3793.0</td>
      <td>4468.0</td>
      <td>594.0</td>
      <td>4428.0</td>
      <td>7203.0</td>
      <td>5519.0</td>
      <td>6132.0</td>
      <td>4386.0</td>
      <td>6545.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>15.0 to 19.9 percent</td>
      <td>1588.0</td>
      <td>1688.0</td>
      <td>1105.0</td>
      <td>1415.0</td>
      <td>891.0</td>
      <td>1894.0</td>
      <td>2396.0</td>
      <td>2332.0</td>
      <td>968.0</td>
      <td>...</td>
      <td>4624.0</td>
      <td>5536.0</td>
      <td>4581.0</td>
      <td>7828.0</td>
      <td>8098.0</td>
      <td>7633.0</td>
      <td>5782.0</td>
      <td>6329.0</td>
      <td>897.0</td>
      <td>739.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20.0 to 24.9 percent</td>
      <td>1331.0</td>
      <td>1750.0</td>
      <td>1532.0</td>
      <td>1939.0</td>
      <td>951.0</td>
      <td>1181.0</td>
      <td>1124.0</td>
      <td>1653.0</td>
      <td>2763.0</td>
      <td>...</td>
      <td>5145.0</td>
      <td>5502.0</td>
      <td>7021.0</td>
      <td>7425.0</td>
      <td>8742.0</td>
      <td>7381.0</td>
      <td>6763.0</td>
      <td>7653.0</td>
      <td>717.0</td>
      <td>9008.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>25.0 to 29.9 percent</td>
      <td>1750.0</td>
      <td>1702.0</td>
      <td>1345.0</td>
      <td>1828.0</td>
      <td>2449.0</td>
      <td>1742.0</td>
      <td>1536.0</td>
      <td>1712.0</td>
      <td>2463.0</td>
      <td>...</td>
      <td>3908.0</td>
      <td>4852.0</td>
      <td>3755.0</td>
      <td>7791.0</td>
      <td>6789.0</td>
      <td>7948.0</td>
      <td>6036.0</td>
      <td>7638.0</td>
      <td>7948.0</td>
      <td>6373.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>30.0 to 34.9 percent</td>
      <td>1331.0</td>
      <td>1288.0</td>
      <td>550.0</td>
      <td>925.0</td>
      <td>2324.0</td>
      <td>2026.0</td>
      <td>1769.0</td>
      <td>2427.0</td>
      <td>3555.0</td>
      <td>...</td>
      <td>3093.0</td>
      <td>3349.0</td>
      <td>4994.0</td>
      <td>5002.0</td>
      <td>497.0</td>
      <td>4309.0</td>
      <td>5708.0</td>
      <td>4344.0</td>
      <td>4262.0</td>
      <td>6887.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>35.0 percent or more</td>
      <td>6838.0</td>
      <td>7095.0</td>
      <td>8390.0</td>
      <td>8699.0</td>
      <td>10338.0</td>
      <td>10632.0</td>
      <td>11700.0</td>
      <td>12502.0</td>
      <td>10997.0</td>
      <td>...</td>
      <td>11788.0</td>
      <td>11140.0</td>
      <td>12728.0</td>
      <td>16037.0</td>
      <td>18055.0</td>
      <td>15945.0</td>
      <td>17033.0</td>
      <td>19463.0</td>
      <td>16683.0</td>
      <td>16907.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Not computed</td>
      <td>1281.0</td>
      <td>739.0</td>
      <td>1441.0</td>
      <td>1356.0</td>
      <td>1164.0</td>
      <td>1191.0</td>
      <td>840.0</td>
      <td>1701.0</td>
      <td>1944.0</td>
      <td>...</td>
      <td>1162.0</td>
      <td>1995.0</td>
      <td>1196.0</td>
      <td>2118.0</td>
      <td>98.0</td>
      <td>1503.0</td>
      <td>2302.0</td>
      <td>2532.0</td>
      <td>2193.0</td>
      <td>2378.0</td>
    </tr>
  </tbody>
</table>
<p>7 rows × 31 columns</p>
</div>




```python
#prep data for housing tenure
#all the dataframes were cleaned in the source to make them consistent
williamson_tenure_data_clean_df
hays_housing_tenure_data_clean_df
travis_housing_tenure_data_df
None
```


```python
#input all the data for the dataframe
data_for_merged_housing_tenure = { "Austin Housing" : travis_housing_tenure_data_df["HOUSING TENURE"],
                            "Hays County 2007" : hays_housing_tenure_data_clean_df["2007"],
                           "Travis County 2007" : travis_housing_tenure_data_df["2007"],  
                           "Williamson County 2007" : williamson_tenure_data_clean_df["2007"],
                           "Hays County 2008" : hays_housing_tenure_data_clean_df["2008"],
                           "Travis County 2008" : travis_housing_tenure_data_df["2008"],  
                           "Williamson County 2008" : williamson_tenure_data_clean_df["2008"],
                           "Hays County 2009" : hays_housing_tenure_data_clean_df["2009"],
                           "Travis County 2009" : travis_housing_tenure_data_df["2009"],  
                           "Williamson County 2009" : williamson_tenure_data_clean_df["2009"],
                           "Hays County 2010" : hays_housing_tenure_data_clean_df["2010"],
                           "Travis County 2010" : travis_housing_tenure_data_df["2010"],  
                           "Williamson County 2010" : williamson_tenure_data_clean_df["2010"],
                           "Hays County 2011" : hays_housing_tenure_data_clean_df["2011"],
                           "Travis County 2011" : travis_housing_tenure_data_df["2011"],  
                           "Williamson County 2011" : williamson_tenure_data_clean_df["2011"],
                           "Hays County 2012" : hays_housing_tenure_data_clean_df["2012"],
                           "Travis County 2012" : travis_housing_tenure_data_df["2012"],  
                           "Williamson County 2012" : williamson_tenure_data_clean_df["2012"],
                           "Hays County 2013" : hays_housing_tenure_data_clean_df["2013"],
                           "Travis County 2013" : travis_housing_tenure_data_df["2013"],  
                           "Williamson County 2013" : williamson_tenure_data_clean_df["2013"],
                           "Hays County 2014" : hays_housing_tenure_data_clean_df["2014"],
                           "Travis County 2014" : travis_housing_tenure_data_df["2014"],  
                           "Williamson County 2014" : williamson_tenure_data_clean_df["2014"],
                           "Hays County 2015" : hays_housing_tenure_data_clean_df["2015"],
                           "Travis County 2015" : travis_housing_tenure_data_df["2015"],  
                           "Williamson County 2015" : williamson_tenure_data_clean_df["2015"],
                           "Hays County 2016" : hays_housing_tenure_data_clean_df["2016"],
                           "Travis County 2016" : travis_housing_tenure_data_df["2016"],  
                           "Williamson County 2016" : williamson_tenure_data_clean_df["2016"],
                           
                            
    
}
```


```python
#complete the dataframe
complete_merged_housing_tenure_df = pd.DataFrame(data_for_merged_housing_tenure)
complete_merged_housing_tenure_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Occupied housing units</td>
      <td>44803</td>
      <td>47008</td>
      <td>48709</td>
      <td>54422</td>
      <td>56754</td>
      <td>57395</td>
      <td>60739</td>
      <td>63497</td>
      <td>67346</td>
      <td>...</td>
      <td>121899.0</td>
      <td>127791.0</td>
      <td>132981.0</td>
      <td>152739.0</td>
      <td>156738.0</td>
      <td>156215.0</td>
      <td>161887.0</td>
      <td>164805.0</td>
      <td>170987.0</td>
      <td>173125.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Owner-occupied</td>
      <td>29272</td>
      <td>31367</td>
      <td>32946</td>
      <td>37412</td>
      <td>36861</td>
      <td>37764</td>
      <td>39751</td>
      <td>38945</td>
      <td>41317</td>
      <td>...</td>
      <td>88133.0</td>
      <td>91626.0</td>
      <td>94284.0</td>
      <td>100598.0</td>
      <td>104671.0</td>
      <td>104293.0</td>
      <td>112744.0</td>
      <td>110714.0</td>
      <td>119375.0</td>
      <td>117637.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Renter-occupied</td>
      <td>15531</td>
      <td>15641</td>
      <td>15763</td>
      <td>17010</td>
      <td>19893</td>
      <td>19631</td>
      <td>20988</td>
      <td>24552</td>
      <td>26029</td>
      <td>...</td>
      <td>33766.0</td>
      <td>36165.0</td>
      <td>38697.0</td>
      <td>52141.0</td>
      <td>52067.0</td>
      <td>51922.0</td>
      <td>49143.0</td>
      <td>54091.0</td>
      <td>51612.0</td>
      <td>55488.0</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 31 columns</p>
</div>




```python
#collected all the data for the merged SMOC dataframe
data_for_merged_smoc = { "Austin Housing" : williamson_mortgage_clean_df["SELECTED MONTHLY OWNER COSTS (SMOC)"],
                            "Hays County 2007" : hays_monthly_costs_with_mortgage_data_clean_df["2007"],
                           "Travis County 2007" : travis_mortgage_data_df["2007"],  
                           "Williamson County 2007" : williamson_mortgage_clean_df["2007"],
                           "Hays County 2008" : hays_monthly_costs_with_mortgage_data_clean_df["2008"],
                           "Travis County 2008" : travis_mortgage_data_df["2008"],  
                           "Williamson County 2008" : williamson_mortgage_clean_df["2008"],
                           "Hays County 2009" : hays_monthly_costs_with_mortgage_data_clean_df["2009"],
                           "Travis County 2009" : travis_mortgage_data_df["2009"],  
                           "Williamson County 2009" : williamson_mortgage_clean_df["2009"],
                           "Hays County 2010" : hays_monthly_costs_with_mortgage_data_clean_df["2010"],
                           "Travis County 2010" : travis_mortgage_data_df["2010"],  
                           "Williamson County 2010" : williamson_mortgage_clean_df["2010"],
                           "Hays County 2011" : hays_monthly_costs_with_mortgage_data_clean_df["2011"],
                           "Travis County 2011" : travis_mortgage_data_df["2011"],  
                           "Williamson County 2011" : williamson_mortgage_clean_df["2011"],
                           "Hays County 2012" : hays_monthly_costs_with_mortgage_data_clean_df["2012"],
                           "Travis County 2012" : travis_mortgage_data_df["2012"],  
                           "Williamson County 2012" : williamson_mortgage_clean_df["2012"],
                           "Hays County 2013" : hays_monthly_costs_with_mortgage_data_clean_df["2013"],
                           "Travis County 2013" : travis_mortgage_data_df["2013"],  
                           "Williamson County 2013" : williamson_mortgage_clean_df["2013"],
                           "Hays County 2014" : hays_monthly_costs_with_mortgage_data_clean_df["2014"],
                           "Travis County 2014" : travis_mortgage_data_df["2014"],  
                           "Williamson County 2014" : williamson_mortgage_clean_df["2014"],
                           "Hays County 2015" : hays_monthly_costs_with_mortgage_data_clean_df["2015"],
                           "Travis County 2015" : travis_mortgage_data_df["2015"],  
                           "Williamson County 2015" : williamson_mortgage_clean_df["2015"],
                           "Hays County 2016" : hays_monthly_costs_with_mortgage_data_clean_df["2016"],
                           "Travis County 2016" : travis_mortgage_data_df["2016"],  
                           "Williamson County 2016" : williamson_mortgage_clean_df["2016"],
                           
                            
    
}
```


```python
completed_merged_smoc_df = pd.DataFrame(data_for_merged_smoc)
completed_merged_smoc_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Housing units with a mortgage</td>
      <td>20947</td>
      <td>22107</td>
      <td>24425</td>
      <td>27063</td>
      <td>27404</td>
      <td>28555</td>
      <td>27811</td>
      <td>27216</td>
      <td>28943</td>
      <td>...</td>
      <td>67646.0</td>
      <td>70176.0</td>
      <td>74115.0</td>
      <td>79934.0</td>
      <td>80318.0</td>
      <td>80830.0</td>
      <td>82526.0</td>
      <td>80534.0</td>
      <td>86936.0</td>
      <td>87071.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Less than $500</td>
      <td>139</td>
      <td>271</td>
      <td>332</td>
      <td>294</td>
      <td>96</td>
      <td>51</td>
      <td>655</td>
      <td>268</td>
      <td>73</td>
      <td>...</td>
      <td>319.0</td>
      <td>409.0</td>
      <td>378.0</td>
      <td>499.0</td>
      <td>394.0</td>
      <td>297.0</td>
      <td>1308.0</td>
      <td>1156.0</td>
      <td>493.0</td>
      <td>106.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$500 to $999</td>
      <td>2260</td>
      <td>2283</td>
      <td>2167</td>
      <td>3589</td>
      <td>5947</td>
      <td>3062</td>
      <td>2689</td>
      <td>3750</td>
      <td>3406</td>
      <td>...</td>
      <td>5970.0</td>
      <td>5701.0</td>
      <td>5729.0</td>
      <td>6034.0</td>
      <td>7335.0</td>
      <td>6810.0</td>
      <td>7003.0</td>
      <td>6287.0</td>
      <td>5192.0</td>
      <td>6148.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$1,000 to $1,499</td>
      <td>8604</td>
      <td>7399</td>
      <td>9808</td>
      <td>9107</td>
      <td>8765</td>
      <td>10693</td>
      <td>10154</td>
      <td>8126</td>
      <td>8669</td>
      <td>...</td>
      <td>25157.0</td>
      <td>23247.0</td>
      <td>25859.0</td>
      <td>27209.0</td>
      <td>26638.0</td>
      <td>28615.0</td>
      <td>29006.0</td>
      <td>27652.0</td>
      <td>28518.0</td>
      <td>24479.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$1,500 to $1,999</td>
      <td>5400</td>
      <td>6346</td>
      <td>5975</td>
      <td>6963</td>
      <td>5147</td>
      <td>7034</td>
      <td>7539</td>
      <td>7914</td>
      <td>8162</td>
      <td>...</td>
      <td>20153.0</td>
      <td>23204.0</td>
      <td>23923.0</td>
      <td>25597.0</td>
      <td>22632.0</td>
      <td>25270.0</td>
      <td>26817.0</td>
      <td>23770.0</td>
      <td>26355.0</td>
      <td>26599.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$2000 or more</td>
      <td>4544</td>
      <td>5808</td>
      <td>6143</td>
      <td>7110</td>
      <td>7449</td>
      <td>7715</td>
      <td>6774</td>
      <td>7158</td>
      <td>8635</td>
      <td>...</td>
      <td>16047.0</td>
      <td>17615.0</td>
      <td>18226.0</td>
      <td>20595.0</td>
      <td>23319.0</td>
      <td>19838.0</td>
      <td>18392.0</td>
      <td>21669.0</td>
      <td>26378.0</td>
      <td>29739.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Median (dollars)</td>
      <td>1473</td>
      <td>1567</td>
      <td>1496</td>
      <td>1531</td>
      <td>1440</td>
      <td>1536</td>
      <td>1526</td>
      <td>1570</td>
      <td>1601</td>
      <td>...</td>
      <td>1553.0</td>
      <td>1605.0</td>
      <td>1588.0</td>
      <td>1600.0</td>
      <td>1612.0</td>
      <td>1581.0</td>
      <td>1566.0</td>
      <td>1602.0</td>
      <td>1646.0</td>
      <td>1702.0</td>
    </tr>
  </tbody>
</table>
<p>7 rows × 31 columns</p>
</div>




```python
#gather all the data for housing values
#prep it for making a dataframe
data_for_housing_value_df = { "Austin Housing" : hays_housing_value_data_clean_df["VALUE"],
                            "Hays County 2007" : hays_housing_value_data_clean_df["2007"],
                           "Travis County 2007" : travis_housing_value_data_df["2007"],  
                           "Williamson County 2007" : williamson_value_data_drop_pd["2007"],
                           "Hays County 2008" : hays_housing_value_data_clean_df["2008"],
                           "Travis County 2008" : travis_housing_value_data_df["2008"],  
                           "Williamson County 2008" : williamson_value_data_drop_pd["2008"],
                           "Hays County 2009" : hays_housing_value_data_clean_df["2009"],
                           "Travis County 2009" : travis_housing_value_data_df["2009"],  
                           "Williamson County 2009" : williamson_value_data_drop_pd["2009"],
                           "Hays County 2010" : hays_housing_value_data_clean_df["2010"],
                           "Travis County 2010" : travis_housing_value_data_df["2010"],  
                           "Williamson County 2010" : williamson_value_data_drop_pd["2010"],
                           "Hays County 2011" : hays_housing_value_data_clean_df["2011"],
                           "Travis County 2011" : travis_housing_value_data_df["2011"],  
                           "Williamson County 2011" : williamson_value_data_drop_pd["2011"],
                           "Hays County 2012" : hays_housing_value_data_clean_df["2012"],
                           "Travis County 2012" : travis_housing_value_data_df["2012"],  
                           "Williamson County 2012" : williamson_value_data_drop_pd["2012"],
                           "Hays County 2013" : hays_housing_value_data_clean_df["2013"],
                           "Travis County 2013" : travis_housing_value_data_df["2013"],  
                           "Williamson County 2013" : williamson_value_data_drop_pd["2013"],
                           "Hays County 2014" : hays_housing_value_data_clean_df["2014"],
                           "Travis County 2014" : travis_housing_value_data_df["2014"],  
                           "Williamson County 2014" : williamson_value_data_drop_pd["2014"],
                           "Hays County 2015" : hays_housing_value_data_clean_df["2015"],
                           "Travis County 2015" : travis_housing_value_data_df["2015"],  
                           "Williamson County 2015" : williamson_value_data_drop_pd["2015"],
                           "Hays County 2016" : hays_housing_value_data_clean_df["2016"],
                           "Travis County 2016" : travis_housing_value_data_df["2016"],  
                           "Williamson County 2016" : williamson_value_data_drop_pd["2016"],
                           
                            
    
}
```


```python
#make a completed data frame
completed_housing_value_df = pd.DataFrame(data_for_housing_value_df)
completed_housing_value_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Less than $50,000</td>
      <td>1062.0</td>
      <td>2161.0</td>
      <td>2037.0</td>
      <td>2798.0</td>
      <td>3161.0</td>
      <td>1890.0</td>
      <td>2824.0</td>
      <td>2761.0</td>
      <td>1763.0</td>
      <td>...</td>
      <td>1763</td>
      <td>2565</td>
      <td>2733</td>
      <td>3893</td>
      <td>3541</td>
      <td>3281</td>
      <td>5114</td>
      <td>3525</td>
      <td>2079</td>
      <td>4183</td>
    </tr>
    <tr>
      <th>1</th>
      <td>$50,000 to $99,999</td>
      <td>3320.0</td>
      <td>3454.0</td>
      <td>3141.0</td>
      <td>3480.0</td>
      <td>4623.0</td>
      <td>3561.0</td>
      <td>4083.0</td>
      <td>4517.0</td>
      <td>3568.0</td>
      <td>...</td>
      <td>6084</td>
      <td>6047</td>
      <td>6314</td>
      <td>5020</td>
      <td>6056</td>
      <td>5492</td>
      <td>5593</td>
      <td>4257</td>
      <td>4461</td>
      <td>3354</td>
    </tr>
    <tr>
      <th>2</th>
      <td>$100,000 to $149,999</td>
      <td>6025.0</td>
      <td>7137.0</td>
      <td>7456.0</td>
      <td>6731.0</td>
      <td>8187.0</td>
      <td>8340.0</td>
      <td>7196.0</td>
      <td>5834.0</td>
      <td>5492.0</td>
      <td>...</td>
      <td>25041</td>
      <td>20707</td>
      <td>22617</td>
      <td>25226</td>
      <td>24827</td>
      <td>24574</td>
      <td>24154</td>
      <td>16800</td>
      <td>13429</td>
      <td>10088</td>
    </tr>
    <tr>
      <th>3</th>
      <td>$150,000 to $199,999</td>
      <td>6552.0</td>
      <td>6256.0</td>
      <td>7051.0</td>
      <td>9435.0</td>
      <td>7831.0</td>
      <td>7780.0</td>
      <td>6717.0</td>
      <td>8985.0</td>
      <td>9395.0</td>
      <td>...</td>
      <td>25401</td>
      <td>26022</td>
      <td>25539</td>
      <td>26508</td>
      <td>28556</td>
      <td>27683</td>
      <td>26892</td>
      <td>25324</td>
      <td>26434</td>
      <td>19907</td>
    </tr>
    <tr>
      <th>4</th>
      <td>$200,000 to $299,999</td>
      <td>6124.0</td>
      <td>5851.0</td>
      <td>5792.0</td>
      <td>7197.0</td>
      <td>6447.0</td>
      <td>7208.0</td>
      <td>10254.0</td>
      <td>7926.0</td>
      <td>9328.0</td>
      <td>...</td>
      <td>19839</td>
      <td>22815</td>
      <td>24125</td>
      <td>26565</td>
      <td>26446</td>
      <td>30458</td>
      <td>31215</td>
      <td>36233</td>
      <td>41354</td>
      <td>42681</td>
    </tr>
    <tr>
      <th>5</th>
      <td>$300,000 to $499,999</td>
      <td>4692.0</td>
      <td>4852.0</td>
      <td>4911.0</td>
      <td>5598.0</td>
      <td>5432.0</td>
      <td>6930.0</td>
      <td>6237.0</td>
      <td>6478.0</td>
      <td>8889.0</td>
      <td>...</td>
      <td>9082</td>
      <td>11270</td>
      <td>9989</td>
      <td>11277</td>
      <td>13437</td>
      <td>10685</td>
      <td>16979</td>
      <td>21087</td>
      <td>25538</td>
      <td>31510</td>
    </tr>
    <tr>
      <th>6</th>
      <td>$500,000 to $999,999</td>
      <td>1103.0</td>
      <td>1314.0</td>
      <td>1489.0</td>
      <td>1784.0</td>
      <td>1133.0</td>
      <td>1595.0</td>
      <td>1810.0</td>
      <td>2126.0</td>
      <td>2465.0</td>
      <td>...</td>
      <td>970</td>
      <td>1833</td>
      <td>2544</td>
      <td>1891</td>
      <td>1632</td>
      <td>1797</td>
      <td>2202</td>
      <td>2863</td>
      <td>5391</td>
      <td>5423</td>
    </tr>
    <tr>
      <th>7</th>
      <td>$1,000,000 or more</td>
      <td>394.0</td>
      <td>342.0</td>
      <td>1069.0</td>
      <td>389.0</td>
      <td>47.0</td>
      <td>460.0</td>
      <td>630.0</td>
      <td>318.0</td>
      <td>417.0</td>
      <td>...</td>
      <td>265</td>
      <td>367</td>
      <td>471</td>
      <td>218</td>
      <td>176</td>
      <td>323</td>
      <td>595</td>
      <td>625</td>
      <td>689</td>
      <td>491</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Median (dollars)</td>
      <td>174600.0</td>
      <td>170200.0</td>
      <td>172600.0</td>
      <td>178500.0</td>
      <td>162300.0</td>
      <td>178900.0</td>
      <td>191400.0</td>
      <td>183400.0</td>
      <td>203900.0</td>
      <td>...</td>
      <td>176700</td>
      <td>178400</td>
      <td>175300</td>
      <td>175100</td>
      <td>176500</td>
      <td>179600</td>
      <td>187900</td>
      <td>212300</td>
      <td>227000</td>
      <td>242000</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 31 columns</p>
</div>



# % Income Spent on Housing


```python
#gather data for smocapi dataframe
#cleaned a bunch of the source data to make the rows more consistent
data_for_smocapi_df = { "Austin Housing" : williamson_SMOCAPI_data_clean_df["SELECTED MONTHLY OWNER COSTS AS A PERCENTAGE OF HOUSEHOLD INCOME (SMOCAPI)"],
                            "Hays County 2007" : hays_income_percent_with_mortgage_data_clean_df["2007"],
                           "Travis County 2007" : travis_income_percent_data_df["2007"],  
                           "Williamson County 2007" : williamson_SMOCAPI_data_clean_df["2007"],
                           "Hays County 2008" : hays_income_percent_with_mortgage_data_clean_df["2008"],
                           "Williamson County 2008" : williamson_SMOCAPI_data_clean_df["2008"],
                           "Hays County 2009" : hays_income_percent_with_mortgage_data_clean_df["2009"],
                           "Travis County 2009" : travis_income_percent_data_df["2009"],  
                           "Williamson County 2009" : williamson_SMOCAPI_data_clean_df["2009"],
                           "Hays County 2010" : hays_income_percent_with_mortgage_data_clean_df["2010"],
                           "Travis County 2010" : travis_income_percent_data_df["2010"],  
                           "Williamson County 2010" : williamson_SMOCAPI_data_clean_df["2010"],
                           "Hays County 2011" : hays_income_percent_with_mortgage_data_clean_df["2011"],
                           "Travis County 2011" : travis_income_percent_data_df["2011"],  
                           "Williamson County 2011" : williamson_SMOCAPI_data_clean_df["2011"],
                           "Hays County 2012" : hays_income_percent_with_mortgage_data_clean_df["2012"],
                           "Travis County 2012" : travis_income_percent_data_df["2012"],  
                           "Williamson County 2012" : williamson_SMOCAPI_data_clean_df["2012"],
                           "Hays County 2013" : hays_income_percent_with_mortgage_data_clean_df["2013"],
                           "Travis County 2013" : travis_income_percent_data_df["2013"],  
                           "Williamson County 2013" : williamson_SMOCAPI_data_clean_df["2013"],
                           "Hays County 2014" : hays_income_percent_with_mortgage_data_clean_df["2014"],
                           "Travis County 2014" : travis_income_percent_data_df["2014"],  
                           "Williamson County 2014" : williamson_SMOCAPI_data_clean_df["2014"],
                           "Hays County 2015" : hays_income_percent_with_mortgage_data_clean_df["2015"],
                           "Travis County 2015" : travis_income_percent_data_df["2015"],  
                           "Williamson County 2015" : williamson_SMOCAPI_data_clean_df["2015"],
                           "Hays County 2016" : hays_income_percent_with_mortgage_data_clean_df["2016"],
                           "Travis County 2016" : travis_income_percent_data_df["2016"],  
                           "Williamson County 2016" : williamson_SMOCAPI_data_clean_df["2016"],
                           
                            
    
}
```


```python
#completed the smocapi df
completed_smocapi_df = pd.DataFrame(data_for_smocapi_df)
completed_smocapi_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Austin Housing</th>
      <th>Hays County 2007</th>
      <th>Hays County 2008</th>
      <th>Hays County 2009</th>
      <th>Hays County 2010</th>
      <th>Hays County 2011</th>
      <th>Hays County 2012</th>
      <th>Hays County 2013</th>
      <th>Hays County 2014</th>
      <th>Hays County 2015</th>
      <th>...</th>
      <th>Williamson County 2007</th>
      <th>Williamson County 2008</th>
      <th>Williamson County 2009</th>
      <th>Williamson County 2010</th>
      <th>Williamson County 2011</th>
      <th>Williamson County 2012</th>
      <th>Williamson County 2013</th>
      <th>Williamson County 2014</th>
      <th>Williamson County 2015</th>
      <th>Williamson County 2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Housing units with a mortgage (excluding units...</td>
      <td>20947.0</td>
      <td>22107.0</td>
      <td>24412.0</td>
      <td>27013.0</td>
      <td>27318.0</td>
      <td>28491.0</td>
      <td>27748.0</td>
      <td>27182.0</td>
      <td>28943.0</td>
      <td>...</td>
      <td>70353.0</td>
      <td>72583.0</td>
      <td>73991.0</td>
      <td>79569.0</td>
      <td>80151.0</td>
      <td>80473.0</td>
      <td>82188.0</td>
      <td>80138.0</td>
      <td>86686.0</td>
      <td>86854.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Less than 20.0 percent</td>
      <td>7826.0</td>
      <td>7307.0</td>
      <td>8937.0</td>
      <td>10072.0</td>
      <td>10524.0</td>
      <td>10559.0</td>
      <td>11259.0</td>
      <td>10886.0</td>
      <td>11060.0</td>
      <td>...</td>
      <td>23850.0</td>
      <td>25477.0</td>
      <td>28635.0</td>
      <td>27862.0</td>
      <td>26900.0</td>
      <td>30590.0</td>
      <td>37663.0</td>
      <td>35481.0</td>
      <td>39895.0</td>
      <td>41219.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20.0 to 24.9 percent</td>
      <td>3908.0</td>
      <td>3878.0</td>
      <td>4258.0</td>
      <td>4970.0</td>
      <td>3397.0</td>
      <td>3332.0</td>
      <td>4316.0</td>
      <td>5751.0</td>
      <td>5570.0</td>
      <td>...</td>
      <td>14774.0</td>
      <td>15097.0</td>
      <td>13244.0</td>
      <td>15416.0</td>
      <td>19326.0</td>
      <td>17255.0</td>
      <td>16619.0</td>
      <td>16429.0</td>
      <td>15725.0</td>
      <td>16289.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>25.0 to 29.9 percent</td>
      <td>2316.0</td>
      <td>2480.0</td>
      <td>3015.0</td>
      <td>3048.0</td>
      <td>2753.0</td>
      <td>4129.0</td>
      <td>3739.0</td>
      <td>4103.0</td>
      <td>3838.0</td>
      <td>...</td>
      <td>11468.0</td>
      <td>9073.0</td>
      <td>9841.0</td>
      <td>11338.0</td>
      <td>10395.0</td>
      <td>9341.0</td>
      <td>8742.0</td>
      <td>10239.0</td>
      <td>11246.0</td>
      <td>8600.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>30.0 to 34.9 percent</td>
      <td>1888.0</td>
      <td>2193.0</td>
      <td>1697.0</td>
      <td>3236.0</td>
      <td>2556.0</td>
      <td>3246.0</td>
      <td>1590.0</td>
      <td>1725.0</td>
      <td>2203.0</td>
      <td>...</td>
      <td>7035.0</td>
      <td>6242.0</td>
      <td>6659.0</td>
      <td>8454.0</td>
      <td>8237.0</td>
      <td>7703.0</td>
      <td>5551.0</td>
      <td>4291.0</td>
      <td>5789.0</td>
      <td>5445.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>35.0 percent or more</td>
      <td>5009.0</td>
      <td>6249.0</td>
      <td>6505.0</td>
      <td>5687.0</td>
      <td>8088.0</td>
      <td>7225.0</td>
      <td>6844.0</td>
      <td>4717.0</td>
      <td>6272.0</td>
      <td>...</td>
      <td>13297.0</td>
      <td>16622.0</td>
      <td>15834.0</td>
      <td>16499.0</td>
      <td>15293.0</td>
      <td>15584.0</td>
      <td>13613.0</td>
      <td>13698.0</td>
      <td>14031.0</td>
      <td>15301.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Not computed</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>13.0</td>
      <td>50.0</td>
      <td>86.0</td>
      <td>64.0</td>
      <td>63.0</td>
      <td>34.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>140.0</td>
      <td>433.0</td>
      <td>181.0</td>
      <td>365.0</td>
      <td>167.0</td>
      <td>357.0</td>
      <td>338.0</td>
      <td>396.0</td>
      <td>250.0</td>
      <td>217.0</td>
    </tr>
  </tbody>
</table>
<p>7 rows × 30 columns</p>
</div>




```python
labels = ["Less than 20%", "20% - 25%", "25% - 30%", "30% - 35%","35% - 40%","Not Computed"]
```


```python
plt.pie(completed_smocapi_df["Hays County 2007"][1:],labels=labels, startangle=90,autopct='%1.1f%%',colors = ["yellowgreen", "blue", "Violet","pink","coral","red"])
plt.axis("equal")    
plt.title(s="% Spent on rent Hays 2007")
```




    <matplotlib.text.Text at 0x2aa338a9f98>




```python
plt.savefig("Saved_Pngs/morgage_percent_hays_2007.png")
```


```python
plt.show()
```


![png](output_38_0.png)



```python
plt.pie(completed_smocapi_df["Hays County 2016"][1:],labels=labels, startangle=90,autopct='%1.1f%%',colors = ["yellowgreen", "blue", "Violet","pink","coral","red"])
plt.axis("equal")    
plt.title(s="% Spent on rent Hays 2016")
```




    <matplotlib.text.Text at 0x2aa3398d6a0>




```python
plt.savefig("Saved_Pngs/morgage_percent_hays_2016.png")
```


```python
plt.show()
```


![png](output_41_0.png)



```python
plt.pie(completed_smocapi_df["Travis County 2007"][1:],labels=labels, startangle=90,autopct='%1.1f%%',colors = ["yellowgreen", "blue", "Violet","pink","coral","red"])
plt.axis("equal")    
plt.title(s="% Spent on rent Travis 2007")
```




    <matplotlib.text.Text at 0x2aa33d6aac8>




```python
plt.savefig("Saved_Pngs/morgage_percent_travis_2007.png")
```


```python
plt.show()
```


![png](output_44_0.png)



```python
plt.pie(completed_smocapi_df["Travis County 2016"][1:],labels=labels, startangle=90,autopct='%1.1f%%',colors = ["yellowgreen", "blue", "Violet","pink","coral","red"])
plt.axis("equal")    
plt.title(s="% Spent on rent Travis 2016")
```




    <matplotlib.text.Text at 0x2aa33e121d0>




```python
plt.savefig("Saved_Pngs/morgage_percent_travis_2016.png")
```


```python
plt.show()
```


![png](output_47_0.png)



```python
plt.pie(completed_smocapi_df["Williamson County 2007"][1:],labels=labels, startangle=90,autopct='%1.1f%%',colors = ["yellowgreen", "blue", "Violet","pink","coral","red"])
plt.axis("equal")    
plt.title(s="% Spent on rent Williamson 2007")
```




    <matplotlib.text.Text at 0x2aa33eb7c18>




```python
plt.savefig("Saved_Pngs/morgage_percent_williamson_2007.png")
```


```python
plt.show()
```


![png](output_50_0.png)



```python
plt.pie(completed_smocapi_df["Williamson County 2016"][1:],labels=labels, startangle=90,autopct='%1.1f%%',colors = ["yellowgreen", "blue", "Violet","pink","coral","red"])
plt.axis("equal")    
plt.title(s="% Spent on rent Williamson 2016")
```




    <matplotlib.text.Text at 0x2aa33f67828>




```python
plt.savefig("Saved_Pngs/morgage_percent_williamson_2016.png")
```


```python
plt.show()
```


![png](output_53_0.png)


# Rent vs. Own


```python
#get data from previous notebook for consistency
travis_housing_tenure = "Travis_County_Data/Housing_Tenure.csv"
williamson_tenure = "williamson_data/williamson_tenure.csv"
hays_housing_tenure = "hays_data/hays_housing_tenure.csv"

hays_housing_tenure_data_df = pd.read_csv(hays_housing_tenure,thousands = ",")
travis_housing_tenure_data_df = pd.read_csv(travis_housing_tenure)
williamson_tenure_data_df = pd.read_csv(williamson_tenure,sep='\t',thousands = ",")

hays_housing_tenure_data_clean_df = hays_housing_tenure_data_df.dropna(how = "any")
williamson_tenure_data_clean_df = williamson_tenure_data_df.dropna(how = "any")
```


```python
#hays_owners
owned_hays = hays_housing_tenure_data_df.drop([0,2])
owned_hays
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HOUSING TENURE</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Owner-occupied</td>
      <td>27106</td>
      <td>29272</td>
      <td>31367</td>
      <td>32946</td>
      <td>37412</td>
      <td>36861</td>
      <td>37764</td>
      <td>39751</td>
      <td>38945</td>
      <td>41317</td>
      <td>43597</td>
    </tr>
  </tbody>
</table>
</div>




```python
#hays renters
rented_hays = hays_housing_tenure_data_df.drop([0,1])
rented_hays
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HOUSING TENURE</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Renter-occupied</td>
      <td>15444</td>
      <td>15531</td>
      <td>15641</td>
      <td>15763</td>
      <td>17010</td>
      <td>19893</td>
      <td>19631</td>
      <td>20988</td>
      <td>24552</td>
      <td>26029</td>
      <td>27670</td>
    </tr>
  </tbody>
</table>
</div>




```python
#travis county owned
owned_travis = travis_housing_tenure_data_df.drop([0,2])
owned_travis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HOUSING TENURE</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Owner-occupied</td>
      <td>198701</td>
      <td>199550</td>
      <td>206170</td>
      <td>207109</td>
      <td>206912</td>
      <td>205261</td>
      <td>213091</td>
      <td>221657</td>
      <td>223202</td>
      <td>227913</td>
      <td>236286</td>
    </tr>
  </tbody>
</table>
</div>




```python
#travis county rented
rented_travis = travis_housing_tenure_data_df.drop([0,1])
rented_travis
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HOUSING TENURE</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Renter-occupied</td>
      <td>168083</td>
      <td>169028</td>
      <td>175137</td>
      <td>184480</td>
      <td>196726</td>
      <td>205422</td>
      <td>201227</td>
      <td>207232</td>
      <td>214173</td>
      <td>218429</td>
      <td>221524</td>
    </tr>
  </tbody>
</table>
</div>




```python
#williamson county owned
owned_williamson = williamson_tenure_data_clean_df.drop([0,2])
owned_williamson
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HOUSING TENURE</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Owner-occupied</td>
      <td>88133.0</td>
      <td>91626.0</td>
      <td>94284.0</td>
      <td>100598.0</td>
      <td>104671.0</td>
      <td>104293.0</td>
      <td>112744.0</td>
      <td>110714.0</td>
      <td>119375.0</td>
      <td>117637.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#williamson county rented
rented_williamson = williamson_tenure_data_clean_df.drop([0,1])
rented_williamson
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>HOUSING TENURE</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Renter-occupied</td>
      <td>33766.0</td>
      <td>36165.0</td>
      <td>38697.0</td>
      <td>52141.0</td>
      <td>52067.0</td>
      <td>51922.0</td>
      <td>49143.0</td>
      <td>54091.0</td>
      <td>51612.0</td>
      <td>55488.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#total owned dataframe
total_owned = pd.concat([owned_travis,owned_williamson,owned_hays], ignore_index = True)
total_owned = total_owned.drop(["2006","HOUSING TENURE"], axis = 1) 
total_owned
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>199550.0</td>
      <td>206170.0</td>
      <td>207109.0</td>
      <td>206912.0</td>
      <td>205261.0</td>
      <td>213091.0</td>
      <td>221657.0</td>
      <td>223202.0</td>
      <td>227913.0</td>
      <td>236286.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>88133.0</td>
      <td>91626.0</td>
      <td>94284.0</td>
      <td>100598.0</td>
      <td>104671.0</td>
      <td>104293.0</td>
      <td>112744.0</td>
      <td>110714.0</td>
      <td>119375.0</td>
      <td>117637.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>29272.0</td>
      <td>31367.0</td>
      <td>32946.0</td>
      <td>37412.0</td>
      <td>36861.0</td>
      <td>37764.0</td>
      <td>39751.0</td>
      <td>38945.0</td>
      <td>41317.0</td>
      <td>43597.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#get sums of owned for plotting
owned_sums = total_owned.sum(axis = 0)
owned_sums
```




    2007    316955.0
    2008    329163.0
    2009    334339.0
    2010    344922.0
    2011    346793.0
    2012    355148.0
    2013    374152.0
    2014    372861.0
    2015    388605.0
    2016    397520.0
    dtype: float64




```python
#total rented dataframe
total_rented = pd.concat([rented_travis,rented_williamson,rented_hays], ignore_index = True)
total_rented = total_rented.drop(["2006","HOUSING TENURE"], axis = 1) 
total_rented
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>169028.0</td>
      <td>175137.0</td>
      <td>184480.0</td>
      <td>196726.0</td>
      <td>205422.0</td>
      <td>201227.0</td>
      <td>207232.0</td>
      <td>214173.0</td>
      <td>218429.0</td>
      <td>221524.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33766.0</td>
      <td>36165.0</td>
      <td>38697.0</td>
      <td>52141.0</td>
      <td>52067.0</td>
      <td>51922.0</td>
      <td>49143.0</td>
      <td>54091.0</td>
      <td>51612.0</td>
      <td>55488.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15531.0</td>
      <td>15641.0</td>
      <td>15763.0</td>
      <td>17010.0</td>
      <td>19893.0</td>
      <td>19631.0</td>
      <td>20988.0</td>
      <td>24552.0</td>
      <td>26029.0</td>
      <td>27670.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#get sums of rented for plotting
rented_sums = total_rented.sum(axis = 0)
rented_sums
```




    2007    218325.0
    2008    226943.0
    2009    238940.0
    2010    265877.0
    2011    277382.0
    2012    272780.0
    2013    277363.0
    2014    292816.0
    2015    296070.0
    2016    304682.0
    dtype: float64




```python
total_owned_data = owned_sums.values
total_rented_data = rented_sums.values
x_axis = np.arange(len(total_owned_data))
```


```python
ax1 = plt.bar(x_axis, total_rented_data, color = "r")
ax2 = plt.bar(x_axis, total_owned_data, bottom = total_rented_data, color = "b")
```


```python
for r1, r2 in zip(ax1, ax2):
    h1 = r1.get_height()
    h2 = r2.get_height()
    plt.text(r1.get_x() + r1.get_width() / 2., h1 / 2., "%d" % h1, ha="center", va="bottom", color="black", fontsize=6, fontweight="bold")
    plt.text(r2.get_x() + r2.get_width() / 2., h1 + h2 / 2., "%d" % h2, ha="center", va="bottom", color="black", fontsize=6, fontweight="bold")
```


```python
plt.xticks(x_axis, ["2007","2008","2009","2010","2011","2012","2013","2014","2015","2016"])
plt.ylim(0,775000,100000)
plt.xlabel("Year")
plt.ylabel("Number of Housing Units")
plt.title("Rent Vs Owned in Austin")
```




    <matplotlib.text.Text at 0x2aa340ec6a0>




```python
#for legend
red_patch = mpatches.Patch(color = "r", label = "Rented")
blue_patch = mpatches.Patch(color = "b", label = "Owned")
plt.legend(handles = [blue_patch,red_patch], loc = "best")
```




    <matplotlib.legend.Legend at 0x2aa341abe48>




```python
plt.savefig("Saved_Pngs/rented_vs_owned.png")
```


```python
plt.show()
```


![png](output_72_0.png)


# Per Capita Income vs. House Costs 


```python
house_value_income = "avg_house_cost_income_merged.csv"
house_value_income_data = pd.read_csv(house_value_income)
house_value_income_data
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>VALUE</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Median (dollars)</td>
      <td>182133.00000</td>
      <td>180400.00000</td>
      <td>184833.00000</td>
      <td>189233.00000</td>
      <td>185567.00000</td>
      <td>192033.00000</td>
      <td>203667.00000</td>
      <td>213767</td>
      <td>236000.00000</td>
      <td>256200.00000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Per capita personal income (dollars) 2/</td>
      <td>37399.33333</td>
      <td>39213.66667</td>
      <td>36980.33333</td>
      <td>37788.66667</td>
      <td>40167.33333</td>
      <td>41676.66667</td>
      <td>42026.66667</td>
      <td>44571</td>
      <td>46901.66667</td>
      <td>47430.33333</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Set the 'Country Code' to be our index for easy referencing of rows
house_value_income_data = house_value_income_data.set_index("VALUE")

years = np.array([2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016])
years

# Plot the world average as a line chart
median, = plt.plot(years, house_value_income_data.loc["Median (dollars)"], color="red", label="Average House Cost" )

# Plot the unemployment values for a single country
income, = plt.plot(years, house_value_income_data.loc["Per capita personal income (dollars) 2/"], color="green",label="Per Capita Personal Income")

# Create a legend for our chart
plt.legend(handles=[median, income], loc="best")
plt.title("Austin Housing Costs vs. Per Capita Income")
plt.ylabel("Dollars ($)")
plt.xlabel("Year")
plt.savefig("Saved_Pngs/percapita_vs_value.png")

# Show the chart
plt.show()
```


```python
years = np.array([2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016])
years
```




    array([2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016])




```python
# Plot the world average as a line chart
median, = plt.plot(years, house_value_income_data.loc["Median (dollars)"], color="blue", label="Average House Cost" )

# Plot the unemployment values for a single country
income, = plt.plot(years, house_value_income_data.loc["Per capita personal income (dollars) 2/"], color="green",label="Per Capita Personal Income")

# Create a legend for our chart
plt.legend(handles=[median, income], loc="best")
plt.title("Austin Housing Costs vs. Per Capita Income")
plt.ylabel("Dollars ($)")
plt.xlabel("Year")
plt.savefig("Saved_Pngs/percapita_vs_value.png")

# Show the chart
plt.show()
```


![png](output_77_0.png)



```python
# Add dual axes
fig, ax1 = plt.subplots()

ax2 = ax1.twinx()
ax2.plot(years, house_value_income_data.loc["Median (dollars)"], 'b-')
ax1.plot(years, house_value_income_data.loc["Per capita personal income (dollars) 2/"], 'g-')

ax1.set_xlabel('Year')
ax2.set_ylabel('Average House Cost ($)', color='b')
ax1.set_ylabel('Per Capita Personal Income ($)', color='g')
plt.legend(handles=[income, median], loc="best")

plt.show()
```


![png](output_78_0.png)



```python
house_cost_mean = house_value_income_data.loc["Median (dollars)"].mean()
personal_income_mean = house_value_income_data.loc["Per capita personal income (dollars) 2/"].mean()
print(house_cost_mean)
print(personal_income_mean)
```

    202383.3
    41415.566667
    


```python
stats.pearsonr(house_value_income_data.loc["Median (dollars)"], house_value_income_data.loc["Per capita personal income (dollars) 2/"])
```




    (0.92551980858672023, 0.00012296653685145147)



# Population vs House Costs


```python
population_2007_data_df_drop = population_2007_data_df.drop(population_2007_data_df.index[0])
population_2007_data_df_drop


pop_2007_final = population_2007_data_df_drop.rename(index=str, columns={"HD01_VD01": "2007"})
pop_2007_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO.id</th>
      <th>GEO.id2</th>
      <th>GEO.display-label</th>
      <th>2007</th>
      <th>HD02_VD01</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0500000US48209</td>
      <td>48209</td>
      <td>Hays County, Texas</td>
      <td>141480</td>
      <td>*****</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0500000US48453</td>
      <td>48453</td>
      <td>Travis County, Texas</td>
      <td>974365</td>
      <td>*****</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0500000US48491</td>
      <td>48491</td>
      <td>Williamson County, Texas</td>
      <td>373363</td>
      <td>*****</td>
    </tr>
  </tbody>
</table>
</div>




```python
population_2008_data_df_drop = population_2008_data_df.drop(population_2008_data_df.index[0])
population_2008_data_df_drop

pop_2008_final = population_2008_data_df_drop.rename(index=str, columns={"HD01_VD01": "2008"})
pop_2008_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO.id</th>
      <th>GEO.id2</th>
      <th>GEO.display-label</th>
      <th>2008</th>
      <th>HD02_VD01</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0500000US48209</td>
      <td>48209</td>
      <td>Hays County, Texas</td>
      <td>149476</td>
      <td>*****</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0500000US48453</td>
      <td>48453</td>
      <td>Travis County, Texas</td>
      <td>998543</td>
      <td>*****</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0500000US48491</td>
      <td>48491</td>
      <td>Williamson County, Texas</td>
      <td>394193</td>
      <td>*****</td>
    </tr>
  </tbody>
</table>
</div>




```python
population_2009_data_df_drop = population_2009_data_df.drop(population_2009_data_df.index[0])
population_2009_data_df_drop

pop_2009_final = population_2009_data_df_drop.rename(index=str, columns={"HD01_VD01": "2009"})
pop_2009_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO.id</th>
      <th>GEO.id2</th>
      <th>GEO.display-label</th>
      <th>2009</th>
      <th>HD02_VD01</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0500000US48209</td>
      <td>48209</td>
      <td>Hays County, Texas</td>
      <td>155545</td>
      <td>*****</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0500000US48453</td>
      <td>48453</td>
      <td>Travis County, Texas</td>
      <td>1026158</td>
      <td>*****</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0500000US48491</td>
      <td>48491</td>
      <td>Williamson County, Texas</td>
      <td>410686</td>
      <td>*****</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop first row
population_2010_2016_data_df_drop = population_2010_2016_data_df.drop(population_2010_2016_data_df.index[0])
population_2010_2016_data_df_drop

pop_2010_2016_final = population_2010_2016_data_df_drop.rename(index=str, columns={"respop72010": "2010", "respop72011": "2011", "respop72012": "2012", "respop72013": "2013", "respop72014": "2014", "respop72015": "2015", "respop72016": "2016"})
pop_2010_2016_final
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO.id</th>
      <th>GEO.id2</th>
      <th>GEO.display-label</th>
      <th>rescen42010</th>
      <th>resbase42010</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0500000US48209</td>
      <td>48209</td>
      <td>Hays County, Texas</td>
      <td>157107</td>
      <td>157089</td>
      <td>158241</td>
      <td>163209</td>
      <td>168408</td>
      <td>176029</td>
      <td>184951</td>
      <td>194574</td>
      <td>204470</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0500000US48453</td>
      <td>48453</td>
      <td>Travis County, Texas</td>
      <td>1024266</td>
      <td>1024478</td>
      <td>1030569</td>
      <td>1061858</td>
      <td>1096122</td>
      <td>1120948</td>
      <td>1149668</td>
      <td>1174818</td>
      <td>1199323</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0500000US48491</td>
      <td>48491</td>
      <td>Williamson County, Texas</td>
      <td>422679</td>
      <td>422537</td>
      <td>426415</td>
      <td>442278</td>
      <td>456352</td>
      <td>470822</td>
      <td>489143</td>
      <td>508059</td>
      <td>528718</td>
    </tr>
  </tbody>
</table>
</div>




```python
population_merge = pd.merge(pop_2007_final, pop_2008_final, on="GEO.display-label", how="outer")
population_merge2 = pd.merge(population_merge, pop_2009_final, on="GEO.display-label", how="outer")
population_merge3 = pd.merge(population_merge2, pop_2010_2016_final, on="GEO.display-label", how="outer")
# population_merge3
population_merge3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GEO.id_x</th>
      <th>GEO.id2_x</th>
      <th>GEO.display-label</th>
      <th>2007</th>
      <th>HD02_VD01_x</th>
      <th>GEO.id_y</th>
      <th>GEO.id2_y</th>
      <th>2008</th>
      <th>HD02_VD01_y</th>
      <th>GEO.id_x</th>
      <th>...</th>
      <th>GEO.id2_y</th>
      <th>rescen42010</th>
      <th>resbase42010</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0500000US48209</td>
      <td>48209</td>
      <td>Hays County, Texas</td>
      <td>141480</td>
      <td>*****</td>
      <td>0500000US48209</td>
      <td>48209</td>
      <td>149476</td>
      <td>*****</td>
      <td>0500000US48209</td>
      <td>...</td>
      <td>48209</td>
      <td>157107</td>
      <td>157089</td>
      <td>158241</td>
      <td>163209</td>
      <td>168408</td>
      <td>176029</td>
      <td>184951</td>
      <td>194574</td>
      <td>204470</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0500000US48453</td>
      <td>48453</td>
      <td>Travis County, Texas</td>
      <td>974365</td>
      <td>*****</td>
      <td>0500000US48453</td>
      <td>48453</td>
      <td>998543</td>
      <td>*****</td>
      <td>0500000US48453</td>
      <td>...</td>
      <td>48453</td>
      <td>1024266</td>
      <td>1024478</td>
      <td>1030569</td>
      <td>1061858</td>
      <td>1096122</td>
      <td>1120948</td>
      <td>1149668</td>
      <td>1174818</td>
      <td>1199323</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0500000US48491</td>
      <td>48491</td>
      <td>Williamson County, Texas</td>
      <td>373363</td>
      <td>*****</td>
      <td>0500000US48491</td>
      <td>48491</td>
      <td>394193</td>
      <td>*****</td>
      <td>0500000US48491</td>
      <td>...</td>
      <td>48491</td>
      <td>422679</td>
      <td>422537</td>
      <td>426415</td>
      <td>442278</td>
      <td>456352</td>
      <td>470822</td>
      <td>489143</td>
      <td>508059</td>
      <td>528718</td>
    </tr>
  </tbody>
</table>
<p>3 rows × 24 columns</p>
</div>




```python
pop_merge = "population data/pop_merge.csv"
population_merge = pd.read_csv(pop_merge,thousands = ",")
population_merge
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Geography</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Population</td>
      <td>1489208</td>
      <td>1542212</td>
      <td>1592389</td>
      <td>1615225</td>
      <td>1667345</td>
      <td>1720882</td>
      <td>1767799</td>
      <td>1823762</td>
      <td>1877451</td>
      <td>1932511</td>
    </tr>
  </tbody>
</table>
</div>




```python
house_value_income_data.loc["Median (dollars)"]
```




    2007    182133.0
    2008    180400.0
    2009    184833.0
    2010    189233.0
    2011    185567.0
    2012    192033.0
    2013    203667.0
    2014    213767.0
    2015    236000.0
    2016    256200.0
    Name: Median (dollars), dtype: float64




```python
population_merge.loc["Population"]
```




    2007    1489208
    2008    1542212
    2009    1592389
    2010    1615225
    2011    1667345
    2012    1720882
    2013    1767799
    2014    1823762
    2015    1877451
    2016    1932511
    Name: Population, dtype: int64




```python
years = np.array([2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016])
years
```




    array([2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016])




```python
# Plot the world average as a line chart
median, = plt.plot(years, house_value_income_data.loc["Median (dollars)"], color="green", label="Average House Cost" )

# Plot the unemployment values for a single country
population, = plt.plot(years, population_merge.loc["Population"], color="blue",label="Population")

# Create a legend for our chart
plt.legend(handles=[median, population], loc="best")
plt.title("Austin Housing Costs vs. Population")
plt.ylabel("Dollars ($)")
plt.xlabel("Year")
plt.savefig("Saved_Pngs/pop_vs_value.png")

# Show the chart
plt.show()
```


![png](output_91_0.png)



```python
# Add dual axes
fig, ax1 = plt.subplots()

ax2 = ax1.twinx()
ax1.plot(years, population_merge.loc["Population"], 'b-')
ax2.plot(years, house_value_income_data.loc["Median (dollars)"], 'g-')

ax1.set_xlabel('Year')
ax1.set_ylabel('Population', color='b')
ax2.set_ylabel('Average House Cost ($)', color='g')
plt.legend(handles=[population, median], loc="best")

plt.show()
```


![png](output_92_0.png)

