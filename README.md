Optimizing Functions of One Variable: Cost Minimization
In this assignment you will solve a simple optimization problem for a function of one variable. Given a dataset of historical prices of a product from two suppliers, your task is to identify what share of the product you should buy from each of the suppliers to make the best possible investment in the future. Stating the problem mathematically, you will construct a target function to minimize, evaluate its minimum and investigate how its derivative is connected with the result.

Table of Contents
1 - Statement of the Optimization Problem
1.1 - Description of the Problem
1.2 - Mathematical Statement of the Problem
1.3 - Solution Approach
2 - Optimizing Function of One Variable in Python
2.1 - Packages
2.2 - Open and Analyze the Dataset
Exercise 1
2.3 - Construct the Function 
 to Optimize and Find its Minimum Point
Exercise 2
Exercise 3
Exercise 4

1 - Statement of the Optimization Problem

1.1 - Description of the Problem
Your Company is aiming to minimize production costs of some goods. During the production process, an essential product P is used, which can be supplied from one of two partners - supplier A and supplier B. Your consultants requested the historical prices of product P from both suppliers A and B, which were provided as monthly averages for the period from February 2018 to March 2020.

Preparing Company Budget for the coming twelve months period, your plan is to purchase the same amount of product P monthly. Choosing the supplier, you noticed, that there were some periods in the past, when it would be more profitable to use supplier A (the prices of product P were lower), and other periods to work with supplier B. For the Budget model you can set some percentage of the goods to be purchased from supplier A (e.g. 60%) and the remaining part from supplier B (e.g. 40%), but this split should be kept consistent for the whole of the twelve months period. The Budget will be used in preparation for the contract negotiations with both suppliers.

Based on the historical prices, is there a particular percentage which will be more profitable to supply from Company A, and the remaining part from Company B? Or maybe it does not matter and you can work just with one of the suppliers?


1.2 - Mathematical Statement of the Problem
Denoting prices of the product P from Company A and Company B as 𝑝𝐴
 (USD) and 𝑝𝐵
 (USD) respectively, and the volume of the product to be supplied per month as 𝑛
 (units), the total cost in USD is:

𝑓(𝜔)=𝑝𝐴𝜔𝑛+𝑝𝐵(1−𝜔)𝑛,
where 0≤𝜔≤1
 is the parameter. If 𝜔=1
, all goods will be supplied from Company A, and if 𝜔=0
, from Company B. In case of 0<𝜔<1
, some percentage will be allocated to both.

As it is planned to keep the volume 𝑛
 constant over the next twelve months, in the mathematical model the common approach is to put 𝑛=1
. You can do this, because nothing depends on the volume and the end result will be the same. Now the total cost will be simpler:

𝑓(𝜔)=𝑝𝐴𝜔+𝑝𝐵(1−𝜔)(1)
Obviously, you do not know the future prices 𝑝𝐴
 and 𝑝𝐵
, only historical values (prices {𝑝1𝐴,⋯,𝑝𝑘𝐴}
 and {𝑝1𝐵,⋯,𝑝𝑘𝐵}
 for 𝑘
 months). And historically there were various periods of time when it was better to take 𝜔=1
 (𝑝𝑖𝐴<𝑝𝑖𝐵
) or 𝜔=0
 (𝑝𝑖𝐴>𝑝𝑖𝐵
). Is it possible now to choose some 𝜔
 value that would provide some evidence of minimum costs in the future?


1.3 - Solution Approach
This is a standard portfolio management (investment) problem well known in statistics, where based on the historical prices you need to make investment decision to maximize profit (minimize costs). Since statistics has not been covered in this Course, you do not need to understand the details about the function (𝜔)
 (called loss function) to minimize, explained in the next paragraph.

The approach is to calculate 𝑓(𝜔)
 for each of the historical prices 𝑝𝑖𝐴
 and 𝑝𝑖𝐵
, 𝑓𝑖(𝜔)=𝑝𝑖𝐴𝜔+𝑝𝑖𝐵(1−𝜔)
. Then take an average of those values, 𝑓(𝜔)⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯=mean(𝑓𝑖(𝜔))=1𝑘∑𝑘𝑖=1𝑓𝑖(𝜔)
 and look for such value of 𝜔
 which makes 𝑓𝑖(𝜔)
 as "stable" as possible - varying as little as possible from the average 𝑓(𝜔)⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
. This means that you would want to minimize the sum of the differences (𝑓𝑖(𝜔)−𝑓(𝜔)⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯)
. As the differences can be negative or positive, a common approach is to take the squares of those and take an average of the squares:

