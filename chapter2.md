---
title_meta  : Chapter 2
title       : Springboard Yelp Analysis
description : "Springboard Yelp Analysis"

--- type:NormalExercise xp:100 skills:1,3  key:0d1199072c
## Exploring the Data

The second chapter of this tutorial will be an alternative method of manipulating the Yelp star reviews. You will be working with the same sample of reviews of Indian restaurants but adapting the star ratings in a different way. 

This method looks to adapt the star reviews with the perception that Yelp reviewers with Indian heritage would provide more accurate and authentic ratings for Indian cuisine. The strategy for manpulating the star reviews involves selecting only the reviewers with Indian names for the agregate restaurant star rating. 

This means that you need a way to select just the users with native Indian names and that is where this chapter begins! 

You will load in a list of native Indians names that can be used to sort the names of the users 


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
in_names_url = url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt")

# Read Indian names into a list
#indian_names <- scan(in_names_url, what = character())

# Show the first 10 names from the indian_names list
head(indian_names,___)

```

*** =solution
```{r,eval=FALSE}
# This url contains the .txt file with Indian names. (Note: Don't change this code)
in_names_url = url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt")

# Read Indian names into a list
indian_names <- scan(in_names_url, what = character())

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
```

*** =sample_code
```{r, eval = FALSE}
# Subset the `indian` data set to just the users with native Indian names
authentic_users = subset(indian,indian$user_name %in% indian_names)

# Table
table(authentic_users$user_name)

```

*** =solution
```{r,eval=FALSE}
# Subset the `indian` data set to just the users with native Indian names
authentic_users = subset(indian,indian$user_name %in% indian_names)

# Table
table(authentic_users$user_name)
```

*** =sct
```{r,eval=FALSE}
# Fist instruction

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```

--- type:MultipleChoiceExercise xp:50 skills:1,3  key:f48b5ed8a3
## How Many Indian names?

Now that you have created a simplified data set and are almost ready to begin manipulating the reviews take a moment to explore the new data set and answer the following question.

Take a look at the data set `indian` with `str()` and see how many reviews does our data set contain?

*** =instructions
- 67
- 76
- 56
- 121
  
*** =hint

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/authentic_users.RData"))
```

*** =sct
```{r,eval=FALSE}
msg1 <- "Try again!"
msg2 <- "Very good! You found the total. Let's user their star reviews!"
msg3 <- "Incorrect. Maybe have a look at the hint."
msg4 <- "Not so good... Maybe have a look at the hint."
test_mc(correct = 2, feedback_msgs = c(msg1, msg2, msg3, msg4))
```


--- type:NormalExercise xp:100 skills:1,3  key:cd888199f3
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
# Generate new "immigrant" rating
avg_review_indian <- authentic_users %>% 
  select(business_id, business_name, city, stars, 
  avg_stars, is_indian, istars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(count = n(),
            nin = sum(user_name),
            pin = sum(user_name) / n(),
            avg = sum(stars) / count,
            ias = sum(istars) / nin,
            dif = ias - avg)

```

*** =solution
```{r,eval=FALSE}
# Generate new "immigrant" rating
avg_review_indian <- authentic_users %>% 
  select(business_id, business_name, city, stars, 
  avg_stars, is_indian, istars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(count = n(),
            nin = sum(user_name),
            pin = sum(user_name) / n(),
            avg = sum(stars) / count,
            ias = sum(istars) / nin,
            dif = ias - avg)

```

*** =sct
```{r,eval=FALSE}
# Fist instruction

# General
test_error()
success_msg("Well done! Now that your data is loaded in, you can start exploring it!")
```


--- type:NormalExercise xp:100 skills:1,3  key:cd888199f3
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
hist(avg_review_indian$ias)
hist(avg_review_indian$avg)

# Find out extent of effect of new rating
summary(avg_review_indian$dif)

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



