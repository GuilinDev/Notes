# Notes
## Summary
这个repo是关于面试准备的。

<div align="center"><img src="/images/logo.png" height="180" width="215" ></div>

## 互联网公司面试准备思维导图

![面试思维导图](/images/MindMapInterview.jpg)

## 数据结构和算法理论基础

掌握数据结构和算法直接的好处就是能写出性能更优的代码。算法是一种解决问题的思路和方法，从长期来看，大脑思考能力是个人最重要的核心竞争力，而算法是为数不多的能够训练大脑思考能力的途径之一。

🍭 学习路线加强巩固数据结构基础知识，主要通过 leetcode 算法题加深对数据结构的理解。在刷Leetcode之前和同时，看Cracking the Coding Interview (CTCI)和在[Hackerrank](https://www.hackerrank.com/)/[GeeksForGeeks](https://www.geeksforgeeks.org/category/interview-experiences/)上练习一些基础会很有帮助。下面的技巧至少练习三遍到滚瓜烂熟：
* 从scratch实现一个ArrayList
* 翻转链表
* 用Array实现Stack和Queue
* 用简单的Hashing function实现一个hashmap
* 用Adjacency Matrix和Adjacency List来实现Graph，然后在此基础上进行BFS和DFS
* Binary Search的迭代和递归
* Merge Sort，Quick Sort，Counting Sort
* 二叉树的DFS（前序，中序，后序的递归写法和迭代写法），BFS（层序）
* [时间空间复杂度分析](https://www.bigocheatsheet.com/)
* 

可以明确的是，面试时候的算法题目在难度上（尤其是代码难度上）不会吹毛求疵，会倾向于靠擦一些基础的数据结构和算法，对于高级算法和奇技淫巧一般不作考察。

代码题主要考察编程语言的应用是否熟练，基础是否扎实，比如让面试者写出代码完成简单的需求，大约下面的这些内容打好基础就足够了：

**Data Structures**
1. 数组与链表：单/双链表，跳表
2. 栈与队列
3. 树与图：最近公共祖先，并查集
4. 哈希表
5. 堆：大根/小根堆，可并堆
6. 字符串：前缀树，后缀树

**Algorithms**
1. 排序算法：快排，归并，计数
2. 搜索算法：回溯，递归，剪枝技巧
3. 图论：最短路径，最小生成树，网络流
4. 动态规划：背包问题，最长子序列，计数问题
5. 基础技巧：分治，倍增，二分，贪心


| &emsp;&emsp;[Array/Dynamic Array](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/1.%E6%95%B0%E7%BB%84.md)&emsp;&emsp; | &emsp;&emsp;[**LinkedList**](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/2.%E9%93%BE%E8%A1%A8.md)&emsp;&emsp;  |  &emsp;&ensp;&ensp;[**Stack & Queue**](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/3.%E6%A0%88.md)&emsp;&ensp;&emsp; | &emsp;&emsp;[**跳表**](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/4.%E8%B7%B3%E8%A1%A8.md)&emsp;&emsp; | &emsp;[**Hashtable**](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E5%B8%B8%E8%A7%81%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84/5.%E6%95%A3%E5%88%97%E8%A1%A8.md)&emsp;&emsp; | &emsp;&emsp;二叉树&emsp;&emsp; |
| :---: | :---: | :---: | :------: | :---: | :--------: |
| ️⭐⭐⭐ | ⭐⭐⭐ | ⭐ | ️⭐  |  ️⭐⭐  | ️⭐⭐⭐   |



| &emsp;&emsp;贪心&emsp;&emsp;  | &emsp;&emsp;分治&emsp;&emsp;  | &emsp;&emsp;回溯&emsp;&ensp;  | &emsp;[**动态规划**](https://leetcode.com/discuss/general-discussion/458695/dynamic-programming-patterns)&emsp; | &emsp;&emsp;[**递归**](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E9%80%92%E5%BD%92.md)&emsp;&emsp;  | &emsp;复杂度分析&emsp; |
| :---: | :---: | :---: | :------: | :---: | :--------: |
| ️⭐⭐⭐  | ⭐⭐⭐  | ⭐⭐⭐  |  ️⭐⭐⭐    | ️⭐⭐⭐ |⭐⭐⭐|



Data Structures
* Dynamic Array
* Linked List
* Stack & Queue
* Hash Tables
* Binary Search Tree
* Binary Heaps & Priority Queue
* Graphs
* Trie
Algorithms
* Bit Manipulation & Numbers — difference btw Unsigned vs signed numbers
* Stability in Sorting
* Mergesort
* Quicksort
* Heapsort — Sort it in-place to get O(1) space
* Binary Search
* Selections — Kth Smallest Elements (Sort, QuickSelect, Mediums of Mediums) — Implement all three ways
* Permutations
* Subsets
* BFS Graph
* DFS Graph
* Dijkstra’s Algorithm (just learn the idea — no need to implement)
* Tree Traversals — BFS, DFS (in-order, pre-order, post-order): Implement Recursive and Iterative
* External Sort — No implementation; Just know the concept.
* NP-Complete (Video) — Just know the concept
* Topological Sort
* Detect cycle in an undirected graph
* Detect a cycle in a directed graph
* Count connected components in a graph
* Find strongly connected components in a graph
         
         
## 面试常考算法题

以下列出面试高频出现，以及一些非常经典重要的算法题，[点击leetcode的细分类别一定要看](https://leetcode.com/discuss/general-discussion/665604/important-and-useful-links-from-all-over-the-leetcode)，如果想按照类别刷题，可以按照[leetcode的分类题目卡片](https://leetcode.com/explore/interview/card/top-interview-questions-easy/)。在线面试工具通常是类似[Hackerrank](https://www.hackerrank.com/)或者[codepad](https://coderpad.io/)或者公司自己的工具。
  
> 第一周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结  |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  1  | 简单 | [Two Sum](https://leetcode.com/problems/two-sum/) | [Two Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/ksum#1-2sum)                                                             |    Hashmap     |
|  146  | 中等 | [LRU Cache](https://leetcode.com/problems/lru-cache/) | [LRU Cache](https://app.gitbook.com/@guilindev/s/interview/leetcode/gao-ji-de-shu-ju-jie-gou-he-suan-fa#146-lru-cache) |    1. Hashmap + Double Linkedlist <br> 2. LinkedHashMap     |
|  2  | 中等 | [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)           | [Add Two Numbers](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#2-add-two-numbers) |    注意carry，这道题的II从后往前加则用stack或者递归     |
|  4  | 困难 | [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)  | [Median of Two Sorted Arrays](https://app.gitbook.com/@guilindev/s/interview/leetcode/array#4-median-of-two-sorted-arrays) |    1. Kth element <br> 2. [Partition + Binary Searth](https://www.youtube.com/watch?v=LPFhl65R7ww)     |
| 周二 |  |  |  | ✅ |
|  3  | 中等 | [Longest Substring Without Repeating Characters ](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | [Longest Substring Without Repeating Characters ](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#3-longest-substring-without-repeating-characters)                                                             |    1. HashMap or HashSet <br> 2. 256 size Array     |
|  5  | 中等 | [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) | [Longest Palindromic Substring](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#5-longest-palindromic-substring) |    1. 分奇偶 <br> 2. DP <br> 3. 了解Manacher's     |
|  973  | 中等 | [K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)           | [K Closest Points to Origin](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer-1#973-k-closest-points-from-origin) |    topK     |
|  42  | 困难 | [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)  | [Trapping Rain Water](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#42-trapping-rain-water) |    1. DP <br> 2. Stack     |
| 周三 |  |  |  | ✅ |
|  53  | 简单 | [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/) | [Maximum Subarray](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/zi-shu-zu-subarray#53-maximum-subarray)                                                             |    前面所有sum为负舍弃问题，与152乘积子数组一起练习     |
|  200  | 中等 | [Number of Islands](https://leetcode.com/problems/number-of-islands/) | [Number of Islands](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#200-number-of-islands) |    1. DFS <br> 2. BFS <br> 3. Union Find     |
|  56  | 中等 | [Merge Intervals](https://leetcode.com/problems/merge-intervals/)           | [Merge Intervals](https://app.gitbook.com/@guilindev/s/interview/leetcode/hui-wen-jie-gou#56-merge-intervals) |    按头排序，比较尾巴     |
|  23  | 困难 | [Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)  | [Merge k Sorted Lists](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#23-merge-k-sorted-lists) |    1. Merge Sort <br> 2. minHeap     |
| 周四 |  |  |  | ✅ |
|  20  | 简单 | [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) | [Valid Parentheses](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#20-valid-parentheses)                                                             |     1. Stack，注意pop时EmptyStackException <br> 2. counter    |
|  253  | 中等 | [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) | [Meeting Rooms II](https://app.gitbook.com/@guilindev/s/interview/leetcode/hui-wen-jie-gou#253-meeting-rooms-ii) |    1. Sort <br> 2. TreeMap <br> 3. minHeap     |
|  33  | 中等 | [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)           | [Search in Rotated Sorted Array](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/zai-array-zhong-cha-xun-yuan-su#33-search-in-rotated-sorted-array) |    BST，先确定左右两边哪边有序     |
|  301  | 困难 | [Remove Invalid Parentheses ](https://leetcode.com/problems/remove-invalid-parentheses/)  | [Remove Invalid Parentheses ](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-3#301-remove-invalid-parentheses) |    1. BFS <br> 2. DFS     |
| 周五 |  |  |  | ✅ |
|  322  | 中等 | [Coin Change](https://leetcode.com/problems/coin-change/) | [Coin Change](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#322-coin-change)                                                             |     DP - Bottom up    |
|  138  | 中等 | [Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/) | [Copy List with Random Pointer](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#138-copy-list-with-random-pointer) |     1. HashMap <br> 2. 遍历三次    |
|  449  | 中等 | [Serialize and Deserialize BST](https://leetcode.com/problems/serialize-and-deserialize-bst/)           | [Serialize and Deserialize BST](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#449-serialize-and-deserialize-bst) |    DFS前序遍历，二分优化     |
|  297  | 困难 | [Serialize and Deserialize Binary Tree ](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)  | [Serialize and Deserialize Binary Tree ](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#297-serialize-and-deserialize-binary-tree) |    1. DFS前序遍历 <br> 2. BFS层序遍历    |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第二周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  79  | 中等 | [Word Search](https://leetcode.com/problems/word-search/) | [Word Search](https://app.gitbook.com/@guilindev/s/interview/leetcode/backtracking#79-word-search) |    Backtracking<br>(visited + 优化空间)     |
|  560  | 中等 | [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) | [Subarray Sum Equals K](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/zi-shu-zu-subarray#560-subarray-sum-equals-k) |    preSum + HashMap     |
|  46  | 中等 | [Permutations](https://leetcode.com/problems/permutations/) | [Permutations](https://app.gitbook.com/@guilindev/s/interview/leetcode/backtracking#46-permutations) |    [回溯模板](https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning))     |
|  103  | 中等 | [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) | [Binary Tree Zigzag Level Order Traversal](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#103-binary-tree-zigzag-level-order-traversal) |    1. BFS标记<br>2. DFS 递归栈记录     |
| 周二 |  |  |  | ✅ |
|  215  | 中等 | [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) | [Kth Largest Element in an Array](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer-1#215-kth-largest-element-in-an-array) |    掌握两种<br>1. 堆<br>2. 快速选择     |
|  49  | 中等 | [Group Anagrams](https://leetcode.com/problems/group-anagrams/) | [Group Anagrams](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#49-group-anagrams) |    HashMap，确定key     |
|  31  | 中等 | [Next Permutation](https://leetcode.com/problems/next-permutation/) | [Next Permutation](https://app.gitbook.com/@guilindev/s/interview/leetcode/array#31-next-permutation) |    1. 从后向前找一个非增长的元素，位置p<br>2. 再次从后向前找到第一个比刚才位置p元素大的元素，位置q，交换p，q<br>3. p位置后面的数组元素翻转     |
|  10  | 困难 | [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/) | [Regular Expression Matching](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#10-regular-expression-matching) |    DP     |
| 周三 |  |  |  | ✅ |
|  91  | 中等 | [Decode Ways](https://leetcode.com/problems/decode-ways/) | [Decode Ways](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#91-decode-ways) |    1.递归<br>2.DP     |
|  127  | 中等 | [Word Ladder](https://leetcode.com/problems/word-ladder/) | [Word Ladder](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-3#127-word-ladder) |    无向图BFS     |
|  139  | 中等 | [Word Break](https://leetcode.com/problems/word-break/) | [Word Break](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#139-word-break) |    DP，第二个循环往左，Trie解法不要求     |
|  295  | 困难 | [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) | [Find Median from Data Stream](https://app.gitbook.com/@guilindev/s/interview/leetcode/heap#295-find-median-from-data-stream) |    1大顶堆 + 1小顶堆     |
| 周四 |  |  |  | ✅ |
|  100  | 简单 | [Same Tree](https://leetcode.com/problems/same-tree/) | [Same Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#100-same-tree) |     递归，BFS    |
|  98  | 中等 | [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) | [Validate Binary Search Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#98-validate-binary-search-tree) |    前序，中序     |
|  621  | 中等 | [Task Scheduler](https://leetcode.com/problems/task-scheduler/) | [Task Scheduler](https://app.gitbook.com/@guilindev/s/interview/leetcode/queue#621-task-scheduler) |    Greedy排序     |
|  642  | 困难 | [Design Search Autocomplete System](https://leetcode.com/problems/design-search-autocomplete-system/) | [Design Search Autocomplete System](https://app.gitbook.com/@guilindev/s/interview/leetcode/design#642-design-search-autocomplete-system) |    Coding: Trie <br> [System Design](https://www.youtube.com/watch?v=us0qySiUsGU)     |
| 周五 |  |  |  | ✅ |
|  283  | 简单 | [Move Zeroes](https://leetcode.com/problems/move-zeroes/) | [Move Zeroes](https://app.gitbook.com/@guilindev/s/interview/leetcode/array#283-move-zeroes) |    Two Pointers     |
|  986  | 中等 | [Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/) | [Interval List Intersections](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-2#986-interval-list-intersections) |    Two Pointers     |
|  39  | 中等 | [Combination Sum](https://leetcode.com/problems/combination-sum/) | [Combination Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/backtracking#39-combination-sum) |    [回溯模板](https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning))     |
|  85  | 困难 | [Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/) | [Maximal Rectangle](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/array-zhong-de-shu-zi-zu-cheng-san-jiao-xing#85-maximum-rectangle) |    1.Stack<br>2.DP     |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第三周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  207  | 中等 | [Course Schedule ](https://leetcode.com/problems/course-schedule/) | [Course Schedule ](https://app.gitbook.com/@guilindev/s/interview/leetcode/graph#207-course-schedule) |    DAG的BFS和DFS     |
|  227  | 中等 | [Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/) | [Basic Calculator II](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#227-basic-calculator-ii) |    Stack压入数字，乘除弹出数字进行运算，加减最后运算     |
|  34  | 中等 | [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | [Find First and Last Position of Element in Sorted Array](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/zai-array-zhong-cha-xun-yuan-su#34-find-first-and-last-position-of-element-in-sorted-array-search-for-a-range) |    两次Binary Search<br>[二分法模板](https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/er-fen-cha-zhao-xiang-jie)     |
|  124  | 困难 | [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) | [Binary Tree Maximum Path Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#124-binary-tree-maximum-path-sum) |    DFS后序遍历     |
| 周二 |  |  |  | ✅ |
|  341  | 中等 | [Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/) | [Flatten Nested List Iterator](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#341-flatten-nested-list-iterator) |    stack从后向前存     |
|  133  | 中等 | [Clone Graph](https://leetcode.com/problems/clone-graph/) | [Clone Graph](https://app.gitbook.com/@guilindev/s/interview/leetcode/graph#133-clone-graph) |    图的DFS和BFS     |
|  695  | 中等 | [Max Area of Island](https://leetcode.com/problems/max-area-of-island/) | [Max Area of Island](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#695-max-area-of-islands) |    同200，DFS/BFS/UnionFind     |
|  239  | 困难 | [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) | [Sliding Window Maximum](https://app.gitbook.com/@guilindev/s/interview/leetcode/heap#239-sliding-window-maximum) |    Heap     |
| 周三 |  |  |  | ✅ |
|  426  | 中等 | [Convert Binary Search Tree to Sorted Doubly Linked List](https://leetcode.com/problems/convert-binary-search-tree-to-sorted-doubly-linked-list/) | [Convert Binary Search Tree to Sorted Doubly Linked List](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#426-convert-binary-search-tree-to-sorted-doubly-linked-list) |    中序遍历     |
|  300  | 中等 | [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) | [Longest Increasing Subsequence](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#300-longest-increasing-subsequence) |    1. DP<br>2. Greedy + Binary Search     |
|  50  | 中等 | [Pow(x, n)](https://leetcode.com/problems/powx-n/) | [Pow(x, n)](https://app.gitbook.com/@guilindev/s/interview/leetcode/er-fen-sou-suo#50-power-x-n) |    二分+递归     |
|  45  | 困难 | [Jump Game II](https://leetcode.com/problems/jump-game-ii/) | [Jump Game II](https://app.gitbook.com/@guilindev/s/interview/leetcode/greedy#45-jump-game-ii) |    Greedy(BFS)     |
| 周四 |  |  |  | ✅ |
|  173  | 中等 | [Binary Search Tree Iterator](https://leetcode.com/problems/binary-search-tree-iterator/) | [Binary Search Tree Iterator](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#173-binary-search-tree-iterator) |    Stack模拟中序遍历     |
|  210  | 中等 | [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) | [Course Schedule II](https://app.gitbook.com/@guilindev/s/interview/leetcode/graph#210-course-schedule-ii) |    1.BFS<br>2.DFS     |
|  199  | 中等 | [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) | [Binary Tree Right Side View](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-3#199-binary-tree-right-side-view) |    1.树的BFS<br>2.树的DFS-根右左     |
|  212  | 困难 | [Word Search II](https://leetcode.com/problems/word-search-ii/) | [Word Search II](https://app.gitbook.com/@guilindev/s/interview/leetcode/trie-qian-zhui-shu#212-word-search-ii) |    Trie+Backtracking     |
| 周五 |  |  |  | ✅ |
|  105  | 中等 | [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) | [Construct Binary Tree from Preorder and Inorder Traversal](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#105-construct-binary-tree-from-preorder-and-inorder-traversal) |    1.递归，需要搞清楚递归的参数 <br>2.迭代，用Stack    |
|  277  | 中等 | [Find the Celebrity](https://leetcode.com/problems/find-the-celebrity/) | [Find the Celebrity](https://app.gitbook.com/@guilindev/s/interview/leetcode/graph#277-find-the-celebrity) |    出度为0     |
|  211  | 中等 | [Add and Search Word - Data structure design](https://leetcode.com/problems/add-and-search-word-data-structure-design/) | [Add and Search Word - Data structure design](https://app.gitbook.com/@guilindev/s/interview/leetcode/trie-qian-zhui-shu#211-add-and-search-word-data-structure-design) |    Trie     |
|  329  | 困难 | [Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/) | [Longest Increasing Path in a Matrix](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#329-longest-increasing-path-in-a-matrix) |    1.记忆化搜索<br>2.基于top sort的DP     |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第四周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  198  | 简单 | [House Robber](https://leetcode.com/problems/house-robber/) | [House Robber](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#198-house-robber) |    好好练习DP     |
|  545  | 中等 | [Boundary of Binary Tree](https://leetcode.com/problems/boundary-of-binary-tree/) | [Boundary of Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#545-boundary-of-binary-tree) |    1. 分成三部分 <br> 2. 先序     |
|  547  | 中等 | [Friend Circles](https://leetcode.com/problems/friend-circles/) | [Friend Circles](https://app.gitbook.com/@guilindev/s/interview/leetcode/gao-ji-de-shu-ju-jie-gou-he-suan-fa#547-friend-circles) |    1. DFS<br>2. BFS<br>3. Union Find     |
|  128  | 困难 | [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) | [Longest Consecutive Sequence](https://app.gitbook.com/@guilindev/s/interview/leetcode/array#128-longest-consecutive-sequence) |    1.HashSet<br>2.HashMap + DP<br>3. Union Find     |
| 周二 |  |  |  | ✅ |
|  235  | 简单 | [Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/) | [Lowest Common Ancestor of a Binary Search Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#235-lowest-common-ancestor-of-a-binary-search-tree) |    BST特性     |
|  208  | 中等 | [Implement Trie (Prefix Tree)](https://leetcode.com/problems/implement-trie-prefix-tree/) | [Implement Trie (Prefix Tree)](https://app.gitbook.com/@guilindev/s/interview/leetcode/trie-qian-zhui-shu#208-implement-trie-prefix-tree) |    挨个处理传入参数的字符即可     |
|  165  | 中等 | [Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/) | [Compare Version Numbers](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#165-compare-version-number) |    逐个比较每个小版本号     |
|  84  | 困难 | [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) | [Largest Rectangle in Histogram](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/array-zhong-de-shu-zi-zu-cheng-san-jiao-xing#84-largest-rectangle-in-histogram) |    1. 要知道暴力法，两边扩散<br>2. Stack + 哨兵，与85对比     |
| 周三 |  |  |  | ✅ |
|  110  | 简单 | [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) | [Balanced Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#110-balanced-binary-tree) |    求深度然后比较是否大于1     |
|  230  | 中等 | [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) | [Kth Smallest Element in a BST](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#230-kth-smallest-element-in-bst) |    InOrder     |
|  36  | 中等 | [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/) | [Valid Sudoku](https://app.gitbook.com/@guilindev/s/interview/leetcode/hash-table#36-valid-sudoku) |    three hashsets分別查row col cube     |
|  272  | 困难 | [Closest Binary Search Tree Value II](https://leetcode.com/problems/closest-binary-search-tree-value-ii/) | [Closest Binary Search Tree Value II](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#272-closest-binary-search-tree-value-ii) |    InOrder, LinkedList     |
| 周四 |  |  |  | ✅ |
|  28  | 简单 | [Implement strStr()](https://leetcode.com/problems/implement-strstr/) | [Implement strStr()](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#28-implement-substr) |    常规暴力解法<br>KMP要了解一下     |
|  611  | 中等 | [Valid Triangle Number](https://leetcode.com/problems/valid-triangle-number/) | [Valid Triangle Number](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/array-zhong-de-shu-zi-zu-cheng-san-jiao-xing#611-valid-triangle-number) |    固定最大边，双指针两条较小的边，类似3Sum     |
|  366  | 中等 | [Find Leaves of Binary Tree](https://leetcode.com/problems/find-leaves-of-binary-tree/) | [Find Leaves of Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#366-find-leaves-of-binary-tree) |    DFS，其实是先序     |
|  123  | 困难 | [Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/) | [Best Time to Buy and Sell Stock III](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#123-best-time-to-buy-and-sell-stock-iii) |    确定状态机的套路     |
| 周五 |  |  |  | ✅ |
|  346  | 简单 | [Moving Average from Data Stream](https://leetcode.com/problems/moving-average-from-data-stream/) | [Moving Average from Data Stream](https://app.gitbook.com/@guilindev/s/interview/leetcode/queue#346-moving-average-from-data-stream) |    LinkedList/Deque     |
|  209  | 中等 | [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) | [Minimum Size Subarray Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/hua-dong-chuang-kou#209-minimize-size-subarray-sum) |    双指针<br>二分法     |
|  240  | 中等 | [Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/) | [Search a 2D Matrix II](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/zai-array-zhong-cha-xun-yuan-su#240-search-a-2d-matrix-ii) |    从右上或者左下开始查找，每次去掉一行或一列     |
|  407  | 困难 | [Trapping Rain Water II](https://leetcode.com/problems/trapping-rain-water-ii/) | [Trapping Rain Water II](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#407-trapping-rain-water-ii) |    PQ + BFS     |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第五周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  339  | 简单 | [Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum/) | [Nested List Weight Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#339-nested-list-weight-sum) |    递归DFS     |
|  116  | 中等 | [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/) | [Populating Next Right Pointers in Each Node](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#116-populating-next-right-pointers-in-each-node) |    遍历到当前节点式，处理左右子树，DFS或BFS     |
|  114  | 中等 | [Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/) | [Flatten Binary Tree to Linked List]() |         |
|  305  | 困难 | [Number of Islands II](https://leetcode.com/problems/number-of-islands-ii/) | [Number of Islands II]() |         |
| 周二 |  |  |  |  |
|  463  | 简单 | [Island Perimeter](https://leetcode.com/problems/island-perimeter/) | [Island Perimeter]() |         |
|  284  | 中等 | [Peeking Iterator](https://leetcode.com/problems/peeking-iterator/) | [Peeking Iterator]() |         |
|  142  | 中等 | [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) | [Linked List Cycle II]() |         |
|  109  | 中等 | [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/) | [Convert Sorted List to Binary Search Tree]() |         |
| 周三 |  |  |  |  |
|  252  | 简单 | [Meeting Rooms](https://leetcode.com/problems/meeting-rooms/) | [Meeting Rooms]() |         |
|  130  | 中等 | [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/) | [Surrounded Regions]() |         |
|  285  | 中等 | [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/) | [Inorder Successor in BST]() |         |
|  450  | 中等 | [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) | [Delete Node in a BST]() |         |
| 周四 |  |  |  |  |
|  104  | 简单 | [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) | [Maximum Depth of Binary Tree]() |         |
|  150  | 中等 | [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/) | [Evaluate Reverse Polish Notation]() |         |
|  1008  | 中等 | [Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/) | [Construct Binary Search Tree from Preorder Traversal]() |         |
|  223  | 中等 | [Rectangle Area](https://leetcode.com/problems/rectangle-area/) | [Rectangle Area]() |         |
| 周五 |  |  |  |  |
|  704  | 简单 | [Binary Search](https://leetcode.com/problems/binary-search/) | [Binary Search]() |         |
|  244  | 中等 | [Shortest Word Distance II](https://leetcode.com/problems/shortest-word-distance-ii/) | [Shortest Word Distance II]() |         |
|  113  | 中等 | [Path Sum II](https://leetcode.com/problems/path-sum-ii/) | [Path Sum II]() |         |
|  654  | 中等 | [Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/) | [Maximum Binary Tree]() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第六周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  605  | 简单 | [Can Place Flowers](https://leetcode.com/problems/can-place-flowers/) | [Can Place Flowers]() |         |
|  1026  | 中等 | [Maximum Difference Between Node and Ancestor](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/) | [Maximum Difference Between Node and Ancestor]() |         |
|  86  | 中等 | [Partition List](https://leetcode.com/problems/partition-list/) | [Partition List]() |         |
|  51  | 困难 | [N-Queens](https://leetcode.com/problems/n-queens/) | [N-Queens]() |         |
| 周二 |  |  |  |  |
|  303  | 简单 | [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/) | [Range Sum Query - Immutable]() |         |
|  307  | 中等 | [Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/) | [Range Sum Query - Mutable]() |         |
|  946  | 中等 | [Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/) | [Validate Stack Sequences]() |         |
|  236  | 中等 | [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) | [Lowest Common Ancestor of a Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#236-lowest-common-ancestor-of-binary-tree) |         |
| 周三 |  |  |  |  |
|  206  | 简单 | [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | []() |         |
|  15  | 中等 | [3Sum](https://leetcode.com/problems/3sum/) | []() |         |
|  402  | 中等 | [Remove K Digits](https://leetcode.com/problems/remove-k-digits/) | [Remove K Digits]() |         |
|  22  | 中等 | [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) | [Generate Parentheses]() |         |
| 周四 |  |  |  |  |
|  290  | 简单 | [Word Pattern](https://leetcode.com/problems/word-pattern/) | [Word Pattern]() |         |
|  452  | 中等 | [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) | [Minimum Number of Arrows to Burst Balloons]() |         |
|  55  | 中等 | [Jump Game](https://leetcode.com/problems/jump-game/) | [Jump Game]() |         |
|  473  | 中等 | [Matchsticks to Square](https://leetcode.com/problems/matchsticks-to-square/) | [Matchsticks to Square]() |         |
| 周五 |  |  |  |  |
|  169  | 简单 | [Majority Element](https://leetcode.com/problems/majority-element/) | [Majority Element]() |         |
|  78  | 中等 | [Subsets](https://leetcode.com/problems/subsets/) | [Subsets]() |         |
|  187  | 中等 | [Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/) | [Repeated DNA Sequences]() |         |
|  120  | 中等 | [Triangle](https://leetcode.com/problems/triangle/) | [Triangle]() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第七周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  160  | 简单 | [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/) | [Intersection of Two Linked Lists]() |         |
|  1197  | 中等 | [Minimum Knight Moves](https://leetcode.com/problems/minimum-knight-moves/) | [Minimum Knight Moves]() |         |
|  1248  | 中等 | [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/) | [Count Number of Nice Subarrays]() |         |
|  727  | 困难 | [Minimum Window Subsequence](https://leetcode.com/problems/minimum-window-subsequence/) | [Minimum Window Subsequence]() |         |
| 周二 |  |  |  |  |
|  21  | 简单 | [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | [Merge Two Sorted Lists]() |         |
|  1371  | 中等 | [Find the Longest Substring Containing Vowels in Even Counts](https://leetcode.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/) | [Find the Longest Substring Containing Vowels in Even Counts]() |         |
| 863   | 中等 | [All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) | [All Nodes Distance K in Binary Tree]() |         |
|  6  | 中等 | [ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/) | [ZigZag Conversion]() |         |
| 周三 |  |  |  |  |
|  232  | 简单 | [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/) | [Implement Queue using Stacks]() |         |
|  8  | 中等 | [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/) | [String to Integer (atoi)]() |         |
|  62  | 中等 | [Unique Paths](https://leetcode.com/problems/unique-paths/) | [Unique Paths]() |         |
|  63  | 中等 | [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/) | [Unique Paths II]() |         |
| 周四 |  |  |  |  |
|  155  | 简单 | [Min Stack](https://leetcode.com/problems/min-stack/) | [Min Stack]() |         |
|  102  | 中等 | [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) | [Binary Tree Level Order Traversal]() |         |
|  153  | 中等 | [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | [Find Minimum in Rotated Sorted Array]() |         |
|  213  | 中等 | [House Robber II](https://leetcode.com/problems/house-robber-ii/) | [House Robber II]() |         |
| 周五 |  |  |  |  |
|  455  | 简单 | [Assign Cookies](https://leetcode.com/problems/assign-cookies/) | [Assign Cookies]() |         |
|  323  | 中等 | [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) | [Number of Connected Components in an Undirected Graph]() |         |
|  347  | 中等 | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | [Top K Frequent Elements]() |         |
|  373  | 中等 | [Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/) | [Find K Pairs with Smallest Sums]() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第八周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  108  | 简单 | [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/) | [Convert Sorted Array to Binary Search Tree]() |         |
|  929  | 简单 | [Unique Email Addresses](https://leetcode.com/problems/unique-email-addresses/) | [Unique Email Addresses]() |         |
|  1011  | 中等 | [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) | [Capacity To Ship Packages Within D Days]() |         |
|  887  | 困难 | [Super Egg Drop](https://leetcode.com/problems/super-egg-drop/) | [Super Egg Drop]() |         |
| 周二 |  |  |  |  |
|  538  | 简单 | [Convert BST to Greater Tree](https://leetcode.com/problems/convert-bst-to-greater-tree/) | [Convert BST to Greater Tree]() |         |
|  703  | 简单 | [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/) | [Kth Largest Element in a Stream]() |         |
|  776  | 中等 | [Split BST](https://leetcode.com/problems/split-bst/) | [Split BST]() |         |
|  779  | 中等 | [K-th Symbol in Grammar](https://leetcode.com/problems/k-th-symbol-in-grammar/) | [K-th Symbol in Grammar]() |         |
| 周三 |  |  |  |  |
|  35  | 简单 | [Search Insert Position](https://leetcode.com/problems/search-insert-position/) | []() |         |
|  674  | 中等 | [Longest Continuous Increasing Subsequence](https://leetcode.com/problems/longest-continuous-increasing-subsequence/) | [Longest Continuous Increasing Subsequence]() |         |
|  1143  | 中等 | [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) | [Longest Common Subsequence]() |         |
|    | 中等 | []() | []() |         |
| 周四 |  |  |  |  |
|  409  | 简单 | [Longest Palindrome](https://leetcode.com/problems/longest-palindrome/) | [Longest Palindrome]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
| 周五 |  |  |  |  |
|  136  | 简单 | [Single Number](https://leetcode.com/problems/single-number/) | [Single Number]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第九周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  88  | 简单 | [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) | [Merge Sorted Array]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周二 |  |  |  |  |
|  83  | 简单 | [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/) | [Remove Duplicates from Sorted List]() |         |
|  82  | 中等 | [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/) | [Remove Duplicates from Sorted List II]() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周三 |  |  |  |  |
|  111  | 简单 | [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/) | [Minimum Depth of Binary Tree]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周四 |  |  |  |  |
|  112  | 简单 | [Path Sum](https://leetcode.com/problems/path-sum/) | [Path Sum]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周五 |  |  |  |  |
|  121  | 简单 | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | [Best Time to Buy and Sell Stock]() |         |
|  122  | 简单 | [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) | [Best Time to Buy and Sell Stock II]() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第十周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  141  | 简单 | [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) | [Linked List Cycle]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周二 |  |  |  |  |
|  276  | 简单 | [Paint Fence](https://leetcode.com/problems/paint-fence/) | [Paint Fence]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周三 |  |  |  |  |
|  349  | 简单 | [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/) | [Intersection of Two Arrays]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周四 |  |  |  |  |
|  387  | 简单 | [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/) | [First Unique Character in a String]() |         |
|  392  | 简单 | [Is Subsequence](https://leetcode.com/problems/is-subsequence/) | [Is Subsequence]() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周五 |  |  |  |  |
|  617  | 简单 | [Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/) | [Merge Two Binary Trees]() |         |
|    | 中等 | []() | []() |         |
|    | 中等 | []() | []() |         |
|    | 困难 | []() | []() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

## 经典话题

[01背包问题](https://github.com/gaoshengnan/LeetCode/blob/master/src/main/java/theoreticalBasis/%E8%83%8C%E5%8C%85/backpack.md)
当被问到背包的时候，你第一个想到的是什么？点击查看回溯 + 动态规划两种方式解决背包问题

[背包九讲](https://www.kancloud.cn/kancloud/pack/70124)

[LRU](https://mp.weixin.qq.com/s/DhLCNAcenjn7-BcoQ3wUOw) LRU主要考察你什么？

## 系统设计
#### General
0. Designing Data Intensive Application [中文版](https://github.com/Vonng/ddia)

1. [General互联网产品的设计](https://medium.com/better-programming/how-to-design-a-web-application-software-architecture-101-df568b88da76)

2. [Tushar Roy算法和系统设计](https://www.youtube.com/channel/UCZLJf_R2sWyUtXSKiKlyvAw)

3. [Tech Dummies系统设计](https://www.youtube.com/channel/UCn1XnDWhsLS5URXTi5wtFTA)

4. [Gaurav Sen系统设计](https://www.youtube.com/channel/UCRPMAqdtSgd0Ipeef7iFsKw)

#### Metrics System
1. [新手也能看懂的监控报警系统架构设计](https://dbaplus.cn/news-141-2038-1.html)
2. [中小型运维团队如何设计运维自动化平台](https://zhuanlan.zhihu.com/p/31285905)

#### Distributed Transaction
1. [Distributed Transactions with MicroServices](https://www.youtube.com/watch?v=S4FnmSeRpAY)
2. [分布式文件系统](https://cloud.tencent.com/developer/article/1645680)

#### DB 

#### Log System

#### Microservice

#### Message Queue

#### Chat Apps

#### Rate Limiter

#### Payment Systems
1. [被问到“设计一个支付系统”的思考角度](https://medium.com/get-ally/how-to-architect-online-payment-processing-system-for-an-online-store-6dc84350a39)
2. [支付平台架构设计的一些思考](http://objcoding.com/2019/06/04/payment-platform/)
3. [Avoiding Double Payments in a Distributed Payments System](https://medium.com/airbnb-engineering/avoiding-double-payments-in-a-distributed-payments-system-2981f6b070bb)
4. [Paymeng System和API Server如何互相验证1](https://en.wikipedia.org/wiki/Payment_gateway), [Paymeng System和API Server如何互相验证2](https://www.youtube.com/watch?v=GUurzvS3DlY)
5. [Uber支付系统案例](https://www.youtube.com/watch?v=MJABqwzBkHs)

#### Cache

#### Compiler

## Behavioral Questions
1. [100个General BQ与答案](https://collegegrad.com/tough-interview-questions)
2. [Amazon 14条行为准则]()
3. [Netflix文化手册]()