(𝜔)=1𝑘∑𝑖=1𝑘(𝑓𝑖(𝜔)−𝑓(𝜔)⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯)2(2)
In statistics (𝜔)
 is called a variance of {𝑓1(𝜔),⋯,𝑓𝑘(𝜔)}
. The aim is to minimize the variance (𝜔)
, where 𝜔∈[0,1]
. Again, do not worry if you do not understand deeply why particularly this function (𝜔)
 was chosen. You might think if it is logical to minimize an average 𝑓(𝜔)⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯
, but risk management theory states that in this problem variance needs to be optimized.

Statistical theory shows that there is an 𝜔∈[0,1]
 value which minimizes function (𝜔)
 and it can be found using some properties of the datasets {𝑝1𝐴,⋯,𝑝𝑘𝐴}
 and {𝑝1𝐵,⋯,𝑝𝑘𝐵}
. However, as this is not a Course about statistics, the example is taken to illustrate an optimization problem of one variable based on some dataset. It is a chance for you to check your understanding and practice this week material.

Now let's upload a dataset and explore if it is possible to find a minimum point for the corresponding function (𝜔)
.


2 - Optimizing Function of One Variable in Python

2.1 - Packages
Let's import all of the required packages. In addition to the ones you have been using in this Course before, you will need to import pandas library. It is a commonly used package for data manipulation and analysis.

# A function to perform automatic differentiation.
from jax import grad
# A wrapped version of NumPy to use JAX primitives.
import jax.numpy as np
# A library for programmatic plot generation.
import matplotlib.pyplot as plt
# A library for data manipulation and analysis.
import pandas as pd
​
# A magic command to make output of plotting commands displayed inline within the Jupyter notebook.
%matplotlib inline 
Load the unit tests defined for this notebook.

import w1_unittest
​
# Please ignore the warning message about GPU/TPU if it appears.

2.2 - Open and Analyze the Dataset
Historical prices for both suppliers A and B are saved in the file data/prices.csv. To open it you can use pandas function read_csv. This example is very simple, there is no need to use any other parameters.

df = pd.read_csv('data/prices.csv')
The data is now saved in the variable df as a DataFrame, which is the most commonly used pandas object. It is a 2-dimensional labeled data structure with columns of potentially different types. You can think of it as a table or a spreadsheet. Full documentation can be found here.

View the data with a standard print function:

print(df)
To print a list of the column names use columns attribute of the DataFrame:

print(df.columns)
Reviewing the displayed table and the column names you can conclude that monthly prices are provided (in USD) and you only need the data from the columns price_supplier_a_dollars_per_item and price_supplier_b_dollars_per_item. In real life the datasets are significantly larger and require a proper review and cleaning before injection into models. But this is not the focus of this Course.

To access the values of one column of the DataFrame you can use the column name as an attribute. For example, the following code will output date column of the DataFrame df:

df.date

Exercise 1
Load the historical prices of supplier A and supplier B into variables prices_A and prices_B, respectively. Convert the price values into NumPy arrays with elements of type float32 using np.array function.

Hint
### START CODE HERE ### (~ 4 lines of code)
prices_A = None
prices_B = None
prices_A = None(None).astype('None')
prices_B = None(None).astype('None')
### END CODE HERE ###
# Print some elements and mean values of the prices_A and prices_B arrays.
print("Some prices of supplier A:", prices_A[0:5])
print("Some prices of supplier B:", prices_B[0:5])
print("Average of the prices, supplier A:", np.mean(prices_A))
print("Average of the prices, supplier B:", np.mean(prices_B))
Expected Output
Some prices of supplier A: [104. 108. 101. 104. 102.]
Some prices of supplier B: [76. 76. 84. 79. 81.]
Average of the prices, supplier A: 100.799995
Average of the prices, supplier B: 100.0
w1_unittest.test_load_and_convert_data(prices_A, prices_B)
Average prices from both suppliers are similar. But if you will plot the historical prices, you will see that there were periods of time when the prices were lower for supplier A, and vice versa.

fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)
plt.plot(prices_A, 'g', label="Supplier A")
plt.plot(prices_B, 'b', label="Supplier B")
plt.legend()
​
plt.show()
Based on the historical data, can you tell which supplier it will be more profitable to work with? As discussed in the section 1.3, you need to find such an 𝜔∈[0,1]
 which will minimize function (2)
.


2.3 - Construct the Function 
 to Optimize and Find its Minimum Point

