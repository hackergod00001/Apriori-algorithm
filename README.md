# Apriori-algorithm

## 1) Give limitations of Apriori algorithms
Answer:
    
    Apriori Algorithm can be slow.
    The algorithms scans the database too many time which reduces its overall performance.
     i.e. it is not an efficient approach for large number of datasets
     
    For example, if there are 10^4 from frequent 1- itemsets, it need to generate more than 10^7 candidates into 2-length which in turn they will be tested and accumulate. Furthermore, to detect frequent pattern in size 100 i.e. v1, v2… v100, it have to generate 2^100 candidate itemsets that yield on costly and wasting of time of candidate generation. So, it will check for many sets from candidate itemsets, also it will scan database many times repeatedly for finding candidate itemsets. Apriori will be very low and inefficiency when memory capacity is limited with large number of transactions. 
     
## 2) Write different variations of FP tree algorithm
Answer:
      
      FP Tree
      Frequent Pattern Tree is a tree-like structure that is made with the initial itemsets of the database. The purpose of the FP tree is to mine the most frequent pattern. Each node of the FP tree represents an item of the itemset.

      The root node represents null while the lower nodes represent the itemsets. The association of the nodes with the lower nodes that is the itemsets with the other itemsets are maintained while forming the tree.
      
      As the popularity and efficiency of FP-Growth Algorithm contributes with many studies that propose variations to improve its performance. some of them are briefly described belowz:
      
    - DynFP-Growth Algorithm
      The DynFP-Growth, has focused in improving the FP-Tree algorithm construction based on two observed problems:
            1.) The resulting FP-tree is not unique for the same “logical” database;
            2.) The process needs two complete scans of the database.
      An important feature in this approach is that it's not necessary to rebuild the FP-Tree when the actual database is updated. It's only needed to execute the algorithm again taking into consideration the new transactions and the stored FP-Tree.

      Another adaptation proposed, because of the dynamic reordering process, is a modification in the original structures, by replacing the single linked list with a doubly linked list for linking the tree nodes to the header and adding a master-table to the same header. 
      
      - FP-Bonsai Algorithm
      The FP-Bonsai improve the FP-Growth performance by reducing (pruning) the FP-Tree using the ExAnte data-reduction technique. The pruned FP-Tree was called FP-Bonsai.
      
      - AFOPT Algorithm
      Investigating the FP-Growth algorithm performance Liu proposed the AFOPT algorithm in. This algorithm aims at improving the FP-Growth performance in four perspectives:

           - Item Search Order: when the search space is divided, all items are sorted in some order. The number of the conditional databases constructed can differ very much using different items search orders;
           - Conditional Database Representation: the traversal and construction cost of a conditional database heavily depends on its representation;
           - Conditional Database Construction Strategy: constructing every conditional database physically can be expensive affecting the mining cost of each individual conditional database;
           - Tree Traversal Strategy: the traversal cost of a tree is minimal using top-down traversal strategy.
       
       - NONORDFP Algorithm
       The Nonordfp algorithm was motivated by the running time and the space required for the FP-Growth algorithm. The theoretical difference is the main data structure (FP-Tree), which is more compact and which is not needed to rebuild it for each conditional step. A compact, memory efficient representation of an FP-tree by using Trie data structure, with memory layout that allows faster traversal, faster allocation, and optionally projection was introduced. 
       
       - FP-Growth* Algorithm
       This algorithm was proposed by Grahne et al., and is based in his conclusion about the usage of CPU time to compute frequent item sets using FP-Growth. They observed that 80% of CPU time was used for traversing FP-Trees. Therefore, they used an array-based data structure combined with the FP-Tree data structure to reduce the traversal time, and incorporates several optimization techniques.
       
       - PPV, PrePost, and FIN Algorithm
       These three algorithms were proposed by Deng et al., and are based on three novel data structures called Node-list, N-list, and Nodeset respectively for facilitating the mining process of frequent itemsets. They are based on a FP-tree with each node encoding with pre-order traversal and post-order traversal. Compared with Node-lists, N-lists and Nodesets are more efficient. This causes the efficiency of PrePost and FIN is higher than that of PPV.

      
      
