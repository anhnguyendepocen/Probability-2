---
title: "MS 204 First Lab"
author: "PUT YOUR NAME HERE"
date: "Thursday, January 22"
output: html_document
---

# Lab 2

Today in lab, we will talk more about Bayes' Theorem, We will have a brief introduction to loops, and then you will start looking at examples 


#### Loops

Often, we would like to repeat a procedure many times.  For example, let's say that I wanted to find what n! is equal to.  I could use a `for` loop to do this.  `for` loops use a sequence of objects, and will complete the procedure within the loop for each value in the sequence:


```r
n<- 5             # set value for n
n.factorial<-1    # initialize value of n.factorial  
for(i in 1:n){
  n.factorial<-n.factorial*i
  print(n.factorial)
}
```

```
## [1] 1
## [1] 2
## [1] 6
## [1] 24
## [1] 120
```

Or maybe we want to know what the product of the first n even integers:


```r
n<- 5             # set value for n
n.product.even<-1    # initialize value of n.product.even  
for(i in (2*1:n)){
  n.product.even<-n.product.even*i
  print(n.product.even)
}
```

```
## [1] 2
## [1] 8
## [1] 48
## [1] 384
## [1] 3840
```

There is another kind of loop called a `while` loop.  The `while` loop will repeat until the parenthetical condition is true.  When the condition is false, the `while` loop will stop.

We could also use a `while` loop to find n!  


```r
n<- 5             # set value for n
n.factorial<-1    # initialize value of n.factorial  
counter<-1        # initialize value of counter
while(counter < n+1){
  n.factorial<-n.factorial*counter
  counter<-counter+1
  print(n.factorial)
}
```

```
## [1] 1
## [1] 2
## [1] 6
## [1] 24
## [1] 120
```

Or we could use a `while` loop to determine if a number n is a prime number:


```r
n<-999         #is this prime?
counter<-2
prime<-TRUE
first.factor<-NULL

while(prime==TRUE & counter<n){
  if (n/counter== floor(n/counter))
      {prime<-FALSE
       first.factor<-counter
       }
  counter<-counter+1
}

if (prime==TRUE){
  noquote(paste(n ,"is a prime number."))  
}else {
  noquote(paste(n, "is not a prime number.", n, "is divisible by", first.factor, "."))
}
```

```
## [1] 999 is not a prime number. 999 is divisible by 3 .
```



#### Exercise 1

In the code below, we simulate choosing a coin at random from 3 coins, and then flipping the coin using a `while` loop.  The three coins are each different in important ways.  One coin is fair (meaning it has a head and a tails), one coin is 2-headed, and one coin is 2-tailed.  After choosing the coin and then flipping it, we see that we have flipped a heads.  Without looking at the other side of the coin, we want to figure out: What is the probability the coin is 2-headed? 


```r
n <- 50000 
counter <- 0
data <- c(0,0,0)  # Stores number of times coin is fair, 2-h, 2-t

while (counter < n)
{
  coin <- sample(c(1, 2, 3), 1) ### Pick a coin at random
	p <- c(.5, 1, 0)[coin]   ### p = Prob(Heads) for the coin picked
	cointoss <- sample(0:1, size=1, prob=c(1-p,p)) 
			## Flip coin with 1-p - P(Tails), p = P		(Heads)	                			
      ## cointoss = 1 for heads, 0 for tails
	if (cointoss == 1) ### Check if heads 
	                     ### If not, skip through and flip again
	                     ### If yes, keep track of which coin was tossed 
	{
	data[coin] <- data[coin]+1
	counter <- counter + 1
	}
}

### Simulated result
Coin <- c("Fair", "2-Heads", "2-Tails")
data.frame(Coin, data/n)
```

```
##      Coin  data.n
## 1    Fair 0.33624
## 2 2-Heads 0.66376
## 3 2-Tails 0.00000
```

What probability do you get that the coin is fair, 2-headed, or 2-tailed?  

What is the conditional probability that the coun is 2-headed, given that the coin landed heads?

[INSERT YOUR ANSWER FOR EXERCISE 1 HERE]


#### Exercise 2.

The code below simulates rolling one six-sided dice and then another six-sided dice.  We know that the total of the dice ended up being 7, and now we want to know the probability that the first dice rolled a two.  


```r
n <- 10000 
counter <- 0
simlist <- numeric(n) ## Initialize list with 0's
while (counter < n)
{
  trial <- sample(1:6, 2, replace=TRUE) ## Roll 2 dice
  if (sum(trial) == 7) ### Check if sum is 7
	                     ### If not, skip through and roll again
	                     ### If 7, check if first die is a 2 
	{
	success <- if (trial[1] == 2) 1 else 0
	counter <- counter + 1
	simlist[counter] <- success
	### simlist records successes and failures only for
	###   dice rolls that sum to 7
	}
}

### Simulated result
mean(simlist)
```

```
## [1] 0.1652
```

What is the simulated conditional probability that you rolled a two on the first dice given that the total of the dice equals 7?  Do you think that if you roll a two for the first dice gives you a hint as to whether the sum of the two dice is 7?  Explain why or why not.

[INSERT YOUR ANSWER FOR EXERCISE 2 HERE]

#### Exercise 3

For this exercise, copy and paste the Conditional Dice Code Chunk (from Exercise 2), and then edit the code so that it simulates the probability that the two dice sum to seven given that the first dice rolled equals two.  What probability do you find?  Does this make sense to you?  Does this change your opinion of whether or not you rolling a two for the first dice gives you a hint as to whether the sum of the two dice is 7?  Explain why or why not.

[INSERT CODE CHUNK HERE FOR EXERCISE 3]

[INSERT ANSWERS TO QUESTIONS FOR EXERCISE 3 HERE]


