# Study-Visualization-Storytelling (R)

__[R]__
 - I. Explore One Variable
 - II. Explore Two Variable 
 - III. Explore Multi-Variable

### I. One Variable
http://hci.stanford.edu/publications/2013/invisibleaudience/invisibleaudience.pdf

__Story:__ People's perception of their audience on FB matches up to the reality? 
 - Well, FB believes who you think is in your audience affects how you present yourself. 
 - Who's actually seeing the content they are sharing?  
   - __Survey Q1.__ "How many do you think saw the post? 
     - There is a big mismatch b/w people's perceived audience size and their actual audience size.
     - People dramatically underestimate the size of their audience - (1/4). 
   
__Library:__ `ggplot2`

__Data:__ 'pseudo_facebook.tsv' 

#### Adjust a font size?
 - with the font size set to 20 ?
```
install.packages('ggthemes', dependencies = TRUE)
library(ggthemes)
theme_set(theme_minimal(20)) 

pf <- read.csv('C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/pseudo_facebook.tsv', sep = '\t')
```
<img src="https://user-images.githubusercontent.com/31917400/35759700-3fd3e9f2-0873-11e8-93d7-ff5e74cbefc6.jpg" />

>Phase_01. Understand the audience
 - Histogram of Users' **Birthdays**
   - 'date of birth' on x-axis
   - Adjust x-axis' bins, using 'scale' layers - `+ scale_x_continuous(breaks)`...JUST marking ticks - ("1 to 31")
   - 'binwidth argument' in the 'geom_histogram' layer is actually change bin size while 'breaks argument' in the 'scale' layer just change the tick marks!
```
ggplot(aes(x = dob_day), data = pf) + geom_histogram(binwidth = 1) + scale_x_continuous(breaks = 1:31)
```
 - Faceting, Splitting the data over 'dob_month' variable: `+ facet_wrap( ~ variable, ncol)`
<img src="https://user-images.githubusercontent.com/31917400/35760868-2c798ad0-087b-11e8-91e5-08aad97e0341.jpg" width="300" height="160" /> 

```
ggplot(data = pf, aes(x = dob_day)) + geom_histogram(binwidth = 1) + scale_x_continuous(breaks = 1:31) +
  facet_wrap(~dob_month, ncol = 4)
```
<img src="https://user-images.githubusercontent.com/31917400/35760701-e1ce5ce6-0879-11e8-808a-e6f293bc4f09.jpg" width="600" height="160" />

 - Histogram of Users' **friend size**
   - 'friends_count' on x-axis
   - Outliers? then 'Limiting axis': `+ scale_x_continuous(limits = c(n, n), breaks)`
   - Faceting by 'gender': `+ facet_wrap( ~ variable)` or '+ facet_grid(gender ~ .)' 
   - then ommiting NA values..it sould be dealt within the 'data' level: `data=subset(pf, !is.na(gender))`
   - IF the relationship include categorical variable (such as 'gender'), 
     - STATISTICS - which side has more friend on average?
     - To find average 'friend_count_by_gender', we use `by(target variable, categorical variable, function)`
     
```
ggplot(aes(x=friend_count), data=pf) + geom_histogram() 

ggplot(aes(x=friend_count), data=pf) + geom_histogram() + scale_x_continuous(limits = c(0,1000))

ggplot(aes(x = friend_count), data = pf) + geom_histogram(binwidth = 25) + scale_x_continuous(limits = c(0, 1000), breaks = seq(0, 1000, 50))
```
<img src="https://user-images.githubusercontent.com/31917400/35767164-d029a0c6-08de-11e8-9814-07da198c3bc2.jpg" width="1200" height="160" />

```
ggplot(aes(x = friend_count), data = pf) + geom_histogram(binwidth = 25) + scale_x_continuous(limits = c(0, 1000), breaks = seq(0, 1000, 50)) + facet_wrap(~gender)

ggplot(aes(x = friend_count), data = subset(pf, !is.na(gender))) + geom_histogram(binwidth = 25) + scale_x_continuous(limits = c(0, 1000), breaks = seq(0, 1000, 50)) + facet_wrap(~gender)
```
<img src="https://user-images.githubusercontent.com/31917400/35767303-de7caf80-08e1-11e8-9bdb-9f4b269e2486.jpg" width="700" height="200" />

```
table(pf$gender) 
by(pf$friend_count, pf$gender, summary)
```
<img src="https://user-images.githubusercontent.com/31917400/35767397-73a5e5bc-08e3-11e8-800c-4b8a94318713.jpg" width="600" height="80" />

 - Histogram of Users **tenure by year** - how many days they've used facebook so far?
   - 'tenure/365' on x-axis
   - Determines the color of the outline, area_inside in a plot - `+ geom_histogram(binwidth, color, fill)`
   - How about gender difference? - `+ facet_wrap(~gender)`
```
ggplot(aes(x = tenure), data = pf) +
  geom_histogram(binwidth = 30, color = 'black', fill = '#099DD9')
  
ggplot(aes(x = tenure/365), data=subset(pf, !is.na(gender))) +
  geom_histogram(binwidth = 0.25, color = 'black', fill = '#F79420') + scale_x_continuous(breaks=seq(1,7,1), limits=c(0,7)) +
  facet_wrap(~gender) +  xlab('Number of years using Facebook') + ylab('Number of users in sample')
```   
<img src="https://user-images.githubusercontent.com/31917400/35768009-bc496a96-08ed-11e8-8982-6e2c6598ae49.jpg" width="600" height="170" />   













