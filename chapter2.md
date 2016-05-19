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
indian_names_url = url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt")

# Read Indian names into a list
#indian_names <- scan(indian_names_url, what = character())

# Show the first 10 names from the indian_names list
head(indian_names, ___)

```

*** =solution
```{r,eval=FALSE}
# This url contains the .txt file with Indian names. (Note: Don't change this code)
indian_names_url = url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt")

# Read Indian names into a list
indian_names <- scan(indian_names_url, what = character())

# Show the first 10 names from the indian_names list
head(indian_names,10)
```

*** =sct
```{r,eval=FALSE}
# Fist instruction
test_object("indian_names", incorrect_msg = "Something went wrong with loading the `indian_names`. Don't change the `sample_code` just remove the `#`.")

# Second instruction
test_function("head", args = c("x","n"), index = 1, incorrect_msg  = "Did you include the number of names you wanted to display?")

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```

--- type:NormalExercise xp:100 skills:1,3  key:cd888199f3
## Cleaning the Names list
 
Now that you have a list of native Indian names, make sure that the list will do what you need it to. The list was taken from an online resouce and may contain names that don't make sense or aren't useful. 

Take a look at the list and see if any names don't fit. 

Looks like there are a few names that could select users that would be hard to tell whether they were native Indian or not. 

The single character names like `A.`, `C.` or `K.` may select users that we don't want. You should remove those names from the list before using it to select the native Indian users.

You can do this by finding a regular expression that will find all the names with a single character followed by a `.`. The regular expression `[A-z]\\.` should do the trick. Combine the regular expression with the `grep` function to locate the names that you want to eliminate. These locations can be used to eliminate just the names you don't want.


*** =instructions
- Use `grep` and the regular expression `[A-z]\\.` to locate the names you want to eliminate
- Double check that those are the right names
- Remove the unwanted names from the `indain_names` list
- Display a table of the cleaned names list

*** =hint
When loading the names don't change the sample_code! Just remove the `#`

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.RData"))
```

*** =sample_code
```{r, eval = FALSE}
# Locate the names that you want to eliminate
indian_names_remove = grep("[A-z]\\.",indian_names, perl = TRUE)

# Check to make sure they are the correct names
indian_names[indian_names_remove]

# Eliminate them from the indian_names list
indian_names_clean <- indian_names[-indian_names_remove]

# Table
table(indian_names_clean)

#indian_names_clean <- indian_names[-grep("[A-z]\\.",indian_names, perl = TRUE)]

```

*** =solution
```{r,eval=FALSE}
# Locate the names that you want to eliminate
indian_names_remove = grep("[A-z]\\.",indian_names, perl = TRUE)

# Check to make sure they are the correct names
indian_names[indian_names_remove]

# Eliminate them from the indian_names list
indian_names_clean <- indian_names[-indian_names_remove]

# Table
table(indian_names_clean)

#indian_names_clean <- indian_names[-grep("[A-z]\\.",indian_names, perl = TRUE)]

```

*** =sct
```{r,eval=FALSE}
# Fist instruction

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```


--- type:NormalExercise xp:100 skills:1,3  key:69423673cb
## Finding Authentic Users
 

*** =instructions
- Use `scan()` to load in the `indian_names.txt` file
- Display the first 10 names with `head()`

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
```{r, eval = FALSE}
# Subset the `indian` data set to just the users with native Indian names
authentic_users = subset(indian,indian$user_name %in% indian_names_clean)

# Table
table(authentic_users$user_name)
```

*** =solution
```{r,eval=FALSE}
# Subset the `indian` data set to just the users with native Indian names
authentic_users = subset(indian,indian$user_name %in% indian_names_clean)

# Table
table(authentic_users$user_name)

# Find the number of users
number_authentic_city = authentic_users %>%
  select(city,user_name) %>%
  group_by(city) %>%
  summarise(users = n())

```

*** =sct
```{r,eval=FALSE}
# Fist instruction

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
authentic_users = subset(indian,indian$user_name %in% indian_names_clean)

library(dplyr)

number_authentic_city = authentic_users %>%
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



*** =instructions

*** =hint

*** =pre_exercise_code
```{r,eval=FALSE}
library(dplyr)
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/authentic_users.RData"))
names(authentic_users)
```

*** =sample_code
```{r, eval = FALSE}
names(authentic_users)
# Generate new "immigrant" rating
avg_review_indian <- authentic_users %>% 
    select(business_id, business_name, city, stars,
         avg_stars, is_indian, user_name) %>%
    group_by(city, business_name, avg_stars) %>%
    summarise(count = n(),
    new_stars = sum(stars) / count) %>%
    mutate(dif = new_stars - avg_stars)

```

*** =solution
```{r,eval=FALSE}
# Generate new "immigrant" rating
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
# Fist instruction

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```


--- type:NormalExercise xp:100 skills:1,3  key:03314d8871
## Detecting Manipulation Effect 



*** =instructions


*** =hint


*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/avg_review_indian.RData"))
```

*** =sample_code
```{r, eval = FALSE}
# Plots
#save(avg_review_indian, file = "avg_review_indian.RData")


hist(avg_review_indian$avg_stars)
hist(avg_review_indian$new_stars)
# Find out extent of effect of new rating
summary(avg_review_indian$dif)

# Plot the distribution of changes to ratings 
hist(avg_review_indian$dif, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes to per restaurant 
qplot(reorder(avg_review_indian$business_name,avg_review_indian$dif),avg_review_indian$dif, xlab = "", ylab = "Changes in Star Rating")

# Display a summary of the 
summary(avg_review_indian)


```

*** =solution
```{r,eval=FALSE}
# Plots
hist(avg_review_indian$ias)
hist(avg_review_indian$avg)

# Find out extent of effect of new rating
summary(avg_review_indian$dif)
```

*** =sct
```{r,eval=FALSE}
# Fist instruction

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```



