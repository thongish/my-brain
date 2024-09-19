#MATH/W2
# Graphical summaries of numerical data

## Frequency distribution

- The possible values of X are divided into non-overlapping classes (i.e. intervals) of equal width
- The number of times a measurement of X falls into a given class is the *frequency* of that class
- **Relative frequency**
	- Frequency / total # of values of X
	- ex. X falls into a class 20 times, the total number of values is 100,
		- Relative frequency of that class is 0.2 

### Precision

- The interval of values in the data set
### Class

- **Modal class**
	- The class of which has the highest frequency
- **Class limit**
	- Upper class limit
		- The highest value in the range of a class
	- Lower class limit
		- The lowest value in the range of a class
- **Class mark**
	- Average of the lower and upper class limit of a class
- **Class boundaries**
	- Lower class boundary
		- The average of the previous class highest value with the current class we are looking at lowest value
	- Upper class boundary
		- The average of the highest value of the current class we are looking at and the lowest value of the next class
- **Class width**
	- Is the upper boundary minus the lower boundary

- The number of classes should be approximately **n^1/2**, where **n = sample size**

## Histograms

- A histogram is a visual representation of the corresponding frequency distribution
- You need to determine the *class boundaries* to correctly position the left and right sides of the rectangle
- The height of a histogram rectangle represents the frequency or relative frequency of that class

# Percentiles and quartiles

**Percentile**
- The k$^t$$^h$ percentile of a numerical variable X is denoted P$_k$ 
- Divides data into two parts:
	- The lower k% of values and the upper (100 - k)% of values
		- The lower k% of values have to be less than P$_k$

- Example: On the Math 12 Provincial exam, Bill scored in the 75th percentile
	- Incorrect: he scored 75/100
	- Correct: he is doing better than 75% of people

**Quartiles**
- Are percentiles in multiples of 25
	- Q1 = P$_2$$_5$ (also the 25th percentile)
	- Q2 = P$_5$$_0$ (also the 50th percentile)
	- Q3 = P$_7$$_5$ (also the 75th percentile)
- Inter-quartile range
	- Q3 - Q1

**Five-number summary**
- Q$_0$, Q$_1$, Q$_2$, Q$_3$, Q$_4$
	- Where Q$_0$ is the minimum value
		- Q$_4$ is the maximum value

# Box plots

![[Pasted image 20240911104741.png]]
- A boxplot is a simple way to visualize the *five-number summary*
- Shows the full *range* (distance between min and max values)
- Also shows the range of the middle 50% of the observations (**the box**) which is the **inter-quartile range** (IQR)

# Outliers

- Extremely small or large values of X
- Rule used for identifying outliers
	- *IQR* = Q$_3$ - Q$_1$ 
	- lower limit = Q$_1$ - 1.5 * *IQR*
	- upper limit = Q$_3$ + 1.5 * *IQR*
- If the value is below or above the lower and upper limits, they are outliers
# Graphs for categorical data

## Pie chart

- An alternative to the bar chart, although they can make it harder to compare different categories
![[Pasted image 20240915113744.png]]
## Bar chart

- The best way to present one categorical variable 
- Possible values of X go along the horizontal axis
- The frequencies (count) go along the vertical axis
![[Pasted image 20240915113704.png]]





# Flash cards

What is a **class**? A group of values of which X is placed in

What is the ***frequency*** of a class?::The number of times a measurement of X falls into a give class

What is a **frequency distribution**?::How often different values or ranges of values occur in a dataset

What is relative frequency?::Frequency / total number of values of X.

What is precision?::The interval of values in the data set.

What is a modal class?::The class with the highest frequency.

What is the upper class limit?::The highest value in the range of a class.

What is the lower class limit?::The lowest value in the range of a class.

What is the class mark?::The average of the lower and upper class limits of a class.

What is the lower class boundary?::The average of the highest value of the previous class and the lowest value of the current class.

What is the upper class boundary?::The average of the highest value of the current class and the lowest value of the next class.

What is class width?::The upper boundary minus the lower boundary.

How do you determine the number of classes?::The number of classes is approximately n^(1/2), where n = sample size.

What is a histogram?::A visual representation of the corresponding frequency distribution.

What does the height of a histogram rectangle represent?::The frequency or relative frequency of that class.

What does it mean if Bill scored in the 75th percentile?::He is doing better than 75% of people.

What are quartiles?::Percentiles in multiples of 25.

What is the inter-quartile range (IQR)?
?
The difference between Q3 and Q1.
- Q$_3$ - Q$_1$

What is the five-number summary?::Q0 (min), Q1, Q2, Q3, Q4 (max).

What is a boxplot?::A simple way to visualize the five-number summary and the inter-quartile range.

What are outliers?::Extremely small or large values of X.

What is the rule for identifying outliers?
?
- Outliers are below (Q1 - 1.5 * IQR) 
- or above (Q3 + 1.5 * IQR).

What is a pie chart?::A chart that represents parts of a whole, but can make comparing categories harder.

What is a bar chart?::The best way to present one categorical variable, with values on the horizontal axis and frequencies on the vertical axis.

Given data values 1, 3, 5, 7, 8, 10, 12, 16
What is the 50th percentile?
?
7.5
![[Pasted image 20240918140651.png]]