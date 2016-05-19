---
title_meta  : Chapter 2
title       : Springboard Yelp Analysis
description : "Springboard Yelp Analysis"

--- type:NormalExercise xp:100 skills:1,3  key:0d1199072c
## Exploring the Data

The second chapter of this tutorial will be an alternative method of manipulating the Yelp star reviews. You will be working with the same sample of reviews of Indian restaurants but adapting the star ratings in a different way. 

This method looks to adapt the star reviews with the perception that Yelp reviewers with Indian heritage would provide more accurate and authentic ratings for Indian cuisine. The strategy for manpulating the star reviews involves selecting only the reviewers with Indian names for the agregate restaurant star rating. 

This means that you need a way to select just the users with native Indian names and that is where this chapter begins! 

You will first load in a list of native Indians names that can be used to sort users. A list of native Indain names is located on our server in a text file `indian_names.txt`. The object `indian_names_url` contains a link to the data. Use the `indian_names_url` and the `scan` function to create a list `indian_names` that contains the native names you will use to sort the users.


*** =instructions
- Use `scan()` to load in the `indian_names.txt` file
- Display the first 10 names with `head()`

*** =hint
When loading the names don't change the sample_code! Just remove the `#`

*** =pre_exercise_code
```{r,eval=FALSE}
# no pec
```

*** =sample_code
```{r, eval = FALSE}
# This url contains the .txt file with Indian names. (Note: Don't change this code)
indian_names_url <-url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt")

# Read Indian names into a list
#indian_names <- scan(indian_names_url, what = character())

# Show the first 10 names from the indian_names list
head(indian_names, ___)

```

*** =solution
```{r,eval=FALSE}
# This url contains the .txt file with Indian names. (Note: Don't change this code)
indian_names_url <-url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt")

# Read Indian names into a list
indian_names <- scan(indian_names_url, what = character())

# Show the first 10 names from the indian_names list
head(indian_names,10)
```

*** =sct
```{r,eval=FALSE}
# Fist instruction
test_object("indian_names", undefined_msg = "Something went wrong with loading the `indian_names`. Don't change the `sample_code` just remove the `#`.")

# Second instruction
test_function("head", args = c("x","n"), index = 1, incorrect_msg  = "Did you include the number of names you wanted to display?")

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```


--- type:NormalExercise xp:100 skills:1,3  key:cd888199f3
## Cleaning the Names list
 
Now that you have a list of native Indian names, make sure that the list will do what you need it to. The list was taken from an online resouce and may contain names that don't make sense or aren't useful. 

Take a look at the list and see if any names don't fit. The `table()` displays the names well. 

Looks like there are a few names that could select users that would be hard to tell whether they were native Indian or not. 

The single character names like `A.`, `C.` or `K.` may select users that we don't want. You should remove those names from the list before using it to select the native Indian users.

You can do this by finding a regular expression that will find all the names with a single character followed by a `.`. The regular expression `[A-z]\\.` should do the trick. Combine the regular expression with the `grep` function to locate the names that you want to eliminate. These locations can be used to eliminate just the names you don't want.


*** =instructions
- Display the names list with `table()`
- Use `grep` and the regular expression `[A-z]\\.` to locate the names you want to eliminate
- Double check that those are the right names
- Remove the unwanted names from the `indain_names` list using `-indian_names_remove`
- Display a table of the cleaned names list

*** =hint
When there is a `#` before the sample_code, don't change it, just remove the `#`

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.RData"))
```

*** =sample_code
```{r, eval = FALSE}
# Show the names list
#table(indian_names)

# Locate the names that you want to eliminate
indian_names_remove <- grep("___",indian_names, perl = TRUE)

# Check to make sure they are the correct names
#indian_names[indian_names_remove]

# Eliminate them from the indian_names list
indian_names_clean <- indian_names[-____]

# Table
#table(indian_names_clean)


```

*** =solution
```{r,eval=FALSE}
# Show the names list
table(indian_names)

# Locate the names that you want to eliminate
indian_names_remove <- grep("[A-z]\\.",indian_names, perl = TRUE)

# Check to make sure they are the correct names
indian_names[indian_names_remove]

# Eliminate them from the indian_names list
indian_names_clean <- indian_names[-indian_names_remove]

# Table
table(indian_names_clean)


```

*** =sct
```{r,eval=FALSE}
# Fist instruction
test_function("table", index = 1, not_called_msg = "You didn't show the table of indian names. Just remove the # before the sample_code.")

# Second instruction
test_function(grep, args = c("pattern","x","perl"), incorrect_msg = "Did you include the correct regular expression? Check the instructions for the right pattern.")

# Third instruction 
test_output_contains("indian_names[indian_names_remove]", not_called_msg = "Just remove the # before the sample_code.")

# Fourth instruction
test_output_contains("indian_names_clean <- indian_names[-indian_names_remove]", incorrect_msg = "Did you fill in the black space to remove the unwanted names?")

# Fifth instruction
test_function("table",index = 2, not_called_msg = "Don't forget to remove the # before the sample_code.")