Exercise 2
Calculate f_of_omega, corresponding to the 𝑓𝑖(𝜔)=𝑝𝑖𝐴𝜔+𝑝𝑖𝐵(1−𝜔)
. Prices {𝑝1𝐴,⋯,𝑝𝑘𝐴}
 and {𝑝1𝐵,⋯,𝑝𝑘𝐵}
 can be passed in the arrays pA and pB. Thus, multiplying them by the scalars omega and 1 - omega and adding together the resulting arrays, you will get an array containing {𝑓1(𝜔),⋯,𝑓𝑘(𝜔)}
.

Then array f_of_omega can be taken to calculate L_of_omega, according to the expression (2)
:

(𝜔)=1𝑘∑𝑖=1𝑘(𝑓𝑖(𝜔)−𝑓(𝜔)⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯⎯)2
def f_of_omega(omega, pA, pB):
    ### START CODE HERE ### (~ 1 line of code)
    f = None
    ### END CODE HERE ###
    return f
​
def L_of_omega(omega, pA, pB):
    return 1/len(f_of_omega(omega, pA, pB)) * np.sum((f_of_omega(omega, pA, pB) - np.mean(f_of_omega(omega, pA, pB)))**2)
print("L(omega = 0) =",L_of_omega(0, prices_A, prices_B))
print("L(omega = 0.2) =",L_of_omega(0.2, prices_A, prices_B))
print("L(omega = 0.8) =",L_of_omega(0.8, prices_A, prices_B))
print("L(omega = 1) =",L_of_omega(1, prices_A, prices_B))
Expected Output
L(omega = 0) = 110.72
L(omega = 0.2) = 61.1568
L(omega = 0.8) = 11.212797
L(omega = 1) = 27.48
w1_unittest.test_f_of_omega(f_of_omega)
Analysing the output above, you can notice that values of the function 
 are decreasing for 𝜔
 increasing from 0
 to 0.2
, then to 0.8
, but there is an increase of the function 
 when 𝜔=1
. What will be the 𝜔
 giving the minimum value of the function 
?

In this simple example (𝜔)
 is a function of one variable and the problem of finding its minimum point with a certain accuracy is a trivial task. You just need to calculate function values for each 𝜔=0,0.001,0.002,⋯,1
 and find minimum element of the resulting array.

Function L_of_omega will not work if you will pass an array instead of a single value of omega (it was not designed for that). It is possible to rewrite it in a way that it would be possible, but here there is no need in that right now - you can calculate the resulting values in the loop as there will be not as many of them.


Exercise 3
Evaluate function L_of_omega for each of the elements of the array omega_array and pass the result into the corresponding element of the array L_array with the function .at[<index>].set(<value>).

Note: jax.numpy has been uploaded instead of the original NumPy. Up to this moment jax functionality has not been actually used, but it will be called in the cells below. Thus there was no need to upload both versions of the package, and you have to use .at[<index>].set(<value>) function to update the array.

# Parameter endpoint=True will allow ending point 1 to be included in the array.
# This is why it is better to take N = 1001, not N = 1000
N = 1001
omega_array = np.linspace(0, 1, N, endpoint=True)
​
# This is organised as a function only for grading purposes.
def L_of_omega_array(omega_array, pA, pB):
    N = len(omega_array)
    L_array = np.zeros(N)
​
    for i in range(N):
        ### START CODE HERE ### (~ 2 lines of code)
        L = None(None[None], None, None)
        L_array = L_array.at[None].set(None)
        ### END CODE HERE ###
        
    return L_array
​
L_array = L_of_omega_array(omega_array, prices_A, prices_B)
print("L(omega = 0) =",L_array[0])
print("L(omega = 1) =",L_array[N-1])
Expected Output
L(omega = 0) = 110.72
L(omega = 1) = 27.48
w1_unittest.test_L_of_omega_array(L_of_omega_array)
Now a minimum point of the function (𝜔)
 can be found with a NumPy function argmin(). As there were 𝑁=1001
 points taken in the segment [0,1]
, the result will be accurate to three decimal places:

i_opt = L_array.argmin()
omega_opt = omega_array[i_opt]
L_opt = L_array[i_opt]
print(f'omega_min = {omega_opt:.3f}\nL_of_omega_min = {L_opt:.7f}')
This result means that, based on the historical data, 𝜔=0.702
 is expected to be the most profitable choice for the share between suppliers A and B. It is reasonable to plan 70.2%
 of product P to be supplied from Company A, and 29.8%
 from Company B.

