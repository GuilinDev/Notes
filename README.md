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

每道题的[时间安排](https://medium.com/@alimirio/how-to-solve-problems-on-leetcode-to-prepare-for-technical-interviews-e74781b865d2)。
  
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
| 周一 |  |  |  | ✅ |
|  339  | 简单 | [Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum/) | [Nested List Weight Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#339-nested-list-weight-sum) |    递归DFS     |
|  116  | 中等 | [Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/) | [Populating Next Right Pointers in Each Node](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#116-populating-next-right-pointers-in-each-node) |    遍历到当前节点式，处理左右子树，DFS或BFS     |
|  114  | 中等 | [Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/) | [Flatten Binary Tree to Linked List](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#114-flatten-binary-tree-to-linked-list) |    1. 先序迭代<br>2.后序遍历     |
|  305  | 困难 | [Number of Islands II](https://leetcode.com/problems/number-of-islands-ii/) | [Number of Islands II](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#305-number-of-islands-ii) |    Union Find     |
| 周二 |  |  |  | ✅ |
|  463  | 简单 | [Island Perimeter](https://leetcode.com/problems/island-perimeter/) | [Island Perimeter](https://app.gitbook.com/@guilindev/s/interview/leetcode/hash-table#463-island-perimeter) |    直接遍历，按照遍历顺序优化只用检查右边和下边的就行     |
|  284  | 中等 | [Peeking Iterator](https://leetcode.com/problems/peeking-iterator/) | [Peeking Iterator](https://app.gitbook.com/@guilindev/s/interview/leetcode/7.-design#284-peeking-iterator) |    在Implemented的迭代器基础上新增一个变量记录头部元素即可     |
|  142  | 中等 | [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) | [Linked List Cycle II](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#142-linked-list-cycle-ii) |    先两步一步，再一步一步     |
|  109  | 中等 | [Convert Sorted List to Binary Search Tree](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/) | [Convert Sorted List to Binary Search Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#109-convert-sorted-list-to-binary-search-tree) |    快慢指针找中点，递归构建     |
| 周三 |  |  |  | ✅ |
|  252  | 简单 | [Meeting Rooms](https://leetcode.com/problems/meeting-rooms/) | [Meeting Rooms](https://app.gitbook.com/@guilindev/s/interview/leetcode/hui-wen-jie-gou#252-meeting-rooms) |    对会议开始时间进行排序，检查后一个会议的开始时间是否早于前一个会议的结束时间     |
|  130  | 中等 | [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/) | [Surrounded Regions](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#130-surrounded-regions) |    1.DFS<br>2.BFS<br>3.Union Find     |
|  285  | 中等 | [Inorder Successor in BST](https://leetcode.com/problems/inorder-successor-in-bst/) | [Inorder Successor in BST](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#285-inorder-successor-in-bst) |    中序遍历     |
|  450  | 中等 | [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) | [Delete Node in a BST](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#450-delete-node-in-a-bst) |    找到待删除节点后的处理情况     |
| 周四 |  |  |  | ✅ |
|  104  | 简单 | [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) | [Maximum Depth of Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#104-maximum-depth-of-binary-tree) |    DFS/BFS     |
|  150  | 中等 | [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/) | [Evaluate Reverse Polish Notation](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#150-evaluate-reverse-polish-notation) |    1.Stack<br>2.递归     |
|  1008  | 中等 | [Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/) | [Construct Binary Search Tree from Preorder Traversal](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#1008-construct-binary-search-tree-from-preorder-traversal) |    1. 递归<br>2.stack     |
|  223  | 中等 | [Rectangle Area](https://leetcode.com/problems/rectangle-area/) | [Rectangle Area](https://app.gitbook.com/@guilindev/s/interview/leetcode/math#223-rectangle-area) |    先求两矩形面积，再减去重叠区面积     |
| 周五 |  |  |  | ✅ |
|  704  | 简单 | [Binary Search](https://leetcode.com/problems/binary-search/) | [Binary Search](https://app.gitbook.com/@guilindev/s/interview/leetcode/er-fen-sou-suo#704-binary-search) |    模板     |
|  244  | 中等 | [Shortest Word Distance II](https://leetcode.com/problems/shortest-word-distance-ii/) | [Shortest Word Distance II](https://app.gitbook.com/@guilindev/s/interview/leetcode/hash-table#244-shortest-word-distance-ii) |    HashMap     |
|  113  | 中等 | [Path Sum II](https://leetcode.com/problems/path-sum-ii/) | [Path Sum II](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#113-path-sum-ii) |    DFS回溯     |
|  654  | 中等 | [Maximum Binary Tree](https://leetcode.com/problems/maximum-binary-tree/) | [Maximum Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#654-maximum-binary-tree) |    递归     |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第六周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  605  | 简单 | [Can Place Flowers](https://leetcode.com/problems/can-place-flowers/) | [Can Place Flowers](https://app.gitbook.com/@guilindev/s/interview/leetcode/array#605-can-place-flowers) |    贪心     |
|  1026  | 中等 | [Maximum Difference Between Node and Ancestor](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/) | [Maximum Difference Between Node and Ancestor](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#1026-maximum-difference-between-node-and-ancestor) |    DFS找节点和其左右子树的最大值和最小值     |
|  86  | 中等 | [Partition List](https://leetcode.com/problems/partition-list/) | [Partition List](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#86-partition-list) |    双指针，交换指针的下一个元素     |
|  51  | 困难 | [N-Queens](https://leetcode.com/problems/n-queens/) | [N-Queens](https://app.gitbook.com/@guilindev/s/interview/leetcode/backtracking#51-n-queens) |    Backtracking     |
| 周二 |  |  |  | ✅ |
|  303  | 简单 | [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/) | [Range Sum Query - Immutable](https://app.gitbook.com/@guilindev/s/interview/leetcode/design#303-range-sum-query-immutable) |    1.直接做<br>2.记忆化搜索     |
|  307  | 中等 | [Range Sum Query - Mutable](https://leetcode.com/problems/range-sum-query-mutable/) | [Range Sum Query - Mutable](https://app.gitbook.com/@guilindev/s/interview/leetcode/design#307-range-sum-query-mutable) |    1.直接做<br>2.线段树     |
|  946  | 中等 | [Validate Stack Sequences](https://leetcode.com/problems/validate-stack-sequences/) | [Validate Stack Sequences](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#946-validate-stack-sequence) |    用栈模拟过程     |
|  236  | 中等 | [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) | [Lowest Common Ancestor of a Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#236-lowest-common-ancestor-of-binary-tree) |    根据节点所处的位置进行递归     |
| 周三 |  |  |  | ✅ |
|  206  | 简单 | [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) | [Reverse Linked List](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#206-reverse-linked-list) |    迭代和递归都掌握     |
|  15  | 中等 | [3Sum](https://leetcode.com/problems/3sum/) | [3Sum](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/ksum#15-3sum) |    双指针的扩展-三指针     |
|  402  | 中等 | [Remove K Digits](https://leetcode.com/problems/remove-k-digits/) | [Remove K Digits](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#402-remove-k-digits) |    删除较大的左邻居     |
|  22  | 中等 | [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/) | [Generate Parentheses](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#22-generate-parentheses) |     递归检查左右括号的剩余数量    |
| 周四 |  |  |  | ✅ |
|  290  | 简单 | [Word Pattern](https://leetcode.com/problems/word-pattern/) | [Word Pattern](https://app.gitbook.com/@guilindev/s/interview/leetcode/hash-table#290-word-pattern) |    HashMap 可用另外一个HashMap替代containsValue()     |
|  452  | 中等 | [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) | [Minimum Number of Arrows to Burst Balloons](https://app.gitbook.com/@guilindev/s/interview/leetcode/greedy#452-minimum-number-of-arrows-to-burst-balloons) |    贪心，注意按照左右边缘排序的区别     |
|  55  | 中等 | [Jump Game](https://leetcode.com/problems/jump-game/) | [Jump Game](https://app.gitbook.com/@guilindev/s/interview/leetcode/greedy#55-jump-game) |    1.DP比较前一个元素和前一个状态<br>2.贪心     |
|  473  | 中等 | [Matchsticks to Square](https://leetcode.com/problems/matchsticks-to-square/) | [Matchsticks to Square](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#473-matchsticks-to-square) |    DFS并剪枝     |
| 周五 |  |  |  | ✅ |
|  169  | 简单 | [Majority Element](https://leetcode.com/problems/majority-element/) | [Majority Element](https://app.gitbook.com/@guilindev/s/interview/leetcode/array#169-majority-element) |    投票算法     |
|  78  | 中等 | [Subsets](https://leetcode.com/problems/subsets/) | [Subsets](https://app.gitbook.com/@guilindev/s/interview/leetcode/backtracking#78-subsets) |    [回溯模板](https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning))     |
|  187  | 中等 | [Repeated DNA Sequences](https://leetcode.com/problems/repeated-dna-sequences/) | [Repeated DNA Sequences](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled#187-repeated-dna-sequence) |    两个sets:<br>1.滑动窗口<br>2.位操作     |
|  120  | 中等 | [Triangle](https://leetcode.com/problems/triangle/) | [Triangle](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#120-triangle) |   DP从最后一行开始递推      |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第七周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  160  | 简单 | [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/) | [Intersection of Two Linked Lists](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#160-intersection-of-two-linked-lists) |    确保两个指针走相同长度的路     |
|  1197  | 中等 | [Minimum Knight Moves](https://leetcode.com/problems/minimum-knight-moves/) | [Minimum Knight Moves](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-3#1197-minimum-knight-moves) |    BFS最短路径     |
|  1248  | 中等 | [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/) | [Count Number of Nice Subarrays](https://app.gitbook.com/@guilindev/s/interview/leetcode/hua-dong-chuang-kou#1248-count-number-of-nice-subarrays) |    1.双指针<br>2.前缀和     |
|  727  | 困难 | [Minimum Window Subsequence](https://leetcode.com/problems/minimum-window-subsequence/) | [Minimum Window Subsequence](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#727-minimum-window-subsequence) |    二维DP     |
| 周二 |  |  |  | ✅ |
|  21  | 简单 | [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) | [Merge Two Sorted Lists](https://app.gitbook.com/@guilindev/s/interview/leetcode/linkedlist#21-merge-two-sorted-lists) |    dummy迭代和递归都要掌握     |
|  1371  | 中等 | [Find the Longest Substring Containing Vowels in Even Counts](https://leetcode.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/) | [Find the Longest Substring Containing Vowels in Even Counts](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#1371-find-the-longest-substring-containing-vowels-in-even-counts) |    前缀和+状态压缩     |
| 863   | 中等 | [All Nodes Distance K in Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) | [All Nodes Distance K in Binary Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#863-all-nodes-distance-k-in-binary-tree) |    1.DFS<br>2.BFS当作图处理     |
|  6  | 中等 | [ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/) | [ZigZag Conversion](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#6-zigzag-conversion) |    坐标转换     |
| 周三 |  |  |  | ✅ |
|  232  | 简单 | [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/) | [Implement Queue using Stacks](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#232-implement-queue-using-stacks) |    两个stacks     |
|  8  | 中等 | [String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/) | [String to Integer (atoi)](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#8-string-to-integer-atoi) |    空格/正负号/越界等corner cases     |
|  62  | 中等 | [Unique Paths](https://leetcode.com/problems/unique-paths/) | [Unique Paths](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#62-unique-paths) |    DP并考虑状态压缩     |
|  63  | 中等 | [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/) | [Unique Paths II](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#63-unique-path-ii) |    DP并考虑状态压缩，障碍物影响路径状态     |
| 周四 |  |  |  | ✅ |
|  155  | 简单 | [Min Stack](https://leetcode.com/problems/min-stack/) | [Min Stack](https://app.gitbook.com/@guilindev/s/interview/leetcode/stack#155-min-stack) |    1.两个stack<br>2.一个stack，最小值存在栈顶元素下     |
|  102  | 中等 | [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) | [Binary Tree Level Order Traversal](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#102-binary-tree-level-order-traversal) |    1. BFS<br>2. DFS了解     |
|  153  | 中等 | [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) | [Find Minimum in Rotated Sorted Array](https://app.gitbook.com/@guilindev/s/interview/leetcode/array/zai-array-zhong-cha-xun-yuan-su#153-find-minimum-in-rotated-sorted-array) |    按情况Binary Search     |
|  213  | 中等 | [House Robber II](https://leetcode.com/problems/house-robber-ii/) | [House Robber II](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#213-house-robber-ii) |    分区间DP     |
| 周五 |  |  |  | ✅ |
|  455  | 简单 | [Assign Cookies](https://leetcode.com/problems/assign-cookies/) | [Assign Cookies](https://app.gitbook.com/@guilindev/s/interview/leetcode/greedy#455-assign-cookies) |    排序+贪心     |
|  323  | 中等 | [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) | [Number of Connected Components in an Undirected Graph](https://app.gitbook.com/@guilindev/s/interview/leetcode/dfs#323-number-of-connected-components-in-an-undirected-graph) |    1. DFS<br>2. BFS<br>3. Union Find     |
|  347  | 中等 | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) | [Top K Frequent Elements](https://app.gitbook.com/@guilindev/s/interview/leetcode/hash-table#347-top-k-frequent-elements) |    1. HashMap + 最大堆<br>2. TreeMap<br>3. 桶排序     |
|  373  | 中等 | [Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/) | [Find K Pairs with Smallest Sums](https://app.gitbook.com/@guilindev/s/interview/leetcode/heap#373-find-k-pairs-with-smallest-sums) |    最小堆     |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第八周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  | ✅ |
|  108  | 简单 | [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/) | [Convert Sorted Array to Binary Search Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#108-convert-sorted-array-to-binary-search-tree) |    二分搜索父节点     |
|  929  | 简单 | [Unique Email Addresses](https://leetcode.com/problems/unique-email-addresses/) | [Unique Email Addresses](https://app.gitbook.com/@guilindev/s/interview/leetcode/string#929-unique-email-address) |    直接思路，hashset除重     |
|  1011  | 中等 | [Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/) | [Capacity To Ship Packages Within D Days](https://app.gitbook.com/@guilindev/s/interview/leetcode/er-fen-sou-suo#1011-capacity-to-ship-packages-within-d-days) |    二分搜索     |
|  887  | 困难 | [Super Egg Drop](https://leetcode.com/problems/super-egg-drop/) | [Super Egg Drop](https://app.gitbook.com/@guilindev/s/interview/leetcode/divide-and-conquer#887-super-egg-drop) |    记忆化搜索，DP     |
| 周二 |  |  |  |  |
|  538  | 简单 | [Convert BST to Greater Tree](https://leetcode.com/problems/convert-bst-to-greater-tree/) | [Convert BST to Greater Tree](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#538-convert-bst-to-greater-tree) |    先右后左     |
|  703  | 简单 | [Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/) | [Kth Largest Element in a Stream](https://app.gitbook.com/@guilindev/s/interview/leetcode/heap#703-kth-largest-element-in-a-stream) |    优先队列实现小顶堆     |
|  776  | 中等 | [Split BST](https://leetcode.com/problems/split-bst/) | [Split BST](https://app.gitbook.com/@guilindev/s/interview/leetcode/untitled-1#776-split-bst) |    递归，根据当前root值，连接左子树的较大部分或右子树的较小部分     |
|  779  | 中等 | [K-th Symbol in Grammar](https://leetcode.com/problems/k-th-symbol-in-grammar/) | [K-th Symbol in Grammar]() |         |
| 周三 |  |  |  |  |
|  35  | 简单 | [Search Insert Position](https://leetcode.com/problems/search-insert-position/) | []() |         |
|  674  | 中等 | [Longest Continuous Increasing Subsequence](https://leetcode.com/problems/longest-continuous-increasing-subsequence/) | [Longest Continuous Increasing Subsequence]() |         |
|  1143  | 中等 | [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) | [Longest Common Subsequence]() |         |
|  11  | 中等 | [Container With Most Water ](https://leetcode.com/problems/container-with-most-water/) | [Container With Most Water ]() |         |
| 周四 |  |  |  |  |
|  409  | 简单 | [Longest Palindrome](https://leetcode.com/problems/longest-palindrome/) | [Longest Palindrome]() |         |
|  54  | 中等 | [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/) | [Spiral Matrix]() |         |
|  59  | 中等 | [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/) | [Spiral Matrix II]() |         |
|  17  | 中等 | [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/) | [Letter Combinations of a Phone Number]() |         |
| 周五 |  |  |  |  |
|  136  | 简单 | [Single Number](https://leetcode.com/problems/single-number/) | [Single Number]() |         |
|  7  | 简单 | [Reverse Integer](https://leetcode.com/problems/reverse-integer/) | [Reverse Integer]() |         |
|  19  | 中等 | [Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) | [Remove Nth Node From End of List]() |         |
|  238  | 中等 | [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) | [Product of Array Except Self]() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第九周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  88  | 简单 | [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) | [Merge Sorted Array]() |         |
|  380  | 中等 | [Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/) | [Insert Delete GetRandom O(1)]() |         |
|  378  | 中等 | [Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) | [Kth Smallest Element in a Sorted Matrix]() |         |
|  269  | 困难 | [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) | [Alien Dictionary]() |         |
| 周二 |  |  |  |  |
|  83  | 简单 | [Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/) | [Remove Duplicates from Sorted List]() |         |
|  82  | 中等 | [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/) | [Remove Duplicates from Sorted List II]() |         |
|  348  | 中等 | [Design Tic-Tac-Toe](https://leetcode.com/problems/design-tic-tac-toe/) | [Design Tic-Tac-Toe]() |         |
|  289  | 中等 | [Game of Life](https://leetcode.com/problems/game-of-life/) | [Game of Life]() |         |
| 周三 |  |  |  |  |
|  111  | 简单 | [Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/) | [Minimum Depth of Binary Tree]() |         |
|  234  | 简单 | [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) | [Palindrome Linked List]() |         |
|  48  | 中等 | [Rotate Image](https://leetcode.com/problems/rotate-image/) | [Rotate Image]() |         |
|  152  | 中等 | [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) | [Maximum Product Subarray]() |         |
| 周四 |  |  |  |  |
|  112  | 简单 | [Path Sum](https://leetcode.com/problems/path-sum/) | [Path Sum]() |         |
|  202  | 简单 | [Happy Number](https://leetcode.com/problems/happy-number/) | [Happy Number]() |         |
|  179  | 中等 | [Largest Number](https://leetcode.com/problems/largest-number/) | [Largest Number](https://leetcode.com/problems/largest-number/) |         |
|  75  | 中等 | [Sort Colors](https://leetcode.com/problems/sort-colors/) | [Sort Colors]() |         |
| 周五 |  |  |  |  |
|  121  | 简单 | [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | [Best Time to Buy and Sell Stock]() |         |
|  122  | 简单 | [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) | [Best Time to Buy and Sell Stock II]() |         |
|  315  | 困难 | [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/) | [Count of Smaller Numbers After Self]() |         |
|  218  | 困难 | [The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/) | [The Skyline Problem]() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> 第十周

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  141  | 简单 | [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) | [Linked List Cycle]() |         |
|  13  | 简单 | [Roman to Integer](https://leetcode.com/problems/roman-to-integer/) | [Roman to Integer]() |         |
|  148  | 中等 | [Sort List](https://leetcode.com/problems/sort-list/) | [Sort List]() |         |
|  76  | 困难 | [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) | [Minimum Window Substring]() |         |
| 周二 |  |  |  |  |
|  276  | 简单 | [Paint Fence](https://leetcode.com/problems/paint-fence/) | [Paint Fence]() |         |
|  14  | 简单 | [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/) | [Longest Common Prefix]() |         |
|  131  | 中等 | [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/) | [Palindrome Partitioning]() |         |
|  287  | 中等 | [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) | [Find the Duplicate Number]() |         |
| 周三 |  |  |  |  |
|  349  | 简单 | [Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/) | [Intersection of Two Arrays]() |         |
|  166  | 中等 | [Fraction to Recurring Decimal](https://leetcode.com/problems/fraction-to-recurring-decimal/) | [Fraction to Recurring Decimal]() |         |
|  279  | 中等 | [Perfect Squares](https://leetcode.com/problems/perfect-squares/) | [Perfect Squares]() |         |
|  395  | 中等 | [Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/) | [Longest Substring with At Least K Repeating Characters]() |         |
| 周四 |  |  |  |  |
|  387  | 简单 | [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/) | [First Unique Character in a String]() |         |
|  392  | 简单 | [Is Subsequence](https://leetcode.com/problems/is-subsequence/) | [Is Subsequence]() |         |
|  221  | 中等 | [Maximal Square](https://leetcode.com/problems/maximal-square/) | [Maximal Square]() |         |
|  149  | 困难 | [Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line/) | [Max Points on a Line]() |         |
| 周五 |  |  |  |  |
|  617  | 简单 | [Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/) | [Merge Two Binary Trees]() |         |
|  204  | 简单 | [Count Primes](https://leetcode.com/problems/count-primes/) | [Count Primes]() |         |
|  41  | 中等 | [First Missing Positive](https://leetcode.com/problems/first-missing-positive/) | [First Missing Positive]() |         |
|  340  | 困难 | [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) | [Longest Substring with At Most K Distinct Characters]() |         |
| 周六周日重写不够熟悉的题目 |  |  |  |  |

> extra

| &emsp;题号&emsp; | &emsp;难度&emsp; | 题目链接&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;| 简单总结 |
| :--: | :--: | :----------------------------------------------------------- | :----------------------------------------------------------- | :------: |
| 周一 |  |  |  |  |
|  448  | 简单 | [Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/) | [Find All Numbers Disappeared in an Array]() |         |
|  394  | 中等 | [Decode String](https://leetcode.com/problems/decode-string/) | [Decode String]() |         |
|  338  | 中等 | [Counting Bits](https://leetcode.com/problems/counting-bits/) | [Counting Bits]() |         |
|  406  | 中等 | [Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/) | [Queue Reconstruction by Height]() |         |
| 周二 |  |  |  |  |
|  438  | 中等 | [Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/) | [Find All Anagrams in a String]() |         |
|  416  | 中等 | [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) | [Partition Equal Subset Sum]() |         |
|  437  | 中等 | [Path Sum III](https://leetcode.com/problems/path-sum-iii/) | [Path Sum III]() |         |
|  494  | 中等 | [Target Sum](https://leetcode.com/problems/target-sum/) | [Target Sum]() |         |
| 周三 |  |  |  |  |
|  543  | 简单 | [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) | [Diameter of Binary Tree]() |         |
|  647  | 简单 | [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) | [Palindromic Substrings]() |         |
|  739  | 中等 | [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) | [Daily Temperatures]() |         |
|  162  | 中等 | [Find Peak Element](https://leetcode.com/problems/find-peak-element/) | [Find Peak Element]() |         |
| 周四 |  |  |  |  |
|  242  | 简单 | [Valid Anagram](https://leetcode.com/problems/valid-anagram/) | [Valid Anagram]() |         |
|  268  | 简单 | [Missing Number](https://leetcode.com/problems/missing-number/) | [Missing Number]() |         |
|  73  | 中等 | [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/) | [Set Matrix Zeroes]() |         |
|  29  | 中等 | [Divide Two Integers](https://leetcode.com/problems/divide-two-integers/) | [Divide Two Integers]() |         |
| 周五 |  |  |  |  |
|  38  | 简单 | [Count and Say](https://leetcode.com/problems/count-and-say/) | [Count and Say]() |         |
|  189  | 简单 | [Rotate Array](https://leetcode.com/problems/rotate-array/) | [Rotate Array]() |         |
|  384  | 中等 | [Shuffle an Array](https://leetcode.com/problems/shuffle-an-array/) | [Shuffle an Array]() |         |
|  44  | 困难 | [Wildcard Matching](https://leetcode.com/problems/wildcard-matching/) | [Wildcard Matching]() |         |
| 周六 |  |  |  |  |
|  101  | 简单 | [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/) | [Symmetric Tree]() |         |
|  70  | 简单 | [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) | [Climbing Stairs]() |         |
|  134  | 中等 | [Gas Station](https://leetcode.com/problems/gas-station/) | [Gas Station]() |         |
|  140  | 困难 | [Word Break II](https://leetcode.com/problems/word-break-ii/) | [Word Break II]() |         |
| 周日 |  |  |  |  |
|    | 简单 | []() | []() |         |
|    | 简单 | []() | []() |         |
|  877  | 中等 | [Stone Game](https://leetcode.com/problems/stone-game/) | [Stone Game]() |         |
|    | 困难 | []() | []() |         |

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

#### 案例
1. Design a Chat System (Facebook messenger, Whatsapp)
2. Design a Video Streaming Service (YouTube, Netflix)
3. Design a Key-value Store
4. Design a URL shortener
5. Design a Web Crawler
6. Design a Shared Cloud Drive (Google Drive, Dropbox)
7. Design a News feed System
8. Design a Search Autocomplete System
9. Design a Notification System
10. Design a scalable system that supports millions of users

## Behavioral Questions
1. [100个General BQ与答案](https://collegegrad.com/tough-interview-questions)
2. [Amazon 14条行为准则]()
3. [Netflix文化手册]()


