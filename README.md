# Frequent_ItemsetMining
Given a large set of data , frequent itemset mining helps us determine the set of items that mostly occur together.
This data mining technique is particularly useful in shopping, where the items that are frequently together are placed on adjacent aisles. It can also be used as a plagiarism detector tool to find the documents that are similar.
In this project , the algorithm we have used is the `PCY - Park Chen Yu algorithm`

### Steps of algorithm:
1. Extract all the individual items from each basket in the given dataset and calculate the number of times each has occurred.
2. Store all the items that have occurrence value greater than the support value. The support, is a threshold value , only the items appearing at least as many times as the support or more are considered as frequent . This comprises Pass 1 of the algorithm .
3. Since we need to find out the maximum number of frequent occurring items , that is pairs , triplets , quadruplets ...all itemsets up to size 99 , therefore for faster and efficient working of the algorithm we use a hash function .
4. The hash function we have chosen is H(i,j,...,n)=(i+j+...+n)%5. , where i,j,...,n stand for the items in the set . So for example for a set of size 3 , hash function will be H(i,j,k)=(i+j+k)%5 and so on.
5. The value returned from this function determines the bucket number for each of these sets.
6. The items are then placed accordingly in the buckets and the count of items in each bucket is calculated .
7. It is further decided which bucket is non-frequent based on the support value given. These non-frequent buckets can be removed as candidates because their elements will not be frequent and hence should not be included in the final answer.
8. Now , for Pass 2 , we only calculate the item sets that hash to the frequent buckets.
9. For itemsets in each basket we need to first find all the combinations of size 2 for pairs , 3 for triplets and so on. x`
10. Sort the numbers in each of these combinations to eliminate any repetitive itemsets.
11. For a frequent itemset, it should satisfy the following conditions:  
    * Each individual item in the itemset should be frequent.  
    * The hash value of the itemset should be a frequent bucket.  
12. Using the same procedure for itemsets of sizes up to 99 , we finally get all frequently occurring items in the given dataset .


### Optimization 
We started initially by implementing the Apriori algorithm, but it leads to a wastage of time and memory as candidates are generated every time for calculating the itemsets. In order to avoid this, we use the PCY algorithm where we maintain a hash table of the buckets in which each item set is hashed. In order to make sure that no itemsets are repeated we first sort the elements in each item set and only consider these sorted items while adding new items to it in the next iteration.
As per the project requirement, we need to display all frequent items and not just the frequent pairs, therefore we keep finding combinations up to the maximum size. Say for example if the given dataset has only one frequent item set of size four, then we do not check for further combinations for greater size as that is not possible. Furthermore, we noticed that the time is taken to make combinations increases exponentially with the increasing item set size, therefore, we analyzed the run time of our code on various datasets and figured out the size of itemsets beyond which it was not necessary to make combinations anymore. For these larger itemsets, we figured out that an apriori-like approach would give the result faster and hence, optimized the algorithm accordingly.

##### My role: 
* Implementing Apriori algorithm on that dataset for finding all frequent itemsets up to the max size possible as per the given data.
* Verifying the best hash function that should be used and figuring out a way of optimization to reduce the run time of code.

###### References: 
* http://cs.brown.edu/courses/cs195w/slides/freqitems.pdf  
* https://github.com/naoki-style/Apriori  
* http://infolab.stanford.edu/~ullman/mining/pdf/assoc-rules2.pdf  
* https://www.geeksforgeeks.org/apriori-algorithm/  
* Hector Garcia-Molina, Jeff Ullman, and Jennifer Widom. Database Systems, the Complete Book. Second Edition, Prentic-Hall, 2009  
