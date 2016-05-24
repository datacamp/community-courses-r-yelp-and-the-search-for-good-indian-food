---
title_meta  : Chapter 1
title       : Springboard Yelp Analysis
description : "Springboard Yelp Analysis"

--- type:NormalExercise xp:100 skills:1 key:70e19e0e7d
## Quick intro to DataCamp

Welcome to our tutorial based on the popular [Springboard blog post](https://www.springboard.com/blog/eat-rate-love-an-exploration-of-r-yelp-and-the-search-for-good-indian-food) about Yelp Review Modifications. Here you will learn how the author tailored the Yelp star reviews for restaurants to provide more useful information when deciding where to eat. In case you're new to R, it's recommended that you first take our free [Introduction to R Tutorial](https://www.datacamp.com/courses/free-introduction-to-r).

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

--- type:NormalExercise xp:100 skills:1  key:0d1199072c
## Exploring the data

For this course, the data comes in three separate data sets. 

- The first is labeled `reviews` and it contains `user_id's`, `business_id's` and `star` reviews.
- The second is labeled `users` and it is a list of `user_id's` and `user_names's`
- The last is labeled `businesses` and it is a contains information about the businesses on yelp like the business location, the category of food, the number of reviews and the average star review.

They have been loaded into the environment already and are ready to be explored!

*** =instructions
- Explore the `reviews` data set with `summary()` function.
- Explore the `users` data set with `summary()` function.
- Explore the `businesses` data set with `summary()` function.

*** =hint
Don't forget to look at all three data sets.

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/Springboard.yelp.datasets.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Explore the `reviews` data eset with `summary()` 
summary()

# Explore the `users` data set with `summary()` 
summary()

# Explore the `businesses` data set with `summary()` 
summary()
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
test_function("summary",args = c("object"), index = 1, args_not_specified_msg = msg1)

# second instruction
msg2 <- "Did you remember to take a look at the `users` data set?"
#test_output_contains("summary(users)", incorrect_msg = msg2)
test_function("summary",args = c("object"),index = 2, args_not_specified_msg = msg2)

# third instruction
msg3 <- "Did you remember to take a look at the `businesses` data set?"
#test_output_contains("summary(businesses)", incorrect_msg = msg3)
test_function("summary",args = c("object"), index = 3, args_not_specified_msg = msg3)

# General
test_error()
success_msg("Good job! We've seen a little more about the data so now let's move on!")

```

--- type:NormalExercise xp:100 skills:1,3  key:a72c7124db
## Combining data into one

Before manipulating the Yelp star reviews, you first need to combine the three data sets that were just explored so you can understand and adapt the data more effectively. 

The data sets from the previous exercise, `reviews`, `users`, and `businesses`, are data frames, R's way of representing a data set. You can combine a data frame in many ways, but for this exercise you don't want any missing data, let's say a business without a review. So you will use the `inner_join()` function from the `dplyr` package to combine the three data sets. The function `inner_join()` combines two data sets by finding columns with identical labels and then only combining the rows that are found in both independent data sets. 

Let's see how it works!

The 3 data frames are already loaded into your R environment. Apply `inner_join()` to the `reviews` and the `users` data sets first. Don't forget to name that newly combined data set. Next, apply `inner_join()` again but with the newly created data set and the final data set from the previous exercise `businesses`.

Once the data sets have been combined it can be helpful to explore the data some. Using `summary` you can get a better feel for the variables that are in out data and the types data you have to use. 

*** =instructions
- The code provided uses `library()` to load `dplyr` to the environment
- Use `inner_join()` to combine the `reviews` and `users` data sets and assign to `ru`.
- Use `inner_join()` to combine the newly created `ru` and `businesses` data sets and assign new data frame to `rub`. 
- Inspect new data frame `rub`, take note of the variables and types of data.
  
*** =hint
The order of the `join` function is important! Look at the instructions for the correct order. 

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/Springboard.yelp.datasets.Rdata"))
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
msg1 <- "Make sure you combine the `reviews` and the `users` data sets in the correct order."
test_data_frame("ru",incorrect_msg = msg1)

# second instruction
msg2 <- "Make sure you combine the `ru` and `businesses` data sets in the correct order."
test_data_frame("rub",incorrect_msg = msg2)

# third instruction
msg3 <- "Somethings not right. Check your `summary()` code"
#test_output_contains("summary(rub)", incorrect_msg = msg3)
test_function("summary",args = c("object"), index = 1, incorrect_msg = msg3)

# General
test_error()
success_msg("Awesome! We've combined the data set, but let's keep moving.")

```

--- type:NormalExercise xp:100 skills:1,3 key:6a66494184
## Isolate Indian restaurants 

You may have noticed from the previous exercise, the data set `rub` is large and covers many genres of cuisine. It makes sense to compare restaurants of similar cuisine for obvious reasons, so in order to simplify the task of adapting Yelp reviews, you will only look at reviews for Indian restaurants. The modifications in this course will serve as a case study of how you could adapt other reviews from the various types of food that also exist on Yelp.      

With that said, you need to filter out all of the non-Indian reviews. To do this you will use a combination of `grepl()` and `subset()` to create a binary true/false column indicating whether that review was for an Indian restaurant. This column will allow you to filter out all reviews that are not for Indian restaurants.

*** =instructions
- Create binary true/false column `is_indian` for Indian-only restaurant reviews using `grepl()` and the `categories` column.
- Use `subset()` to filter out all non-Indian reviews and assign the remaining reviews to data frame `indian`.

*** =hint
Which column of the `rub` data set should you look for the type of food served at the restaurant?

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/rub.RData"))
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

--- type:MultipleChoiceExercise xp:50 skills:1  key:f48b5ed8a3
## How many reviews?

Now that you have created a simplified data set, you are almost ready to begin manipulating the star reviews. Take a moment to explore the new data set and answer the following question.

Take a look at the data set `indian` with `str()` and see how many reviews does our data set contain?

*** =instructions
- 1456
- 980
- 1238
- 1563
  
*** =hint
There first-row from the `str()` output indicates how many rows are in this data set. There is one review per row!    

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/indian.RData"))
```

*** =sct
```{r,eval=FALSE}
msg1 <- "Try again!"
msg2 <- "Not so good... Maybe have a look at the hint."
msg3 <- "Incorrect. Maybe have a look at the hint."
msg4 <- "Very good! You found the total. Let's start manipulating the star reviews!"
test_mc(correct = 4, feedback_msgs = c(msg1, msg2, msg3, msg4))
```

--- type:NormalExercise xp:100 skills:1,4 key:1b2e20ac0a
## Review modification method I

You now have a manageable data set with just one type of cuisine. It's time to begin adapting the Yelp star reviews to see if you can make them more meaningful. In this course, you will look into just two of the almost infinite ways one can scale and manipulate reviews. The first method is to create a new review that gives more weight to those who have reviewed more restaurants of the same cuisine. 

To do this start by creating a new data frame with the number of reviews each reviewer has made for the collection of Indian restaurants in the original data set.  

The new data frame will be created using the `select()`, `group_by()`, `%>%` and `summarize()` functions of the `dplyr` package. The `select()` function determines the columns that will be included in the new data frame. The `group_by()`, `%>%` and `summarise()` functions allow for separate summaries to be performed within the unique values of the variable being grouped.  

After making the data frame, explore it! Check out the range in numbers of reviews and also the average number of reviews per user.  

*** =instructions
- Create a new data frame `number_reviews_indian` by selecting columns: `user_id`, `user_name`, using `group_by` variable `user_id` and  `summarise()` with `n()` to create `total_reviews` column
- Print the table of `total_reviews`
- Show the average number of reviews per users by averaging the `total_reviews`

*** =hint
Did you `group_by()` the correct variable? Check the instructions again?

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/indian.RData"))
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

# Pring the average number of reviews per users
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

# Pring the average number of reviews per users
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

--- type:NormalExercise xp:100 skills:1,4 key:30db019cde
## Review modification method I Cont.

Before you create a weighted star review for each restaurant, add the `number_reviews_indian` to the larger data frame `indian`. 

Just like an earlier exercise, you don't want any missing data within our data set, so you will use the `inner_join` function to merge all the rows that are in both the `number_reviews_indian` and `indian` data frames.

*** =instructions
- Create a new data frame `indian_plus_number`
- Display column names to ensure that the `total_reviews` column was added

*** =hint
Which column of the `rub` data set should you look for the type of food served at the restaurant?

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/indian.RData"))

library(dplyr)

number_reviews_indian <- indian %>% 
  select(user_id, user_name) %>%
  group_by(user_id) %>% 
  summarise(total_reviews = n())

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
msg1 <- "Although there are many ways to achieve this, try using inner_join and if you are having trouble type ?inner_join in the console for more information. Are your arguements correct?"
test_function("inner_join",args = c("x","y"), index = 1, incorrect_msg = msg1)
test_data_frame("indian_plus_number", incorrect_msg = "Your newly created data frame seems off. Reread the instructions and try again.")

# second instruction
msg2 <- "You didn't display the coloumn names. Use the `names()` function. It is quick and straight forward. If you are having trouble type ?names in the console for more information."
test_function("names",args = c("x"), index = 1, not_called_msg = msg2)

# General
test_error()
success_msg("Good job! We've added a new column to the data. Let's use it in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1,4 key:3981380079
## Review modification method I Cont. 2

Use the combined data set, `indian_plus_number`, to create weighted star reviews for each user. To do this you will simply multiply the unweighted restaurant review variable `stars` by the total number of reviews variable `total_reviews` for each user.

This weighted star variable will allow us to generate weighted star reviews. 

Weighted star reviews for each restaurant are created by taking the sum of the `weighted_stars` variables and dividing them by the sum of the `total_reviews` variable for each user. This is accomplished using the `select()`, `group_by()`, `%>%` and `summarize()` functions of the `dplyr` package. 


*** =instructions
- Create a new column `weighted_stars` in the `indian_plus_number` data frame
- Use `select()`, `group_by()`, `%>%` and `summarize()` to generate new weighted reviews for each restaurant while also creating columns:<p> - Create a variable `cnt` that counts the number of reviews for each restaurant</p><p> - Calculate the previous average star review using the `stars` and the `cnt` variables</p><p> - Generate new star reviews by dividing the sum of the `weighted_stars` variable and the `sum` of the `total_reviews` variable</p><p> - Finally, compute the difference in the star reviews from by subtracting the new star reviews, `new`, and the previous average star reviews `avg`. Assign this variable to `diff`</p>

*** =hint
The `%>%` operators are important for `dplyr` piping. Do not eliminate any of these from the sample code. 

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/indian_plus_number.RData"))
library(dplyr)

```

*** =sample_code
```{r,eval=FALSE}
# Generate weighted_stars variable 
indian_plus_number$___ <- indian_plus_number$stars * indian_plus_number$total_reviews

# Create a new weighted review for each restaurant (Note: package dplyr is available to use)
new_review_indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = ___,
            avg = sum(___) / ___,
            new = sum(___) / sum(___),
            diff = ___ - ___)
```

*** =solution
```{r,eval=FALSE}
# Generate weighted_stars variable
indian_plus_number$weighted_stars <- indian_plus_number$stars * indian_plus_number$total_reviews

# Create a new weighted review for each restaurant (Note: package dplyr is available to use)
new_review_indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = n(),
            avg = sum(stars) / cnt,
            new = sum(weighted_stars) / sum(total_reviews),
            diff = new - avg)

```

*** =sct
```{r,eval=FALSE}
#first instruction

 test_correct({
   test_function("select", ".data", eval = FALSE, incorrect_msg = "Make sure to pass the `indian_plus_number` argument to the  `select()`.")
 },
 {
   test_function("select", ".data", eval = FALSE, incorrect_msg = "Make sure to pass the `indian_plus_number` argument to the  `select()`.")
 })

 test_correct({
   test_function("group_by", ".data", eval = FALSE, incorrect_msg = "Make sure to pass the `select` argument to `group_by()`.")
 },
 {
   test_function("group_by", ".data", eval = FALSE, incorrect_msg = "Make sure to pass the `select` argument to `group_by()`.")
 })

test_correct({
 test_function_result("summarise", incorrect_msg = "Have you correctly performed the `summarise()` operation? Double check instructions for the summary variables, `cnt`, `avg`, `new` and `diff`.")  
}, {
   test_function("summarise", ".data", eval = FALSE, incorrect_msg = "Make sure to pass the `group_by()` argument to `summarise()`.")
 })

test_data_frame("indian_plus_number", incorrect_msg = "There are some issues with how you generated the weighted stars, check your code.", undefined_cols_msg = "Did you assign the weighted star reviews to the correct column name?")

 test_student_typed("indian_plus_number$weighted_stars<- indian_plus_number$stars * indian_plus_number$total_reviews", not_typed_msg ="Did you assign the weighted star reviews to the correct column name?")

test_data_frame("new_review_indian", incorrect_msg = "The new data frame `new_review_indian` is not correct. Make sure the summary variables are all defined correctly. Check the instructions if you are having trouble.")

# General
test_error()
success_msg("Good job! We've created weighted reviews. Let's check them out in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1 key:4ad4885c8d
## Detecting modification effects

Now that you have new weighted star reviews for each restaurant, let's see if you can detect the effects of the modifications. 

To do so, you will make use of some a general `hist` plot and a `qplot` from the `ggplot2` package. These graphs will help us visualize the effect of your modification. Take note of the magnitudes of the changes and if there were any patterns in the distribution of the difference in star reviews.

A final summary of the `new_review_indian` will give context to how the reviews changed as well.

*** =instructions
- Make `ggplot2` available in the environment 
- Use `hist()` function and the `new_review_indian$diff` column to create the plot of the distribution.
- Use `geom_bar()` with the `new_review_indian$diff` to the plot the difference in star review per restaurant. Fill in the `x` enlargement with the `new_review_indian` data set and assign the `y` argument within the `aes()` to the `city` variable.  
- Display the summary of the `new_review_indian` data frame 

*** =hint
The `reorder()` function makes the graph a bit more appealing. If you need assistance type ?reorder into the console.

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/indian_plus_number.RData"))
library(dplyr)

indian_plus_number$weighted_stars <- indian_plus_number$stars * indian_plus_number$total_reviews

new_review_indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = n(),
            avg = sum(stars) / cnt,
            new = sum(weighted_stars) / sum(total_reviews),
            diff = new - avg) %>%
  ungroup() %>%
  arrange(diff)
```

*** =sample_code
```{r,eval=FALSE}
# Load the ggplot2 package into the environment
library(ggplot2)

# Plot the distribution of changes to reviews 
hist(new_review_indian$___, main = "Changes in Star Reviews", xlab = "Change")

# Plot the changes in review per restaurant 
ggplot(______, aes(x=1:nrow(new_review_indian), y=___, fill=city)) +
    geom_bar(stat="identity", position=position_dodge()) + 
    theme_classic() + scale_fill_grey() + xlab("Businesses ID") + ylab("Change in Star Review")

# Display a summary of the 
summary(___)

```

*** =solution
```{r,eval=FALSE}
# Load the ggplot2 package into the environment
library(ggplot2)

# Plot the distribution of changes to reviews 
hist(new_review_indian$diff, main = "Changes in Star Reviews", xlab = "Change")

# Plot the changes to per restaurant 
ggplot(new_review_indian, aes(x=1:nrow(new_review_indian), y=diff, fill=city)) +
    geom_bar(stat="identity", position=position_dodge()) + 
    theme_classic() + scale_fill_grey() + xlab("Businesses ID") + ylab("Change in Star Review")

# Display a summary of the 
summary(new_review_indian)

```

*** =sct
```{r,eval=FALSE}

# first instruction
msg1 <- "Fill in the varaible that is the change in star review."
test_function_v2("hist", "x", eval = FALSE, index = 1, 
                 incorrect_msg = msg1)

# second instruction
msg3 <- "There is something wrong with your `geom_bar()` plot. Fill in the `data` arguement and the `y` argument with the varaible that is the change in star review."
test_function_v2("ggplot", args = c("data"), eval = FALSE, index = 1, 
                 incorrect_msg = msg3)

test_function_v2("aes", args = c("x","y","fill"), eval = FALSE, index = 1, 
                 incorrect_msg = msg3, args_not_specified_msg = "Did you forget to specify the `y` argument?")

# third instruction
msg3 <- "Something went wrong with the `summary()` function. Check your code and run again."
test_function_v2("summary", "object", index = 1, 
                incorrect_msg = msg3)

# General
test_error()
success_msg("Good job! We've modified the Yelp star reviews with one method. Continue to the next chapter for the second method!")


```