## 3) Explain FP tree Algorithms with one example
Answer:
    
    The frequent pattern growth method lets us find the frequent pattern without candidate generation.

    Let us see the steps followed to mine the frequent pattern using frequent pattern growth algorithm:

    1) The first step is to scan the database to find the occurrences of the itemsets in the database. This step is the same as the first step of Apriori. The count of 1-itemsets in the database is called support count or frequency of 1-itemset.

    2) The second step is to construct the FP tree. For this, create the root of the tree. The root is represented by null.

    3) The next step is to scan the database again and examine the transactions. Examine the first transaction and find out the itemset in it. The itemset with the max count is taken at the top, the next itemset with lower count and so on. It means that the branch of the tree is constructed with transaction itemsets in descending order of count.

    4) The next transaction in the database is examined. The itemsets are ordered in descending order of count. If any itemset of this transaction is already present in another branch (for example in the 1st transaction), then this transaction branch would share a common prefix to the root.

    This means that the common itemset is linked to the new node of another itemset in this transaction.

    5) Also, the count of the itemset is incremented as it occurs in the transactions. Both the common node and new node count is increased by 1 as they are created and linked according to transactions.

    6) The next step is to mine the created FP Tree. For this, the lowest node is examined first along with the links of the lowest nodes. The lowest node represents the frequency pattern length 1. From this, traverse the path in the FP Tree. This path or paths are called a conditional pattern base.

    Conditional pattern base is a sub-database consisting of prefix paths in the FP tree occurring with the lowest node (suffix).

    7) Construct a Conditional FP Tree, which is formed by a count of itemsets in the path. The itemsets meeting the threshold support are considered in the Conditional FP Tree.

    8) Frequent Patterns are generated from the Conditional FP Tree.
    
    
    example:
      Support threshold=50%, Confidence= 60%

      Table 1

        Transaction	    List of items
        T1	            I1,I2,I3
        T2	            I2,I3,I4
        T3	            I4,I5
        T4	            I1,I2,I4
        T5	            I1,I2,I3,I5
        T6	            I1,I2,I3,I4

      Solution:
      Support threshold=50% => 0.5*6= 3 => min_sup=3

      1. Count of each item

        Table 2

        Item	Count
        I1	    4
        I2	    5
        I3	    4
        I4	    4
        I5	    2
      
      2. Sort the itemset in descending order.

        Table 3

        Item	Count
        I2	    5
        I1	    4
        I3	    4
        I4	    4
      
      3. Build FP Tree

        Considering the root node null.
        The first scan of Transaction T1: I1, I2, I3 contains three items {I1:1}, {I2:1}, {I3:1}, where I2 is linked as a child to root, I1 is linked to I2 and I3 is linked to I1.
        T2: I2, I3, I4 contains I2, I3, and I4, where I2 is linked to root, I3 is linked to I2 and I4 is linked to I3. But this branch would share I2 node as common as it is already used in T1.
        Increment the count of I2 by 1 and I3 is linked as a child to I2, I4 is linked as a child to I3. The count is {I2:2}, {I3:1}, {I4:1}.
        T3: I4, I5. Similarly, a new branch with I5 is linked to I4 as a child is created.
        T4: I1, I2, I4. The sequence will be I2, I1, and I4. I2 is already linked to the root node, hence it will be incremented by 1. Similarly I1 will be incremented by 1 as it is already linked with I2 in T1, thus {I2:3}, {I1:2}, {I4:1}.
        T5:I1, I2, I3, I5. The sequence will be I2, I1, I3, and I5. Thus {I2:4}, {I1:3}, {I3:2}, {I5:1}.
        T6: I1, I2, I3, I4. The sequence will be I2, I1, I3, and I4. Thus {I2:5}, {I1:4}, {I3:3}, {I4 1}.
        FP Tree
   
   ![image](https://user-images.githubusercontent.com/54675828/133131590-ca86b0ca-fbb1-4aee-81b0-6d82f0225c98.png)

      4. Mining of FP-tree is summarized below:

        The lowest node item I5 is not considered as it does not have a min support count, hence it is deleted.
        The next lower node is I4. I4 occurs in 2 branches , {I2,I1,I3:,I41},{I2,I3,I4:1}. Therefore considering I4 as suffix the prefix paths will be {I2, I1, I3:1}, {I2, I3: 1}. This forms the conditional pattern base.
        The conditional pattern base is considered a transaction database, an FP-tree is constructed. This will contain {I2:2, I3:2}, I1 is not considered as it does not meet the min support count.
        This path will generate all combinations of frequent patterns : {I2,I4:2},{I3,I4:2},{I2,I3,I4:2}
        For I3, the prefix path would be: {I2,I1:3},{I2:1}, this will generate a 2 node FP-tree : {I2:4, I1:3} and frequent patterns are generated: {I2,I3:4}, {I1:I3:3}, {I2,I1,I3:3}.
        For I1, the prefix path would be: {I2:4} this will generate a single node FP-tree: {I2:4} and frequent patterns are generated: {I2, I1:4}.
        
        Item	   Conditional Pattern Base	      Conditional FP-tree	           Frequent Patterns Generated
        I4	      {I2,I1,I3:1},{I2,I3:1}	      {I2:2, I3:2}	                   {I2,I4:2},{I3,I4:2},{I2,I3,I4:2}
        I3	      {I2,I1:3},{I2:1}	              {I2:4, I1:3}	                   {I2,I3:4}, {I1:I3:3}, {I2,I1,I3:3}
        I1	      {I2:4}	                      {I2:4}	                       {I2,I1:4}
      The diagram given below depicts the conditional FP tree associated with the conditional node I3.

      conditional FP tree associated with conditional node I3
      
   ![image](https://user-images.githubusercontent.com/54675828/133130664-898d6c66-4583-45a7-a59f-b12f50941d00.png)

  ###  Advantages Of FP Growth Algorithm
   - This algorithm needs to scan the database only twice when compared to Apriori which scans the transactions for each iteration.
   - The pairing of items is not done in this algorithm and this makes it faster.
   - The database is stored in a compact version in memory.
   - It is efficient and scalable for mining both long and short frequent patterns.
      
  ### Disadvantages Of FP-Growth Algorithm
      FP Tree is more cumbersome and difficult to build than Apriori.
      It may be expensive.
      When the database is large, the algorithm may not fit in the shared memory.
      
      
   ### FP Growth vs Apriori
   
   ![image](https://user-images.githubusercontent.com/54675828/133135638-bff65fb8-c464-4084-9c74-d9e7fe4266cf.png)

      For Example, Apriori and FP growth use:

      Transaction	List of items
      T1	        I1,I2,I3
      T2	        I2,I3,I4
      T3	        I4,I5
      T4	        I1,I2,I4
      T5	        I1,I2,I3,I5
      T6	        I1,I2,I3,I4
      The ECLAT will have the format of the table as:

      Item	Transaction Set
      I1	{T1,T4,T5,T6}
      I2	{T1,T2,T4,T5,T6}
      I3	{T1,T2,T5,T6}
      I4	{T2,T3,T4,T5}
      I5	{T3,T5}
      This method will form 2-itemsets, 3 itemsets, k itemsets in the vertical data format. This process with k is increased by 1 until no candidate itemsets are found. Some optimizations techniques such as diffset are used along with Apriori.

      This method has an advantage over Apriori as it does not require scanning the database to find the support of k+1 itemsets. This is because the Transaction set will carry the count of occurrence of each item in the transaction (support). The bottleneck comes when there are many transactions taking huge memory and computational time for intersecting the sets.

    
    
 ## 4) List the name of packages/libraries used in Part 2 of this experiments
 Answer:
        
        import pandas as pd
        import numpy as np 
        import plotly.express as px
        import seaborn as sns
        import matplotlib.pyplot as plt
        
        %matplotlib inline
        import warnings
        warnings.filterwarnings('ignore')
        
        from mlxtend.frequent_patterns import apriori, association_rules
        from mlxtend.preprocessing import TransactionEncoder
        from pandas.plotting import parallel_coordinates
    
