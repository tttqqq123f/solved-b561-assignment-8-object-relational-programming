Download Link: https://assignmentchef.com/product/solved-b561-assignment-8-object-relational-programming
<br>
<h1>1           Object Relational Programming</h1>

<ol>

 <li><strong>For this problem you can not use arrays.</strong></li>

</ol>

Consider the relational schema Tree(parent int, child int) representing the schema for storing a rooted tree.<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> A pair of nodes (<em>m,n</em>) is in Tree if <em>m </em>is the parent of <em>n </em>in Tree. Notice that a node <em>m </em>can be the parent of multiple children but a node <em>n </em>can have at most one parent node.

It should be clear that for each pair of different nodes <em>m </em>and <em>n </em>in Tree, there is a unique shortest path of nodes (<em>n</em><sub>1</sub><em>,…,n<sub>k</sub></em>) in Tree from <em>m </em>to <em>n </em>provided we interpret the edges in Tree as undirected. A good way to think about this path from a node <em>m </em>to a node <em>n </em>is to first consider the <em>lowest common ancestor node </em>of <em>m </em>of <em>n </em>in Tree. Then the unique path from <em>m </em>to <em>n </em>is the path that is comprised of the path up the tree from <em>m </em>to this common ancestor and then, from this common ancestor, the path down the tree to the node <em>n</em>. (Note that in this path <em>n</em><sub>1 </sub>= <em>m </em>and <em>n<sub>k </sub></em>= <em>n</em>.)

Define the <em>distance </em>from <em>m </em>to <em>n </em>to be <em>k </em>− 1 if (<em>n</em><sub>1</sub><em>,…,n<sub>k</sub></em>) is the unique shortest path from <em>m </em>to <em>n </em>in Tree.

Write a PostgreSQL function distance(m,n) that computes the distance in Tree for any possible pair of different nodes <em>m </em>and <em>n </em>in Tree.

For example, if <em>m </em>is the parent of <em>n </em>in Tree then distance(<em>m,n</em>) = 1 because the shortest path from <em>m </em>to <em>n </em>is (<em>m,n</em>) which has length 1. If <em>m </em>is the grandparent of <em>n </em>in Tree then distance distance(<em>m,n</em>) = 2 since (<em>m,p,n</em>) is the path from <em>m </em>to <em>n </em>where <em>p </em>is the parent of <em>m </em>and <em>p </em>is a child of <em>n</em>. And if <em>m </em>and <em>n </em>have a common grandparent <em>k </em>then <em>distance</em>(<em>m,n</em>) = <em>distance</em>(<em>m,k</em>) + <em>distance</em>(<em>k,n</em>) = 4, etc.

<ol start="2">

 <li><strong>For this problem you can use arrays.</strong></li>

</ol>

Consider the relation schema Graph(source int, target int) representing the schema for storing a directed graph <em>G </em>of edges.

Now let <em>G </em>be a directed graph that is <strong>acyclic</strong>, a graph without cycles.<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a>

A <em>topological sort </em>of an acyclic graph is a list of <strong>all </strong>of its nodes (<em>n</em><sub>1</sub><em>,n</em><sub>2</sub><em>,…,n<sub>k</sub></em>) such that for each edge (<em>m,n</em>) in <em>G</em>, node <em>m </em>occurs before node <em>n </em>in this list.

Write a PostgreSQL program topologicalSort() that returns a topological sort of <em>G</em>.

<ol start="3">

 <li><strong>For this problem, you can not use arrays.</strong></li>

</ol>

Consider the following relational schemas. (You can assume that the domain of each of the attributes in these relations is int.)

partSubpart(pid,sid,quantity) basicPart(pid,weight)

A tuple (<em>p,s,q</em>) is in partSubPart if part <em>s </em>occurs <em>q </em>times as a <strong>direct </strong>subpart of part <em>p</em>. For example, think of a car <em>c </em>that has 4 wheels <em>w </em>and 1 radio <em>r</em>. Then (<em>c,w,</em>4) and (<em>c,r,</em>1) would be in partSubpart. Furthermore, then think of a wheel <em>w </em>that has 5 bolts <em>b</em>. Then (<em>w,b,</em>5) would be in partSubpart.

A tuple (<em>p,w</em>) is in basicPart if basic part <em>p </em>has weight <em>w</em>. A basic part is defined as a part that does not have subparts. In other words, the pid of a basic part does not occur in the pid column of partSubpart.

(In the above example, a bolt and a radio would be basic parts, but car and wheel would not be basic parts.)