If you would like to improve the accuracy, you just need to increase the number of points N. This is a very simple example of a model with one parameter, resulting in optimization of a function of one variable. It is computationally cheap to evaluate it in many points to find the minimum with certain accuracy. But in machine learning the models have hundreds of parameters, using similar approach you would need to perform millions of target function evaluations. This is not possible in most of the cases, and that's where Calculus with its methods and approaches comes into play.

In the next weeks of this Course you will learn how to optimize multivariate functions using differentiation. But for now as you are on the learning curve, let's evaluate the derivative of the function (𝜔)
 at the points saved in the array omega_array to check that at the minimum point the derivative is actually the closest to zero.


Exercise 4
For each 𝜔
 in the omega_array calculate 𝑑𝑑𝜔
 using grad() function from JAX library. Remember that you need to pass the function which you want to differentiate (here (𝜔)
) as an argument of grad() function and then evaluate the derivative for the corresponding element of the omega_array. Then pass the result into the corresponding element of the array dLdOmega_array with the function .at[<index>].set(<value>).

Hint
# This is organised as a function only for grading purposes.
def dLdOmega_of_omega_array(omega_array, pA, pB):
    N = len(omega_array)
    dLdOmega_array = np.zeros(N)
​
    for i in range(N):
        ### START CODE HERE ### (~ 2 lines of code)
        dLdOmega = None(None)(None[None], None, None)
        dLdOmega_array = dLdOmega_array.at[None].set(None)
        ### END CODE HERE ###
        
    return dLdOmega_array
​
dLdOmega_array = dLdOmega_of_omega_array(omega_array, prices_A, prices_B)
print("dLdOmega(omega = 0) =",dLdOmega_array[0])
print("dLdOmega(omega = 1) =",dLdOmega_array[N-1])
Expected Output
dLdOmega(omega = 0) = -288.96
dLdOmega(omega = 1) = 122.47999
w1_unittest.test_dLdOmega_of_omega_array(dLdOmega_of_omega_array)
Now to find the closest value of the derivative to 0
, take absolute values ||𝑑𝑑𝜔||
 for each omega and find minimum of them.

i_opt_2 = np.abs(dLdOmega_array).argmin()
omega_opt_2 = omega_array[i_opt_2]
dLdOmega_opt_2 = dLdOmega_array[i_opt_2]
print(f'omega_min = {omega_opt_2:.3f}\ndLdOmega_min = {dLdOmega_opt_2:.7f}')
The result is the same: 𝜔=0.702
. Let's plot (𝜔)
 and 𝑑𝑑𝜔
 to visualize the graphs of them, minimum point of the function (𝜔)
 and the point where its derivative is around 0
:

import numpy as np
import matplotlib.pyplot as plt
​
# Define the function 𝜑(𝜔) and its derivative 𝑑𝜑/𝑑𝜔
def phi(omega):
    return ...  # Define the function 𝜑(𝜔)
​
def dphi_domega(omega):
    return ...  # Define the derivative 𝑑𝜑/𝑑𝜔
​
# Generate values for 𝜔
omega_array = np.linspace(start_value, end_value, num_points)
​
# Calculate the values of 𝜑(𝜔) and 𝑑𝜑/𝑑𝜔
phi_values = phi(omega_array)
dphi_domega_values = dphi_domega(omega_array)
​
# Plot 𝜑(𝜔) and 𝑑𝜑/𝑑𝜔
plt.plot(omega_array, phi_values, label='𝜑(𝜔)')
plt.plot(omega_array, dphi_domega_values, label='𝑑𝜑/𝑑𝜔')
plt.axvline(x=omega_opt, color='red', linestyle='--', label='Minimum point')
plt.axvline(x=omega_opt_2, color='blue', linestyle='--', label='Point: 𝑑𝜑/𝑑𝜔 ≈ 0')
​
# Set labels and title
plt.xlabel('𝜔')
plt.ylabel('Function Value')
plt.title('Graphs of 𝜑(𝜔) and 𝑑𝜑/𝑑𝜔')
​
# Add legend
plt.legend()
​
# Display the plot
plt.show()
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
Cell In [1], line 12
      9     return ...  # Define the derivative 𝑑𝜑/𝑑𝜔
     11 # Generate values for 𝜔
---> 12 omega_array = np.linspace(start_value, end_value, num_points)
     14 # Calculate the values of 𝜑(𝜔) and 𝑑𝜑/𝑑𝜔
     15 phi_values = phi(omega_array)

NameError: name 'start_value' is not defined

Congratulations, you have finished the assignment for this week! This example illustrates how optimization problems may appear in real life, and gives you an opportunity to explore the simple case of minimizing a function with one variable. Now it is time to learn about optimization of multivariate functions!
