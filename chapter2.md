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

```
