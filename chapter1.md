---
title_meta  : Chapter 1
title       : Springboard Yelp Analysis
description : "Springboard Yelp Analysis"

--- type:NormalExercise xp:100 skills:1 key:70e19e0e7d
## Quick intro to DataCamp

Welcome to COURSE NAME

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

test_student_typed("3", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")
test_student_typed("*", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")
test_student_typed("4", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")

test_output_contains("23", incorrect_msg = "Make sure to add a line of R code, that calculates the sum of 8 and 15. Do not start the line with a `#`, otherwise, your R code will not be executed!")

test_student_typed("8", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")
test_student_typed("+", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")
test_student_typed("15", incorrect_msg = "Do not remove the line of R code that calculates the product of 3 and 4. Instead, just add another line that calculates the sum of 8 and 15.")

success_msg("Awesome! See how the console shows the result of the R code you submitted? Now that you're familiar with the interface, let's get down to R business!")
```

--- type:NormalExercise xp:100 skills:1,3  key:0d1199072c
## Exploring the Data

For this course the data comes in three separate data sets.

- The first is labeled `reviews` and it contains `user_id's`, `business_id's` and `star` reviews.
- The second is labeled `users` and it is a list of `user_id's` and `user_names's`
- The last is labeled `businesses` and it is a contains information about the businesses on yelp like the business location, the category of food, the number of reviews and the average star review.

They have been loaded into the environment already and are ready to be explored!

*** =instructions
- Explore each data sets with `summary()` function.

*** =hint
- Don't forget to look at all three data sets

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/Springboard_Yelp_ch1ex1.Rdata.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Explore the `reviews` data set with `summary()` 
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
test_output_contains("summary(reviews)", incorrect_msg = "Did you remember to take a look at the reviews data set?")
test_function("summary")

# second instruction
test_output_contains("summary(users)", incorrect_msg = "Did you remember to take a look at the reviews data set?")
test_function("summary")

# third instruction
test_output_contains("summary(businesses)", incorrect_msg = "Did you remember to take a look at the reviews data set?")
test_function("summary")

# General
test_error()
success_msg("Good job! We've seen a little more about the data so now let's move on!")

```

--- type:NormalExercise xp:100 skills:1,3  key:a72c7124db
## Combining data into one

Before we start manipulating Yelp ratings, we first need to combine the three data sets we just explored so we can understand and adapt the data more effectively. 

The data sets form the previous exercise, `reviews`, `users`, and `businesses`, are data frames, R's way of representing a dataset. We can combine a data frame in many ways, but for this exercise we don't want any missing data, let's say a business without a review. So we will use the `inner_join()` function from the 'dplyr' package to combine the three data sets. The function `inner_join()` combines two data sets by finding columns with identical labels and then only combining the rows that are in both independent data sets. 

Let's see how it works!

The 3 data frames are already loaded into your workspace. Apply `inner_join()` to the `reviews` and the `users` data sets first. Don't forget to name that newly combined data set. Next apply `inner_join()` again but with the newly created data set and the final data set from the previous exercise `businesses`.

Once the data sets have been combined it can be helpful to explore the data some. Using `summary` we can get a better feel for the variables that are in out data and the types data we have to use. 


*** =instructions
- Use `inner_join()` combine the `reviews` and `users` data set.
- Assign new data frame to `ru`.
- Use `inner_join()` combine the newly created `ru` and `businesses` data set
- Assign new data frame to `rub`. 
- Inspect new data frame `rub`, take note of the variables and types of data.
  
*** =hint
-

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course__/datasets/Springboard_Yelp_ch1ex1.Rdata.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
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
test_output_contains("ru  <- inner_join(reviews,users)", incorrect_msg = "Make sure you combine the reviews and the users data sets first")
test_function("inner_join")

# second instruction
test_output_contains("rub  <- inner_join(ru,businesses)", incorrect_msg = "Make sure you combine the reviews and the users data sets first")
test_function("inner_join")

# third instruction
test_output_contains("summary(rub", incorrect_msg = "Somethings not right. Check your summary() code")
test_function("summary")

# General
test_error()
success_msg("Awesome! We've combined the data set, but let's keep moving.")

```

--- type:NormalExercise xp:100 skills:1 key:6a66494184
## Isolate Indian restaurants 

Following the direction of the Springboard blog post [Blog post link], we will simplify the task of adapting Yelp reviews by looking only at Indian restaurants. It makes sense to compare restaurants of similar cuisine for obvious reasons and we will stick with Indian food to follow the authors original work. 

With that said, we need to filter out all of the non-Indian reviews. To do this we will use a combination of `grepl()` and `subset()` to create a binary true/false column indicating whether that review was for an Indian restaurant. This column will allow us to filter out all reviews that are not for Indian restaurants.

*** =instructions
- Create binary true/false column `is_indian` for Indian-only restaurant reviews using `grepl()`.
- Use `subset()` to filter out all non-Indian reviews.
- Save the subset of reviews to data frame `indian`.

*** =hint
- Which column of the `rub` data set should we look for the type of food served at the restaurant

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/rub.Rdata"))
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
test_output_contains("rub$is_indian <- grepl('Indian', rub$categories) == TRUE", incorrect_msg = "Although there are many ways to achieve this, try using grepl and if you are having trouble type ?grepl in the console for more information.")
test_function("grepl")

# second instruction
test_output_contains("indian <- subset(rub, is_indian == TRUE)", incorrect_msg = "We know there are other ways to do this too, but subset can be quick and straight forward. If you are having trouble typle ?subset in the console for more information.")
test_function("subset")

# General
test_error()
success_msg("Good job! We've seen a little more about the data so now let's move on!")
```

--- type:MultipleChoiceExercise xp:50 skills:1,3  key:f48b5ed8a3
## How Many Reviews?

Now that we have created a simplified data set and are almost ready to begin manipulating the reviews lets take a moment to explore the new data set and answer the following question.

Take a look at the data set with `summary()` and see how many reviews does our data set contain?

*** =instructions
- 1456
- 980
- 1238
- 1563
  
*** =hint
- There are two outputs form the summary that indicate how many reviews are in this data set.  

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course_1073/datasets/indian.Rdata"))
```

*** =sct
```{r,eval=FALSE}
msg1 <- "Try again!"
msg2 <- "Not so good... Maybe have a look at the hint."
msg3 <- "Incorrect. Maybe have a look at the hint."
msg4 <- "Very good! You found the total ."
test_mc(correct =4, feedback_msgs = c(msg1, msg2, msg3, msg4))
```

--- type:NormalExercise xp:100 skills:1 key:1b2e20ac0a
## Review Modification Method I

Now that we have a manageable data set with just one type of cuisine we can begin to adapt the Yelp star ratings to see if we can make them more meaningful. In this course we will look into just two of the almost infinite ways one can scale and manipulate ratings. The first method is to create a new rating that gives more weight to those who have reviewed more restaurants of the same cuisine. 

To do this we will start by creating a new data frame with the number of reviews each reviewer has made for the collection of Indian restaurants in the original data set.  

The new data frame will be created using the `select()`, `group_by()`, `%>%` and `summarize()` functions of the `dplyr` package. The `select()` function determines the columns that will be included in the new data frame. The `group_by()`, `%<%` and `summarized()` functions allow for separate summaries to be performed within the unique values of the variable being grouped.  

After making the data frame, explore it! Check out the range in numbers of reviews and also the average number of reviews per user.  

*** =instructions
- Create a new data frame `number_reviews_Indian`
- Include columns: `user_id`, `user_name`, `is_indian`
- Group_by `user_id`
- Use `summarize()` and `sum()` to create `total_reveiws` column
- Print the table of total_reviews
- Show the average number of reviews per users

*** =hint
- Which column of the `rub` data set should we look for the type of food served at the restaurant

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/indian.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Generate a new data frame with the number of reviews by each reviewer
# DO WE NEED THE IS_INDIAN COLUMN
number_reviews_Indian <- indian %>% 
  select(user_id, user_name, is_indian) %>%
  group_by(user_id) %>% 
  summarise(total_reviews = sum(is_indian))

# Print the table and show the average number of reviews per user
table(number_reviews_Indian$___)
mean(number_reviews_Indian$___)
```

*** =solution
```{r,eval=FALSE}
# Generate a summary of # of reviews of that cuisine done by each reviewer
number_reviews_Indian <- indian %>% 
  select(user_id, user_name, is_indian) %>%
  group_by(user_id) %>% 
  summarise(total_reviews = sum(is_indian))

# Print the table, show the total # of entries, and find the avg # of reviews per user
table(number_reviews_Indian$total_reviews)
mean(number_reviews_Indian$total_reviews)
```

*** =sct
```{r,eval=FALSE}
# first instruction
test_output_contains("number_reviews_Indian <- indian %>% 
  select(user_id, user_name, is_indian) %>%
  group_by(user_id) %>% 
  summarise(total_reviews = sum(is_indian))", incorrect_msg = "Although this is not the only way to accomplish this task, using the dplry package is very efficient. If you are having trouble type ?dplyr in the console for more information.")

# second instruction
test_output_contains("table(number_reviews_Indian$total_reviews)", incorrect_msg = "Something is wrong with your table. Check your code and type ?table into the console for more information")
test_function("table")

# third instruction
test_output_contains("mean(number_reviews_Indian$total_reviews)", incorrect_msg = "Something is wrong with your calculations with te mean. Check your code and type ?mean into the console for more information")
test_function("mean")

# General
test_error()
success_msg("Good job! We've added a new coloumn to the data. Let's use it in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1 key:30db019cde
## Review Modification Method I Cont.
We can use the new data frame to create a weighted star rating. To do so we need to combine the `number_reviews_Indian` data frame with the `indian` data frame.

As before, we don't want any missing data within our data set, so we will use the `inner_join` function to merge all the rows that are in both the `number_reviews_Indian` and `indian` data frames.

*** =instructions
- Create a new data frame `indian_plus_number`
- Display column names to ensure that the `total_reviews` column was added

*** =hint
- Which column of the `rub` data set should we look for the type of food served at the restaurant

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/indian.Rdata"))
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/number_reviews_Indiam.Rdata"))
```

Ended SCTs here

*** =sample_code
```{r,eval=FALSE}
# Combine num_reviews information with original data frame of indian restaurant reviews
indian_plus_number <- inner_join(___,number_reviews_Indian)

# Display column names for the new data frame
indian_plus_number
```

*** =solution
```{r,eval=FALSE}
# Combine num_reviews information with original data frame of indian restaurant reviews
# Should we left join rather than inner_join
indian_plus_number <- inner_join(indian, number_reviews_Indian)

# Display column names for the new data frame
names(indian_plus_number)

```

*** =sct
```{r,eval=FALSE}
# first instruction
test_output_contains("rub$is_indian <- grepl("Indian", rub$categories) == TRUE", incorrect_msg = "Although there are many ways to achieve this, try using grepl and if you are having trouble type ?grepl in the console for more information.")
test_function("grepl")

# second instruction
test_output_contains("indian <- subset(rub, is_indian == TRUE)", incorrect_msg = "We know there are other ways to do this too, but subset can be quick and straight forward. If you are having trouble typle ?subset in the console for more information.")
test_function("subset")

# General
test_error()
success_msg("Good job! We've added a new coloumn to the data. Let's use it in the next exercise!")

```

--- type:NormalExercise xp:100 skills:1 key:3981380079
## Review Modification Method I Cont. 2

With the combined data set we can now create weighted star reviews. To do this we will simply multiply the unweighted restaurant rating by the total number of reviews that particular user has given for that genre of cuisine. 

This weighted star variable will allow us to generate wieghted star reviews. 

Weighted star reviews for each restaurant is created by taking to sum of the weighted star variables and dividing htem by the sum of the total_reviews variable for each restuarant. This is accomplished using the the `select()`, `group_by()`, `%>%` and `summarize()` functions of the `dplyr` package. 


*** =instructions
- Create a new column `weighted_stars` in the `indian_plus_number` data frame
- Use `select()`, `group_by()`, `%>%` and `summarize()` to generate new weighted ratings for each restaurant
- Also create columns: `cnt = n()`, `avg = sum(stars) / cnt`, `dif = new - avg`

*** =hint
- 

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/indian_plus_number.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Generate "weighted_stars" 
indian_plus_number$weighted_stars <- indian_plus_number$stars * indian_plus_number$total_reviews

# Create a new weighted rating for each restaurant
new_rating_Indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = n(),
            avg = sum(stars) / cnt,
            new = sum(weighted_stars) / sum(total_reviews),
            dif = new - avg)

```

*** =solution
```{r,eval=FALSE}
# Generate "weighted_stars" for later calculation
indian_plus_number$weighted_stars <- indian_plus_number$stars * indian_plus_number$tot_rev

# Use "summarise" to generate a new rating for each restaurant
# Generate "weighted_stars" 
indian_plus_number$weighted_stars <- indian_plus_number$stars * indian_plus_number$total_reviews

# Use "summarise" to generate a new rating for each restaurant
new_rating_Indian <- indian_plus_number %>% 
  select(city, business_name, avg_stars, stars, total_reviews, weighted_stars) %>%
  group_by(city, business_name, avg_stars) %>%
  summarise(cnt = n(),
            avg = sum(stars) / cnt,
            new = sum(weighted_stars) / sum(total_reviews),
            dif = new - avg)

```

*** =sct
```{r,eval=FALSE}

```

--- type:NormalExercise xp:100 skills:1 key:4ad4885c8d
## Review Modification Method I Cont. 3

Now that we have new weighted star reviews for our restaurants, let's see if we can detect the effects of the modifications. 

Plot the distribution of the changes in the ratings. 




*** =instructions
- Use `hist()` function and the `new_rating_Indian$dif` column to create the plot of the distribution.
- Use `qplot()`, `new_rating_Indian$business_name` and `new_rating_Indian$dif` for the plot of the difference in star rating per restaurant. To create a more appealing graph use `reorder()` to order of changes from least to greatest. 
- Display the summary of the `new_rating_Indian` data frame 

*** =hint
- 

*** =pre_exercise_code
```{r,eval=FALSE}
load(url("http://s3.amazonaws.com/assets.datacamp.com/production/course1073/datasets/new_rating_Indian.Rdata"))
```

*** =sample_code
```{r,eval=FALSE}
# Plot the distribution of changes to ratings 
hist(new_rating_Indian$___, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes to per restaurant 
qplot(reorder(new_rating_Indian$business_name,new_rating_Indian$dif),new_rating_Indian$dif, xlab = "", ylab = "Changes in Star Rating")

#qplot(new_rating_Indian$new, binwidth = .20)

# Display a summary of the 
summary(new_rating_Indian)

```

*** =solution
```{r,eval=FALSE}
# Plot the distribution of changes to ratings 
hist(new_rating_Indian$___, main = "Changes in Star Ratings", xlab = "Change")

# Plot the changes to per restaurant 
qplot(reorder(new_rating_Indian$business_name,new_rating_Indian$dif),new_rating_Indian$dif, xlab = "", ylab = "Changes in Star Rating")

#qplot(new_rating_Indian$new, binwidth = .20)

# Display a summary of the 
summary(new_rating_Indian)

```

*** =sct
```{r,eval=FALSE}

```
