# codes are written in R studio
```r
# installing packages
install.packages("arules")
install.packages("arulesViz")
library(arules)
library(arulesViz) #For Visualization of Rules
```
```r
# reading the data
#Lets Import the Data3
book <- read.csv(file.choose())
#The Dataset is now Imported as a Data Frame. We will first See the Structure of the Data and make the Necessary Changes and then change it inta Transaction
#Association Rules can be done Only on Transactions

summary(book)
```
```r
# converting the data into categories
#The Whole Dataset is in form of Binary Variables. Lets Convert them All into Categorical Variables

book1 <- as.data.frame(lapply(book, as.factor))

#Now Lets Check the Structure of the Dataset
str(book1)
```
```r
# converting the data into transactions
#All the Variables have been converted into Categorical Variables.Lets Convert the data into Transaction
book2 <- as(book1, "transactions")

itemFrequencyPlot(book2, topN=22)#This will the Plot the Books in Descending Order(order wrt to transaction)
```
```r
# rules
rule1 <- apriori(book2, parameter = list(supp = 0.01, conf = 0.4, minlen = 5, maxlen = 10))
rule1 #Using the Above Parameters we have prepared 127070 rules for the Dataset

inspect(head(sort(rule1), n=15))
```
```r
# quality of rules
head(quality(rule1))
```

```r
# sorting of rules
#By lift
rule1_lift <- sort(rule1, by = "lift", descending = TRUE)
inspect(head(rule1_lift))

#by Confidence
rule1_confidence <- sort(rule1, by = "confidence", descending = TRUE)
inspect(head(rule1_confidence))
```
```r
# trying different rules

# rule 2
rule2 <- rules1 <- apriori(book1, parameter = list(supp = 0.05, confidence = 0.8,minlen = 6, maxlen = 20))
inspect(head(rule2, 10))
rule2 #We have 15855 set of rules
plot(rule2, method = "grouped")

# rule 3
rule3 <- apriori(book1, parameter = list(supp = 0.04, confidence = 0.6,minlen = 7, maxlen = 10))
inspect(head(rule2, 10))
rule3 #Set of 14572 rules Prepared
plot(rule3, method = "graph")

# rule 4
rule4 <- apriori(book1, parameter = list(supp = 0.06, confidence = 0.7,minlen = 8, maxlen = 15))
inspect(head(rule4, 10))
rule4 #Set of 4557 rules Prepared
plot(rule4, method = "paracoord")

# rule 5
rule5 <- apriori(book1, parameter = list(supp = 0.03, confidence = 0.85,minlen = 9, maxlen = 20))
inspect(head(rule5, 10))
rule5 #Prepared 2340 set of Rules
plot(rule5, method = "two-key plot")
```
```r
# plot top five rules
top5rules <- head(rule5, n=10, by = "confidence")
plot(top5rules, engine = "htmlwidget", method = "graph") 
```


