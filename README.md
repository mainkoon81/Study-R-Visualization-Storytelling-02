# Study-Visualization-Storytelling (R)

__[R]__
 - I. Explore One Variable
 - II. Explore Two Variable 
 - III. Explore Multi-Variable

### I. One Variable
__Story:__ People's perception of their audience on FB matches up to the reality? 
 - Well, who you think is in your audience, affects how you present yourself. 
 - Who's actually seeing the content they are sharing?  
 - Survey Q1. "How many do you think saw the post? 
   - There is a big mismatch b/w people's perceived audience size and their actual audience size.
   
__Library:__ `ggplot2`
__Data:__ 'pseudo_facebook.tsv' 
<img src="https://user-images.githubusercontent.com/31917400/35759700-3fd3e9f2-0873-11e8-93d7-ff5e74cbefc6.jpg" />

 - Histogram of Users' Birthdays 
   - x-axis is the 'date of birth'
   - Adjust x-axis' bins, using 'scale' layers!...JUST marking ticks, using "1 to 31"
```
pf <- read.csv('C:/Users/Minkun/Desktop/classes_1/NanoDeg/1.Data_AN/L7/---New R/data/pseudo_facebook.tsv', sep = '\t')

ggplot(aes(x = dob_day), data = pf) + geom_histogram(binwidth = 1) + scale_x_continuous(breaks = 1:31)
```
<img src="https://user-images.githubusercontent.com/31917400/35759700-3fd3e9f2-0873-11e8-93d7-ff5e74cbefc6.jpg" />






















