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

*** =hint
Don't forget to look at all three data sets

*** =pre_exercise_code
```{r,eval=FALSE}
# no pec
```

*** =sample_code
```{r, eval = FALSE}
# Read Indian names into a list
indian_names <- scan(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt"), what = character())
```

*** =solution
```{r,eval=FALSE}
# Read Indian names into a list
indian_names <- scan(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.txt"), what = character())
```

*** =sct
```{r,eval=FALSE}
# first instruction
msg1 = "Did you remember to take a look at the `reviews` data set?"
#test_output_contains("summary(reviews)", incorrect_msg = msg1)
test_function("summary",args = c("object"), index = 1, incorrect_msg = msg1)

# second instruction
msg2 = "Did you remember to take a look at the `users` data set?"
#test_output_contains("summary(users)", incorrect_msg = msg2)
test_function("summary",args = c("object"),index = 2, incorrect_msg = msg2)

# third instruction
msg3 = "Did you remember to take a look at the `businesses` data set?"
#test_output_contains("summary(businesses)", incorrect_msg = msg3)
test_function("summary",args = c("object"), index = 3, incorrect_msg = msg3)

# General
test_error()
success_msg("Good job! We've seen a little more about the data so now let's move on!")

```


--- type:MultipleChoiceExercise xp:50 skills:1,3  key:f48b5ed8a3
## How Many Reviews?

Now that you have created a simplified data set and are almost ready to begin manipulating the reviews take a moment to explore the new data set and answer the following question.

Take a look at the data set `indian` with `str()` and see how many reviews does our data set contain?

*** =instructions
- 1456
- 980
- 1238
- 1563
  
*** =hint
- There first row form the `str()` output indicates how many rows are in this data set. There is one review per row!  

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_names.RData"))
```

*** =sct
```{r,eval=FALSE}
msg1 <- "Try again!"
msg2 <- "Not so good... Maybe have a look at the hint."
msg3 <- "Incorrect. Maybe have a look at the hint."
msg4 <- "Very good! You found the total. Let's start manipulating the star reviews!"
test_mc(correct = 4, feedback_msgs = c(msg1, msg2, msg3, msg4))
```
