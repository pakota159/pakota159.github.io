---
layout: post
subtitle: Index makes query fast - a simple explaination
tags: [sql, data]
comments: true
bigimg: /img/sql/bg.jpg
img1: /img/sql/img1.png
img2: /img/sql/img2.png
img3: /img/sql/img3.png
img4: /img/sql/img4.png
img5: /img/sql/img5.png
img6: /img/sql/img6.png
---

Well, most of developers or people who works with data know this "Index makes query fast" and they also understand why. But for people who don't really know about indexing, I would like to write this post to introduce to them about it.

___
First, let's talk about Tree.

**Tree** is a data structure created to improve the efficiency of looking up stuff.

Imagine we have a list like `[2, 4, 7, 6, 11]`

Now we want to find `number 6`, normally we will search one by one from left to right, `2 -> 4 -> 7 -> 6`. We found it, but if the list has thousand of items, it would took a lot of time to do the `search` operation like that.

Alternatively, we can use binary search tree data structure to improve the speed. We basically arrange order of the items in the list with the rule:
- Each item is stored in a node
- Each node (item) may has left child and right child with the condition: `left child < item < right child`

![img1]({{ page.img1 }}#img1)

With that logic, we don't have to go throught all items to find the number we want.

Start from root (top item), if we want number 6, we compare it with the root node. `6 < 7` so we go to the left branch (cause smaller item is always stored in the left of parent item). We get `number 4` and because `6 > 4` we go to the right of 4.

The time to search/find an item only depends on **height** of the tree which is the longest path from root node to any leaf node (other items) in the tree.
The bigger height, the slower speed to find the item we want.

![img2]({{ page.img2 }}#img2)

___
**Balanced Binary Tree**

Balanced Binary Tree basically is a Binary search tree as above, but the **height** is balanced. It means, with any node of the tree, the left branch height and the right branch height is the same or almost same (differ no more than 1)

Example: with the tree in the image below, if we check the node `4`, left branch has the height of 1 (contain number 2), right branch is 1 (contain number 6).

If we check the node 7, left branch has the height of 2, right branch has the height of 1. So, it differs 2 - 1 = 1. 

Summary, the binary tree below is a balanced binary tree.

This kind of tree is used to optimize the speed of searching, because it optimizes the height of the tree (which is the factor affects to the speed of searching)

![img1]({{ page.img1 }}#img1)

___
**B-tree**

B-tree is some kinds of upgraded Balanced Binary Tree, you now can have multiple item stored in one node (instead of 1 item - 1 node), and each node can have more than 2 children.

As the structure below, we can see each node can have a bulk of data on the left or on the right. The left bulk contains values which are smaller than the value of the parent node. The right bulk contains values which are bigger than the parent.

![img3]({{ page.img3 }}#img3)

___
**The index in database**

Imagine your table will be stored in database like this:

| ID        | author_name           |
| ------------- |:-------------:| 
|001 |Gilles van den Hoven|
|002 |Michael Geary|
|003 |Stefan Petre|
|004 |Yehuda Katz|
|005 |Corey Jewett|
|006 |Klaus Hartl|
|007 |Franck Marcia|
|008 |Jörn Zaefferer|
|009 |Paul Bakaus|
|0010 |Brandon Aaron|

*(Authors above are people who contribute to Jquery library)*

We want to searching name of author name fast, so we need to add a new table - index table which contain the data of column **author_name** and organize that data into B-tree data structure so the search can be optimized.

**index of author_name** can be simply expressed like below.

At the root node of the Tree, we store list of few author_name, for example: [Corey Jewett, Michael Geary, Paul Bakaus], all sorted by A-Z order.

Then for each value, we create a child node which contains other names which is satisfy the rule of B-tree: `left node is all values smaller than parent, right node is bigger`, and in this case, *smaller* means stays in the left of the Alphabet.

![img4]({{ page.img4 }}#img4)

When we do search a name like `Yehuda Katz`, we start from the root, Y is *bigger* than *P* in *Paul Bakaus* so we look up to the right node of *Paul Bakaus*.

In the child node, we do the same thing until we reach to the lowest child node. In this node, we do binary search to search the value. The number of values store in each node is small, so binary search will do the search really fast.

**The reasons we use B-tree**:
- We can store data in each node, therefore reduce the *height* of the tree and improve the speed of the search.
- Values in each node is sorted in a particular order, therefore we can look up faster. Number of values in each node is small enough so binary search can be fast too.

___
Example:

I will demonstrate for you the difference between no-index and indexing query performance. The data I use is 1.5 millions records of sale, and I use Postgre database to store those records.

Before add index to the column `Item Type`, I try the query as below, and it returns `125022 records`, with the speed of `2.244 seconds`.

![img5]({{ page.img5 }}#img5)

Now, we will add index to the `Item Type` column

```sql
CREATE INDEX item_type_index ON sale_records ("Item Type");
```

That command will run for a while to create a new table which is an `index table` contains the data of column `Item Type` with the principle of B-tree as we talked earlier.

![img6]({{ page.img6 }}#img6)

As we can see, the speed is much better now. The index helps us identify the word *Beverages* faster, hence we can search for that better.

___
**Some rules for SQL**

Thanks for understanding the underlying principle of indexes, we now can note down some rules for better query we write in the future.

1. Avoid LIKE expressions with leading wildcards (e.g., '%TERM').  
Because the index use the first letter and sort by A-Z order, we should avoid LIKE expression without first letter specified. The index table will be useless in this case.

2. If we create index for multiple columns, then the WHERE condition for 1 column in those columns will not use index.  
For example, if we make index for `user_id` and `company` then we search for `user_id = 1000`, that query will not use index, because the index only valid for the combination `user_id` and `company`. We have to search for `user_id = 1000 AND company = 'GOOGLE'` to use index.

3. If we want to search with Case-Insensitive (means CUONG and Cuong are the same result), then we should create Index with case-insensitive.  Something like: `CREATE INDEX user_index ON users (UPPER(first_name));` which creates index with uppercase of first_name column values.  
Then we execute the query `SELECT * from users WHERE UPPER(first_name) = 'CUONG';`

4. Note for function-based index. For example, if you want to query the data `how many days from the lastest day each user bought a product` you often query something like `TRUNC(DAYS_BETWEEN(SYSDATE, buy_date))`.  
However, this value can not be index, because it changed daily. (index will be update with the command INSERT, UPDATE, DELTE, but can't automatically update daily like this, or while execute query command). But we still want to quickly search for the days above.  
The solution is that we index `buy_date` and then, if we want to query all users that have 30 days from now to their lastest buy, we calculate that date (*that_date = today - 30 days*), then query with condition `that_date = buy_date`

5. When writing condition for datetime range, we should explicitly declare the start and end of the time range. Instead of writing `WHERE date_time < '2020-10-10'` we should write `WHERE '2020-10-09' < date_time < '2020-10-10'`



___
READ MORE:
1. [Use The Index, Luke](https://use-the-index-luke.com/)

___