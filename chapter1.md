---
title_meta  : Chapter 1
title       : Springboard Yelp Analysis
description : "Springboard Yelp Analysis"

--- type:NormalExercise xp:100 skills:1 key:70e19e0e7d
## Quick intro to DataCamp

Welcome to our tutorial based on the popular Springboard blog post [Blog post link] about Yelp Review Modifications. Here you will learn how the author tailored the Yelp star reviews for restaurants to provide more useful information when deciding where to eat. In case you're new to R, it's recommended that you first take our free [Introduction to R Tutorial](https://www.datacamp.com/courses/free-introduction-to-r).

In the editor on the right, you should type R code to solve the exercises. When you hit the 'Submit Answer' button, every line of code is interpreted and executed by R and you get a message whether or not your code was correct. The output of your R code is shown in the console in the lower right corner. R makes use of the `#` sign to add comments; these lines are not run as R code, so they will not influence your result.

You can also execute R commands straight in the console. This is a good way to experiment with R code, as your submission is not checked for correctness.

*** =instructions
- In the editor on the right, there is already some sample code. Can you see which lines are actual R code and which are comments?
- Add a line of code that calculates the sum of 8 and 15, and hit the 'Submit Answer' button.

*** =hint
Just add a line of R code that calculates the sum of 8 and 15, just like the example in the sample code!

*** =pre_exercise_code
```{r eval=FALSE}
# no pec
```

*** =sample_code
```{r eval=FALSE}
# Calculate 3 * 4
3 * 4

# Calculate 8 + 15


```

*** =solution
```{r eval=FALSE}
# Calculate 3 * 4
3 * 4

# Calculate 8 + 15
8 + 15
```

*** =sct
```{r eval=FALSE}
test_output_contains("12", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")

test_output_contains("3 * 4", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")

test_output_contains("23", incorrect_msg = "Make sure to add a line of R code, that calculates the sum of 8 and 15. Do not start the line with a `#`, otherwise, your R code will not be executed!")

test_output_contains("8 + 15", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")

success_msg("Awesome! See how the console shows the result of the R code you submitted? Now that you're familiar with the interface, let's get down to R business!")
```

--- type:NormalExercise xp:100 skills:1,3  key:0d1199072c
## Exploring the Data

For this course the data comes in three separate data sets. 

- The first is labeled `reviews` and it contains a `user_id`, a `business_id` and a `star` review.
- The second is labeled `users` and it is a list of `user_id's` and `user_names's`
- The last is labeled `businesses` and it is a contains information about the businesses on yelp like the business location, category of food, number of reviews and average star review.

They have been loaded into the environment already and are ready to be explored!

*** =instructions
- Explore the `reviews` data set with `summary()` function.
- Explore the `users` data set with `summary()` function.
- Explore the `businesses` data set with `summary()` function.

*** =hint
- Don't forget to look at all three data sets

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/Springboard.yelp.datasets.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Explore the `reviews` data eset with `summary()` 
summary(___)

# Explore the `users` data set with `summary()` 
summary(___)

# Explore the `businesses` data set with `summary()` 
summary(___)
```

*** =solution
```{r,eval=FALSE}
# Explore the `reviews` data set with `summary()` 
summary(reviews)

# Explore the `users` data set with `summary()` 
summary(users)

# Explore the `businesses` data set with `summary()` 
summary(businesses)

```

*** =sct
```{r,eval=FALSE}
# first instruction
msg1 <- "Did you remember to take a look at the `reviews` data set?"
#test_output_contains("summary(reviews)", incorrect_msg = msg1)
test_function("summary",args = c("object"), index = 1, incorrect_msg = msg1)

# second instruction
msg2 <- "Did you remember to take a look at the `users` data set?"
#test_output_contains("summary(users)", incorrect_msg = msg2)
test_function("summary",args = c("object"),index = 2, incorrect_msg = msg2)

# third instruction
msg3 <- "Did you remember to take a look at the `businesses` data set?"
#test_output_contains("summary(businesses)", incorrect_msg = msg3)
test_function("summary",args = c("object"), index = 3, incorrect_msg = msg3)

# General
test_error()
success_msg("Good job! We've seen a little more about the data so now let's move on!")

```

--- type:NormalExercise xp:100 skills:1,3  key:a72c7124db
## Combining data into one

Before manipulating the Yelp ratings, you first need to combine the three data sets that were just explored so you can understand and adapt the data more effectively. 

The data sets form the previous exercise, `reviews`, `users`, and `businesses`, are data frames, R's way of representing a dataset. You can combine a data frame in many ways, but for this exercise you don't want any missing data, let's say a business without a review. So you will use the `inner_join()` function from the `dplyr` package to combine the three data sets. The function `inner_join()` combines two data sets by finding columns with identical labels and then only combining the rows that are in both independent data sets. 

Let's see how it works!

The 3 data frames are already loaded into your workspace. Apply `inner_join()` to the `reviews` and the `users` data sets first. Don't forget to name that newly combined data set. Next apply `inner_join()` again but with the newly created data set and the final data set from the previous exercise `businesses`.

Once the data sets have been combined it can be helpful to explore the data some. Using `summary` you can get a better feel for the variables that are in out data and the types data you have to use. 


*** =instructions
- The code provided uses `library()` to load `dplyr` to the enironment
- Use `inner_join()` combine the `reviews` and `users` data sets and assign to `ru`.
- Use `inner_join()` combine the newly created `ru` and `businesses` data sets and assign new data frame to `rub`. 
- Inspect new data frame `rub`, take note of the variables and types of data.
  
*** =hint
-

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/Springboard.yelp.datasets.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Make dplry package avaiable to use
library(dplyr)

# Combine the reviews and users data sets
ru  <- inner_join(___, ___)

# combine the newly created data set with the businesses data set
rub <- inner_join(___, ___)

# Take a look at the combined data frame
summary(___)

```

*** =solution
```{r,eval=FALSE}
library(dplyr)

# Combine the reviews and users data sets
ru  <- inner_join(reviews, users)

# combine the newly created data set with the businesses data set
rub <- inner_join(ru, businesses)

# Take a look at the combined data frame
summary(rub)
```

*** =sct
```{r,eval=FALSE}
# first instruction
msg1 <- "Make sure you combine the `reviews` and the `users` data sets first"
#test_output_contains("ru  <- inner_join(reviews,users)", incorrect_msg = msg1)
test_function("inner_join",args = c("x","y"), index = 1, incorrect_msg = msg1)

# second instruction
msg2 <- "Make sure you combine the `ru` and `businesses` data sets"
#test_output_contains("rub  <- inner_join(ru,businesses)", incorrect_msg = msg2)
#test_function("inner_join",args = c("x","y"), index = 2, incorrect_msg = msg2)
test_data_frame("ru", eq_condition = "equal",incorrect_msg = msg2)

# third instruction
msg3 <- "Somethings not right. Check your `summary()` code"
#test_output_contains("summary(rub)", incorrect_msg = msg3)
test_function("summary",args = c("object"), index = 1, incorrect_msg = msg3)

# General
test_error()
success_msg("Awesome! We've combined the data set, but let's keep moving.")

```

--- type:NormalExercise xp:100 skills:1 key:6a66494184
## Isolate Indian restaurants 

As you noticed with the summary of `rub` from the previous exerceise, the data set is large and convers many genres of cuisine. It makes sense to compare restaurants of similar cuisine for obvious reasons, so in order to simplify the task of adapting Yelp reviews you will only look at reviews for Indian restaurants. This modifications in this course will serve as a case study of how you could adapt other reviews from the various types of food that also exist on Yelp.      

With that said, you need to filter out all of the non-Indian reviews. To do this you will use a combination of `grepl()` and `subset()` to create a binary true/false column indicating whether that review was for an Indian restaurant. This column will allow you to filter out all reviews that are not for Indian restaurants.

*** =instructions
- Create binary true/false column `is_indian` for Indian-only restaurant reviews using `grepl()`.
- Use `subset()` to filter out all non-Indian reviews and assign the remiaing reviews to data frame `indian`.

*** =hint
- Which column of the `rub` data set should you look for the type of food served at the restaurant

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/rub.RData"))
```

*** =sample_code
```{r,eval=FALSE}
# Create indian review column
rub$is_indian <- grepl("Indian", rub$___) == TRUE

# Select only reviews for Indian restaurants
_____ <- subset(rub, is_indian == TRUE)
```

*** =solution
```{r,eval=FALSE}
# Create indian review column
rub$is_indian <- grepl("Indian", rub$categories) == TRUE

# Select only reviews for Indian restaurants
indian <- subset(rub, is_indian == TRUE)

```

*** =sct
```{r,eval=FALSE}
# first instruction
msg1 <- "Although there are many ways to achieve this, try using grepl and if you are having trouble type ?grepl in the console for more information. Remember to search for Indian in the `categories` variable."
# test_output_contains("rub$is_indian <- grepl('Indian', rub$categories) == TRUE", incorrect_msg = msg1)
test_function("grepl", args = c("pattern","x"), index = 1, incorrect_msg = msg1)

# second instruction
msg2 <- "We know there are other ways to do this too, but subset can be quick and straight forward. If you are having trouble type ?subset in the console for more information."
test_function("subset", args = c("x","subset"), index = 1, incorrect_msg = msg2)
test_object("indian", incorrect_msg = msg2)

# General
test_error()
success_msg("Good job! We've selected jus the reviews for Indian restaurants so now let's move on!")
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
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian.RData"))
```

*** =sct
```{r,eval=FALSE}
msg1 <- "Try again!"
msg2 <- "Not so good... Maybe have a look at the hint."
msg3 <- "Incorrect. Maybe have a look at the hint."
msg4 <- "Very good! You found the total. Let's start manipulating the star reviews!"
test_mc(correct = 4, feedback_msgs = c(msg1, msg2, msg3, msg4))
```

--- type:NormalExercise xp:100 skills:1 key:1b2e20ac0a
## Review Modification Method I

Now that you have a manageable data set with just one type of cuisine it's time to begin adapting the Yelp star ratings to see if you can make them more meaningful. In this course you will look into just two of the almost infinite ways one can scale and manipulate ratings. The first method is to create a new rating that gives more weight to those who have reviewed more restaurants of the same cuisine. 

To do this start by creating a new data frame with the number of reviews each reviewer has made for the collection of Indian restaurants in the original data set.  

The new data frame will be created using the `select()`, `group_by()`, `%>%` and `summarize()` functions of the `dplyr` package. The `select()` function determines the columns that will be included in the new data frame. The `group_by()`, `%<%` and `summarized()` functions allow for separate summaries to be performed within the unique values of the variable being grouped.  

After making the data frame, explore it! Check out the range in numbers of reviews and also the average number of reviews per user.  

*** =instructions
- Create a new data frame `number_reviews_indian` by selecting columns: `user_id`, `user_name`, using `group_by` variable `user_id` and  `summarize()` with `n()` to create `total_reviews` column
- Print the table of `total_reviews`
- Show the average number of reviews per users by averaging the `total_reviews`

*** =hint
- Did you `group_by()` the correct vararable? Check the the insturctions again.

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian.RData"))
library(dplyr)
```

*** =sample_code
```{r,eval=FALSE}
# The package dplyr is available ot use
# Generate a new data frame with the number of reviews by each reviewer
number_reviews_indian <- indian %>% 
  select(___, ___) %>%
  group_by(___) %>% 
  summarise(total_reviews = n())

# Print the table of total_reviews
table(number_reviews_indian$___)

# Pring the avergare number of reviews per users
mean(number_reviews_indian$___)
```

*** =solution
```{r,eval=FALSE}
# The package dplyr is available ot use
# Generate a summary of # of reviews of that cuisine done by each reviewer
number_reviews_indian <- indian %>% 
  select(user_id, user_name) %>%
  group_by(user_id) %>% 
  summarise(total_reviews = n())

# Print the table of total_reviews
table(number_reviews_indian$total_reviews)

# Pring the avergare number of reviews per users
mean(number_reviews_indian$total_reviews)
```

*** =sct
```{r,eval=FALSE}
# first instruction
test_data_frame("number_reviews_indian", incorrect_msg = "Although this is not the only way to accomplish this task, using the dplry package is very efficient. If you are having trouble type ?dplyr in the console for more information.")

# second instruction
test_function("table", index = 1, incorrect_msg = "Something is wrong with your table. Check your code and type ?table into the console for more information")

# third instruction
test_function("mean", args = c("x"), index = 1, incorrect_msg = "Something is wrong with your mean calculation. Check your code and type ?mean into the console for more information")

# General
test_error()
success_msg("Good job! We've created a data frame with the number of reviews per user. Let's use it in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1 key:30db019cde
## Review Modification Method I Cont.

Before you create the weighted star rating, add the `number_reviews_indian` to the larger data frame `indian`. 

Just like an earlier exercise, you don't want any missing data within our data set, so you will use the `inner_join` function to merge all the rows that are in both the `number_reviews_indian` and `indian` data frames.

*** =instructions
- Create a new data frame `indian_plus_number`
- Display column names to ensure that the `total_reviews` column was added

*** =hint
- Which column of the `rub` data set should you look for the type of food served at the restaurant

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian.RData"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/number_reviews_indian.RData"))
library(dplyr)
```


*** =sample_code
```{r,eval=FALSE}
# The package dplyr is available to use
# Combine number of Indian reviews with original data frame of Indian restaurant reviews
indian_plus_number <- inner_join(___,number_reviews_indian)

# Display column names for the new data frame
indian_plus_number
```

*** =solution
```{r,eval=FALSE}
# The package dplyr is available to use
# Combine number of Indian reviews with original data frame of indian restaurant reviews
indian_plus_number <- inner_join(indian, number_reviews_indian)

# Display column names for the new data frame
names(indian_plus_number)

```

*** =sct
```{r,eval=FALSE}
# first instruction
msg1 <- "Although there are many ways to achieve this, try using inner_join and if you are having trouble type ?inner_join in the console for more information."
test_function("inner_join",args = c("x","y"), index = 1, incorrect_msg = msg1)
test_data_frame("indian_plus_number", incorrect_msg = "Your newly created data frame seems off. Reread the instructions and try again.")

# second instruction
msg2 <- "We know there are other ways to do this too, but names() can be quick and straight forward. If you are having trouble type ?names in the console for more information."
test_function("names",args = c("x"), index = 1, incorrect_msg = msg2)

# General
test_error()
success_msg("Good job! We've added a new coloumn to the data. Let's use it in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1 key:3981380079
## Review Modification Method I Cont. 2

Use the combined data set to create weighted star reviews for each user. To do this you will simply multiply the unweighted restaurant rating variable `stars` by the total number of reviews variable `total_reviews` for each user.

This weighted star variable will allow us to generate weighted star reviews. 

Weighted star reviews for each restaurant is created by taking to sum of the `weighted_stars` variables and dividing them by the sum of the `total_reviews` variable for each restuarant. This is accomplished using the the `select()`, `group_by()`, `%>%` and `summarize()` functions of the `dplyr` package. 


*** =instructions
- Create a new column `weighted_stars` in the `indian_plus_number` data frame
- Use `select()`, `group_by()`, `%>%` and `summarize()` to generate new weighted ratings for each restaurant while also creatng columns: `cnt = n()`, `avg = sum(stars) / cnt`, `dif = new - avg`

*** =hint
- 

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/indian_plus_number.RData"))
library(dplyr)
```

*** =sample_code
```{r,eval=FALSE}
# Generate "weighted_stars" variable 
indian_plus_number$___ <- indian_plus_number$stars * indian_plus_number$total_reviews

# Create a new weighted rating for each restaurant (Note: package dplyr is available to use)
new_review_indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = n(),
            avg = sum(stars) / cnt,
            new = sum(___) / sum(___),
            dif = (new - avg)



```

*** =solution
```{r,eval=FALSE}
# Generate "weighted_stars" for later calculation
indian_plus_number$weighted_stars <- indian_plus_number$stars * indian_plus_number$total_reviews

# Use "summarise" to generate a new rating for each restaurant
new_review_indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = n(),
            avg = sum(stars) / cnt,
            new = sum(weighted_stars) / sum(total_reviews),
            dif = new - avg)

```

*** =sct
```{r,eval=FALSE}
#first instruction
test_data_frame("indian_plus_number", incorrect_msg = "There are some issues with how you generated the weighted stars, check your code.")

# second instruction
test_data_frame("new_review_indian", incorrect_msg = "The new data frame `new_review_indian` is not correct. If you are having trouble type ?dplyr in the console for more information.")

test_function("group_by",args = c(".data"), index = 1, incorrect_msg = "Did you group the correct variable?. Check your code and type ?group_by into the console for more information")

# General
test_error()
success_msg("Good job! We've created weighted reveiws. Let's check them out in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1 key:4ad4885c8d
## Detecting Modification Effects

Now that you have new weighted star reviews for our restaurants, let's see if you can detect the effects of the modifications. 

To do so you will make use of some a general `hist` plot and a `qplot` from the `ggplot2` package. These graphs will help us visualize the effect of your modification. Take note of the magnitudes of the changes and if there were any patterns in the distribution of the difference in star ratings.

A final summary of the `new_review_indian` will give context to how the reviews changed as well.

*** =instructions
- Make `ggplot2` available in the environment 
- Use `hist()` function and the `new_review_indian$dif` column to create the plot of the distribution.
- Use `qplot()`, `new_review_indian$business_name` and `new_review_indian$dif` for the plot of the difference in star rating per restaurant. To create a more appealing graph use `reorder()` to order of changes from least to greatest. 
- Display the summary of the `new_review_indian` data frame 

*** =hint
- The `reorder()` function makes the graph a bit more appealing. If you need assistance type ?reorder into the console.

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1087/datasets/new_review_indian.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Load the ggplot2 package into the environment
library(ggplot2)

# Plot the distribution of changes to ratings 
hist(new_review_indian$___, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes in rating per restaurant 
qplot(reorder(new_review_indian$business_name,new_review_indian$dif),new_review_indian$__, xlab = "", ylab = "Changes in Star Rating")

# Display a summary of the 
summary(___)

```

*** =solution
```{r,eval=FALSE}
# Load the ggplot2 package into the environment
library(ggplot2)

# Plot the distribution of changes to ratings 
hist(new_review_indian$dif, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes to per restaurant 
qplot(reorder(new_review_indian$business_name,new_review_indian$dif),new_review_indian$dif, xlab = "", ylab = "Changes in Star Rating")

# Display a summary of the 
summary(new_review_indian)

```

*** =sct
```{r,eval=FALSE}

# second instruction
msg1 <- "Fill in the varaible that is the change in star rating."
test_function_v2("hist", "x", eval = FALSE, index = 1, 
                 incorrect_msg = msg1)

# third instruction
msg3 <- "Fill in the varaible that is the change in star rating."
test_function_v2("qplot", args = c("x","y"), eval = FALSE, index = 1, 
                 incorrect_msg = msg3)

# fourth instruction
msg3 <- "Something went wrong with the `summary()` function. Check your code and run again."
test_function_v2("summary", "object", index = 1, 
                 incorrect_msg = msg3)

# General
test_error()
success_msg("Good job! We've modified the Yelp star reviews with one method. Continue to the next chapter for the second method!")


```