We define the <em>aggregated weight </em>of a part inductively as follows:

<ul>

 <li>If <em>p </em>is a basic part then its aggregated weight is its weight as given in the basicPart relation</li>

 <li>If <em>p </em>is not a basic part, then its aggregated weight is the sum of the aggregated weights of its subparts, each multiplied by the quantity with which these subparts occur in the partSubpart</li>

</ul>

<strong>Example tables</strong>: The following example is based on a desk lamp with pid 1. Suppose a desk lamp consists of 4 bulbs (with pid 2) and a frame (with pid 3), and a frame consists of a post (with pid 4) and 2 switches (with pid 5). Furthermore, we will assume that the weight of a bulb is 5, that of a post is 50, and that of a switch is 3.

Then the partSubpart and basicPart relation would be as follows:

<strong>partSubPart</strong>

<strong>basicPart</strong>

<table width="251">

 <tbody>

  <tr>

   <td width="147">


    <table width="131">

     <tbody>

      <tr>

       <td width="34">pid</td>

       <td width="32">sid</td>

       <td width="65">quantity</td>

      </tr>

      <tr>

       <td width="34">1</td>

       <td width="32">2</td>

       <td width="65">4</td>

      </tr>

      <tr>

       <td width="34">1</td>

       <td width="32">3</td>

       <td width="65">1</td>

      </tr>

      <tr>

       <td width="34">3</td>

       <td width="32">4</td>

       <td width="65">1</td>

      </tr>

      <tr>

       <td width="34">3</td>

       <td width="32">5</td>

       <td width="65">2</td>

      </tr>

     </tbody>

    </table></td>

   <td width="104">


    <table width="88">

     <tbody>

      <tr>

       <td width="34">pid</td>

       <td width="54">weight</td>

      </tr>

      <tr>

       <td width="34">2</td>

       <td width="54">5</td>

      </tr>

      <tr>

       <td width="34">4</td>

       <td width="54">50</td>

      </tr>

      <tr>

       <td width="34">5</td>

       <td width="54">3</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>

Then the aggregated weight of a lamp is 4×5+1×(1×50+2×3) = 76.

Write a PostgreSQL function aggregatedWeight(p integer) that returns the aggregated weight of a part p.

<ol start="4">

 <li><strong>For this problem you need to use arrays.</strong></li>

</ol>

Consider the relation schema document(<u>doc </u>int, words text[]) representing a relation of pairs (<em>d,W</em>) where <em>d </em>is a unique id denoting a document and <em>W </em>denotes the set of words that occur in <em>d</em>.

Let <strong>W </strong>denote the set of all words that occur in the documents and let <em>t </em>be a positive integer denoting a <em>threshold</em>.

Let <em>X </em>⊆ <strong>W</strong>. We say that <em>X </em>is <em>t</em>-frequent if count({<em>d</em>|(<em>d,W</em>) ∈ documentand<em>X </em>⊆ <em>W</em>}) ≥ <em>t</em>

In other words, <em>X </em>is <em>t-frequent </em>if there are at least <em>t </em>documents that contain all the words in <em>X</em>.

Write a PostgreSQL program frequentSets(t int) that returns the set of all <em>t</em>-frequent set.

In a good solution for this problem, you should use the following rule: if <em>X </em>is not <em>t</em>-frequent then any set <em>Y </em>such that <em>X </em>⊆ <em>Y </em>is not <em>t</em>-frequent either. In the literature, this is called the <em>Apriori </em>rule of the frequent itemset mining problem. This rule can be used as a pruning rule. In other words, if you have determined that a set <em>X </em>in not <em>t</em>-frequent then you no longer have to consider any of <em>X</em>’s supersets.

To learn more about this problem you can visit the site https://en.wikipedia.org/wiki/Apriori algorithm.

<ol start="5">

 <li><strong>For this problem you can use arrays.</strong></li>

</ol>

For this problem, first read about the <em>k</em>-means clustering problem in http://stanford.edu/~cpiech/cs221/handouts/kmeans.html

Look at the <em>k</em>-means clustering algorithm described in this document. Your task is to implement this algorithm in PostgreSQL for a dataset that consists of a set of points in a 2-dimensional space.

Assume that the dataset is stored in a ternary relation with schema

Points(p int, x float, y float)

where p is an integer uniquely identifying a point (x<em>,</em>y).

Write a PostgreSQL program kMeans(k integer) that returns a set of <em>k </em>points that denote the centroids for the points in Points. Note that <em>k </em>is an input parameter to the kMeans function.

