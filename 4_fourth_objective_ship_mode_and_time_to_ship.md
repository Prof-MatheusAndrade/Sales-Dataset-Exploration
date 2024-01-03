# Objective 4 - Relationship Between Ship Mode and Time to Ship
To investigate the correlation between Ship Mode and "Time to Ship" (defined as the difference between Ship date and Order Date), a Databricks notebook named ["2_Ship Mode_and_Time_to_Ship.ipynb"](https://github.com/Prof-MatheusAndrade/Sales-Dataset-Exploration/blob/main/0_Materials/2_Databricks_Notebooks/2_Ship%20Mode_and_Time_to_Ship.ipynb) was employed for the analysis. The notebook documents all the steps involved in the investigation.

In the first step, a SQL query was used to combine the fact table "Order" with the two dimension tables "Ship" and "Ship Mode." This query involved calculating the difference in the number of days between Order Date and Ship Date to derive the "Time to Ship." Additionally, a SQL case was implemented to convert the Ship Mode Class from "Same Day," "First Class," "Second Class," and "Standard Class" to numerical values.

After obtaining the data, Plotly and Pandas were utilized to generate visualizations. The first plot is presented below, featuring a Box plot of the Time to Ship colored by Ship Mode. This initial plot provides strong evidence of a relationship between Ship Mode and Time to Ship, as the box distributions are distinctly separated between the classes.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=13ogKnG007kqwDk3miy60jumU93KucBou"  width="80%" height="50%">
</p>

The second plot serves as a complement to the first one, featuring a histogram of the Time to Ship colored by Ship Mode. Similar to the first plot, this visualization reinforces the observed relationship, with the frequency of the standard class being greater than that of the same day, which is expected due to the longer delivery time associated with the standard class.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=13tCtFtE-OAk4dXKDphxmeUypB1Hlj7Cj"  width="80%" height="50%">
</p>

The third plot is a Box plot of the Time to Ship, now with the Y-axis representing the Ship Mode in the numerical version. This plot, colored by Ship Mode, further suggests a positive linear correlation between Ship Mode and Time to Ship.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=13tQHKK-WRlSBfgSWv5TUM24_nh7c4OuU"  width="80%" height="50%">
</p>

To validate these observations, three different types of correlations were calculated, and the results are presented in the figure below.

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=1422eEscpMlAZBFemCx93O-MAZlZj3sjj"  width="60%" height="30%">
</p>

**1. Pearson = 0.817761**: Pearson correlation ranges from -1 to 1. It measures the linear relationship between two continuous variables. In this case, the value is 0.817761, indicating a strong positive linear correlation.

**2. Spearman = 0.771999**: Spearman correlation is a rank correlation measure, less sensitive to outliers. It assesses the monotonic relationship between variables. The value 0.771999 suggests a strong positive correlation in the ranks of the variables.

**3. Kendall = 0.680643**: Kendall correlation is also a rank correlation measure. It evaluates the concordance or discordance in the ranks of variables. The value 0.680643 indicates a moderate positive correlation in the ranks of the variables.

In summary, all coefficients indicate a positive correlation between the variables, but the strength of this correlation varies slightly between methods. The highest value is for Pearson, followed by Spearman and then Kendall. In conclusion, Time to Ship exhibits a strong relationship with Ship Mode, indicating that the Time to Ship is faster for the following Ship Modes, in order:

-> "Same Day" - Faster delivery with a median of the cases on the same day and few outliers in one day.

->"First Class" - Second fastest delivery with a median of the cases on the second day.

->"Second Class" - Third fastest delivery with a median of the cases on the third day.

->"Standard Class" - Slower delivery with a median of the cases on the fifth day.