# General
test_error()
success_msg("Well done! You've removed the unwanted names now you can subset the reviews for the authentic users!")
```


--- type:NormalExercise xp:100 skills:1,3  key:c56e152f5c
## Finding Authentic Users
 
You have successfully cleaned the list of native Indian names and you are ready to select just the reviews from the users that have a name that is part of this list. The `subset` fuction will make this task simple, so subset the `indian` data set by defining the `select` argument within the `subset` function. You define the column to select from and with the `%in%` operator you can define what to look for.

After successfully subsetting the data, generate a table of the authentic Indian users to get a sense of the size of the data.

Take a look at the number of users in each city. The `select`, `group_by`, `summarise` and `n()` functions of the `dplyr` package are great tools for quickly calculating the users in each city.  
 
*** =instructions
- Subset the `indian` data set to just the users with native Indian names. Use the operator `%in%` with the `indian_names_clean` data set as the sebset terms.
- Generate a table of the `authentic_users`.
- Display the total number of authentic users in each city. Use `select`, `group_by`, `summarise` and `n()`.

*** =hint
When loading the names don't change the sample_code! Just remove the `#`

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.RData"))

library(dplyr)

indian_names_clean <- indian_names[-grep("[A-z]\\.",indian_names, perl = TRUE)]
```

*** =sample_code
```{r, eval = FALSE, warning=FALSE}
# The package `dplyr` is available to use
# Subset the `indian` data set to just the users with native Indian names
authentic_users <- subset(indian$user_name %in% indian_names_clean)

# Table
#table(authentic_users$user_name)

# Find the number of users in each city
number_authentic_city <- authentic_users %>%
  select(city,user_name) %>%
  group_by(city) %>%
  summarise(users = n())

# Print the number of users per city
#number_authentic_city
```

*** =solution
```{r,eval=FALSE}
# The package `dplyr` is available to use
# Subset the `indian` data set to just the users with native Indian names
authentic_users <- subset(indian,indian$user_name %in% indian_names_clean)

# Table
table(authentic_users$user_name)

# Find the number of users in each city
number_authentic_city <- authentic_users %>%
  select(city,user_name) %>%
  group_by(city) %>%
  summarise(users = n())

# Print the number of users per city
number_authentic_city
```

*** =sct
```{r,eval=FALSE}
# Fist instruction
test_function("subset", args = c("x","select"),incorrect_msg = "Some thing went wrong with your `subset()`. Did you remember to add the data frame that the subset is coming from. The data frame `indians` should be included the first arguemnt.")

# Second instruction
test_output_contains("table(authentic_users$user_name)", not_called_msg = "Don't forget to remove the # before the sample_code." )

# Third instruction
test_data_frame("number_authentic_city", undefined_msg = NULL, incorrect_msg = "Some thing went wrong with your `number_authentic_city` data frame. Look at the `sample_code` that was given. Hit the refresh button to see it again.")

# Fourth instruction
test_output_contains("number_authentic_city", not_called_msg = "Don't forget to remove the # before the sample_code." )

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```


--- type:MultipleChoiceExercise xp:50 skills:1,3  key:f48b5ed8a3
## How Many Authentic Users?

Now that you have selected just the users with native Indian names you are ready to begin manipulate the reviews. Before you do, take a moment to explore the new data set and answer the following question.

Take a look at the `authentic_uers` and `number_authentic_city` data sets with `str()` or `summary` and then calculate the total number of authentic users.

*** =instructions
- 67
- 91
- 56
- 121
  
*** =hint
- a simple sum of the `number_authentic_city$users` would tell you the total users

*** =pre_exercise_code
```{r,eval=FALSE}

load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.RData"))


indian_names_clean <- indian_names[-grep("[A-z]\\.",indian_names, perl = TRUE)]
authentic_users <- subset(indian,indian$user_name %in% indian_names_clean)

library(dplyr)

number_authentic_city <- authentic_users %>%
  select(city,user_name) %>%
  group_by(city) %>%
  summarise(users = n())

```

*** =sct
```{r,eval=FALSE}
msg1 <- "Try again!"
msg2 <- "Very good! You found the total. Let's move on to calculating the authentic star reviews!"
msg3 <- "Incorrect. Maybe have a look at the hint."
msg4 <- "Not so good... Maybe have a look at the hint."
test_mc(correct = 2, feedback_msgs = c(msg1, msg2, msg3, msg4))
```


--- type:NormalExercise xp:100 skills:1,3  key:50ac99f74a
## Generating Average Authenic User Star Review

You've now selected your authentic Indian users and can use their reviews to generate average authentic star reviews! 

There are many ways to do this but the `dplyr` package, as you have seen, has many great tools to quickly group data, add new columns and calculate new values. You will use the `select`, `group_by`, `summarise` and `mutate` to add new variables to larger data set. 

You can use the `select` to choose the varibales you want in choose from to create the new variables. The `group_by()`, `%<%` and `summarized()` functions allow for separate calcualtions to be performed within the unique values of the variable being grouped. 

*** =instructions
- `group_by` the variables `city`, `business_name`, and `avg_stars`
- Use the `count` fucntion to tally the number of reviews for that restaurant
- Create a `new_stars` column using a `sum` of the `star` column
- Using the `mutate` fuction add a `diff` variable by subtracting the `new_stars` column by the `avg_stars` column
*** =hint
- Don't remove any of the `%>%` operators and make sure you have one after each function

*** =pre_exercise_code
```{r,eval=FALSE}
library(dplyr)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/authentic_users.RData"))
names(authentic_users)
```

*** =sample_code
```{r, eval = FALSE}
# The package `dplyr` is available to use
# Generate new "immigrant" rating
avg_review_indian <- authentic_users %>% 
    select(business_id, business_name, city, stars, avg_stars, is_indian, user_name) %>%