You will need to reason about how to determine when the algorithm terminates. A possible termination condition is to set a number of iterations that denotes how many iterations are run to approximate the centroids. Another termination condition is to consider when the set of centroids no longer changes.

<h1>2   Physical Database Organization and Algorithms</h1>

<ol start="6">

 <li>Consider the following parameters:</li>

</ol>

<table width="275">

 <tbody>

  <tr>

   <td width="119">block size</td>

   <td width="26">=</td>

   <td width="129">4096 bytes</td>

  </tr>

  <tr>

   <td width="119">block-address size</td>

   <td width="26">=</td>

   <td width="129">9 bytes</td>

  </tr>

  <tr>

   <td width="119">block access time</td>

   <td width="26">=</td>

   <td width="129">10 ms (micro seconds)</td>

  </tr>

  <tr>

   <td width="119">record size</td>

   <td width="26">=</td>

   <td width="129">200 bytes</td>

  </tr>

  <tr>

   <td width="119">record key size</td>

   <td width="26">=</td>

   <td width="129">12 bytes</td>

  </tr>

 </tbody>

</table>

Assume that there is a B<sup>+</sup>-tree, adhering to these parameters, that indexes 10<sup>8 </sup>million records on their primary key values.

Show all the intermediate computations leading to your answers.

<ul>

 <li>Specify (in ms) the minimum time to retrieve a record with key <em>k </em>in the B<sup>+</sup>-tree provided that there is a record with this key.</li>

 <li>Specify (in ms) the maximum time to retrieve a record with key <em>k </em>in the B<sup>+</sup>-tree.</li>

</ul>

<ol start="7">

 <li>Consider the following B<sup>+</sup>-tree of order 2 that holds records with keys 2, 7, 9, and 11. (Observe that (a) an internal node of a B<sup>+</sup>-tree of order 2 can have either 1 or 2 keys values, and 2 or 3 sub-trees, and (b) a leaf node can have either 1 or 2 key values.)</li>

</ol>

———–

| / 9  |

———–

/                      

/                          

———-                    ————

| 2           7 |—&gt;| 9               11 |

———-                    ————

<ul>

 <li>Show the contents of your B<sup>+</sup>-tree after inserting records with keys 6, 10, 14, and 4, in that order.</li>

 <li>Starting from your answer in question 7a, show the contents of yourB<sup>+</sup>-tree after deleting records with keys 2, 14, 4, and 10, in that order.</li>

</ul>

<ol start="8">

 <li>Consider an extensible hashing data structure wherein (1) the initial globaldepth is set at 1 and (2) all directory pointers point to the same <strong>empty </strong>block which has local depth 0. So the hashing structure looks like this:</li>

</ol>

global-depth 1                       local-depth 0

——                                 ——————

<ul>

 <li>| –|——–&gt;| |</li>

</ul>

——                        |                                      |

<ul>

 <li>| –|——–&gt;| |</li>

</ul>

——                                 ——————

Assume that a block can hold at most two records.

(a) Show the state of the hash data structure after each of the following insert sequences:<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a>

<ol start="6">

 <li>records with keys 2 and 6. ii. records with keys 1 and 7. iii. records with keys 4 and 8.</li>

 <li>records with keys 0 and 9.</li>

</ol>

(b) Starting from the answer you obtained for Question 8a, show the state of the hash data structure after each of the following delete sequences:

<ol start="2">

 <li>records with keys 1 and 2. ii. records with keys 6 and 7.</li>

</ol>

iii. records with keys 0 and 9.

<ol start="9">

 <li>Let <em>R</em>(<em>A,B</em>) and <em>S</em>(<em>B,C</em>) be two relations and consider their natural join <em>R ./ S</em>.</li>

</ol>

Assume that <em>R </em>has 1,500,000 records and that <em>S </em>has 5<em>,</em>000 records.

Furthermore, assume that 30 records of <em>R </em>can fit in a block and that 10 records of <em>S </em>can fit in a block.

Assume that you have a main-memory buffer with 101 blocks.

<ul>

 <li>How many block IO’s are necessary to perform <em>R ./ S </em>using the block nested-loops join algorithm? Show your analysis.</li>

 <li>How many block IO’s are necessary to perform <em>R ./ S </em>using the sort-merge join algorithm? Show your analysis.</li>

 <li>Repeat question 9b under the following assumptions.</li>

</ul>

Assume that there are <em>p </em>different <em>B</em>-values and that these are uniformly distributed in <em>R </em>and <em>S</em>.

Observe that to solve this problem, depending on <em>p</em>, it may be necessary to perform a block nested-loop join per occurrence of a <em>B</em>-value.

<ul>

 <li>How many block IO’s are necessary to perform <em>R ./ S </em>using the hash-join algorithm? Show your analysis.</li>

</ul>

<h1>3           Concurrency Control</h1>

<ol start="10">

 <li>State which of the following schedules <em>S</em><sub>1</sub>, <em>S</em><sub>2</sub>, and <em>S</em><sub>3 </sub>over transactions <em>T</em><sub>1</sub>, <em>T</em><sub>2</sub>, and <em>T</em><sub>3 </sub>are conflict-serializable, and for each of the schedules that is serializable, given a serial schedule with which that schedule is conflictequivalent.

  <ul>

   <li><em>S</em><sub>1 </sub>= <em>R</em><sub>1</sub>(<em>x</em>)<em>R</em><sub>2</sub>(<em>y</em>)<em>R</em><sub>1</sub>(<em>z</em>)<em>R</em><sub>2</sub>(<em>x</em>)<em>R</em><sub>1</sub>(<em>y</em>).</li>

   <li><em>S</em><sub>2 </sub>= <em>R</em><sub>1</sub>(<em>x</em>)<em>W</em><sub>2</sub>(<em>y</em>)<em>R</em><sub>1</sub>(<em>z</em>)<em>R</em><sub>3</sub>(<em>z</em>)<em>W</em><sub>2</sub>(<em>x</em>)<em>R</em><sub>1</sub>(<em>y</em>).</li>

   <li><em>S</em><sub>3 </sub>= <em>R</em><sub>1</sub>(<em>z</em>)<em>W</em><sub>2</sub>(<em>x</em>)<em>R</em><sub>2</sub>(<em>z</em>)<em>R</em><sub>2</sub>(<em>y</em>)<em>W</em><sub>1</sub>(<em>x</em>)<em>W</em><sub>3</sub>(<em>z</em>)<em>W</em><sub>1</sub>(<em>y</em>)<em>R</em><sub>3</sub>(<em>x</em>).</li>

  </ul></li>

 <li>Give 3 transactions <em>T</em><sub>1</sub>, <em>T</em><sub>2</sub>, <em>T</em><sub>3 </sub>and a schedule <em>S </em>on these transactions whose precedence graph (i.e. serialization graph) consists of the edges (<em>T</em><sub>1</sub><em>,T</em><sub>2</sub>), (<em>T</em><sub>2</sub><em>,T</em><sub>1</sub>), (<em>T</em><sub>1</sub><em>,T</em><sub>3</sub>), (<em>T</em><sub>3</sub><em>,T</em><sub>2</sub>).</li>

 <li>Give 3 transactions <em>T</em><sub>1</sub>, <em>T</em><sub>2</sub>, and <em>T</em><sub>3 </sub>that each involve read and write operations and a schedule <em>S </em>that is conflict-equivalent with <strong>all </strong>serial schedules over <em>T</em><sub>1</sub>, <em>T</em><sub>2</sub>, and <em>T</em><sub>3</sub>.</li>

 <li>Consider the following transactions:</li>

</ol>

T1: read(A); read(B);

if A = 0 then B := B+1; write(B).

T2: read(B); read(A);

if B = 0 then A := A+1; write(A).

Let the consistency requirement be A = 0 ∨ B = 0, and let A = B = 0 be the initial values.

<ul>

 <li>Show that each serial schedule involving transaction <em>T</em><sub>1 </sub>and <em>T</em><sub>2 </sub>preserves the consistency requirement of the database.</li>

 <li>Construct a schedule on <em>T</em><sub>1 </sub>and <em>T</em><sub>2 </sub>that produces a non-serializable schedule.</li>

 <li>Is there a non-serial schedule on <em>T</em><sub>1 </sub>and <em>T</em><sub>2 </sub>that produces a serializable schedule. If so, give an example.</li>

</ul>

<a href="#_ftnref1" name="_ftn1">[1]</a> We assume that a tree is a connected graph with a finite number of nodes.

<a href="#_ftnref2" name="_ftn2">[2]</a> A cycle is a path (<em>v</em><sub>0</sub><em>,…,v<sub>k</sub></em>) where <em>v</em><sub>0 </sub>= <em>v<sub>k</sub></em>.

<a href="#_ftnref3" name="_ftn3">[3]</a> You should interpret the key values as bit strings of length 4. So for example, key value 7 is represented as the bit string 0111 and key value 2 is represented as the bit string 0010.