# Group by the `city`, `Business_name` and `avg_stars` variables  
    group_by(city, business_name, avg_stars) %>%
  
# Tally the number of restaurants
    summarise(count = n(),
              
# Create a `new_stars` column
    new_stars <- sum(stars) / count) %>%
  
# Mutate a column `dif` between the new authentic star rating and the overall average rating
    mutate(dif = new_stars - avg_stars)

```

*** =solution
```{r,eval=FALSE}
# The package `dplyr` is available to use
# Generate new "immigrant" rating
avg_review_indian <- authentic_users %>% 
    select(business_id, business_name, city, stars,
         avg_stars, is_indian, user_name) %>%
    group_by(city, business_name, avg_stars) %>%
    summarise(count = n(),
    new_stars = sum(stars) / count) %>%
    mutate(dif = new_stars - avg_stars)
```

*** =sct
```{r,eval=FALSE}
#first instruction
test_data_frame("avg_review_indian", incorrect_msg = "There are some issues with how you generated the avg_review_indian, check your see if you changed any of the sample code.")

# second instruction
test_function("group_by",args = c(".data"), index = 1, incorrect_msg = "Did you group the correct variable?. Check your code and type ?group_by into the console for more information")

# General
test_error()
success_msg("Good job! We've created weighted reveiws. Let's check them out in the next exercise!")
```


--- type:NormalExercise xp:100 skills:1,3  key:03314d8871
## Detecting Manipulation Effect 

Now that you have created new average star reviews for our the authentic Indian users, let's see if you can detect the effects of the modifications. 

To do so you will make use of some the `hist` plot and a `qplot` from the `ggplot2` package. These graphs will help us visualize the effect of your modification. Take note of the magnitudes of the changes and if there were any patterns in the distribution of the difference in star ratings.

*** =instructions
- Create a histogram of the `avg_stars` using the `hist()` function
- Create a histogram of the `new_stars` using the `hist()` function
- Plot the distribution of changes to ratings using the `hist()` function 
- Plot the changes to per restaurant using `qplot()`. Using the `reorder()` function will make the data more astetically pleaseing. Reorder the `business_name`variable by the `dif` variable.

*** =hint
- Remember to remove the `#` from the code to run!

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/avg_review_indian.RData"))
library(ggplot2)
```

*** =sample_code
```{r, eval = FALSE}
# The plotting package `ggplot2` is avaibale to use
# Create a histogram of the avg_stars
hist(avg_review_indian$___)

# Create a histogram of the new_stars
hist(avg_review_indian$___)

# Plot the distribution of changes to ratings 
hist(avg_review_indian$___, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes to per restaurant 
qplot(reorder(avg_review_indian$___,avg_review_indian$dif),avg_review_indian$___, xlab = "", ylab = "Changes in Star Rating")


```

*** =solution
```{r,eval=FALSE}
# The plotting package `ggplot2` is avaibale to use
# Create a histogram of the avg_stars
hist(avg_review_indian$avg_stars)

# Create a histogram of the new_stars
hist(avg_review_indian$new_stars)

# Plot the distribution of changes to ratings 
hist(avg_review_indian$dif, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes to per restaurant 
qplot(reorder(avg_review_indian$business_name,avg_review_indian$dif),avg_review_indian$dif, xlab = "", ylab = "Changes in Star Rating")

```

*** =sct
```{r,eval=FALSE}
# Fist instruction
msg1 <- "Fill in the varaible that is the overall average star rating."
test_function_v2("hist", "x", eval = FALSE, index = 1, 
                 incorrect_msg = msg1)
# second instruction
msg2 <- "Fill in the varaible that is the new star rating."
test_function_v2("hist", "x", eval = FALSE, index = 2, 
                 incorrect_msg = msg2)

# third instruction
msg3 <- "Fill in the varaible that is the difference in star rating."
test_function_v2("hist", "x", eval = FALSE, index = 3, 
                 incorrect_msg = msg3)

# fourth instruction
msg4 <- "Something went wrong with the `qplot()` function. Did you reorder correctly? If you need assistance type ?reorcer in the console."
test_function_v2("qplot", args = c("x","y"), eval = FALSE, index = 1, 
                 incorrect_msg = msg4)

# General
test_error()
success_msg("Congradulations! You have finished the course and now know some good tools in R to manipulate data. You have also seen them work to solve an interesting problem! For more indepth coverage to the concepts in this course try our Premium courses!")
```




