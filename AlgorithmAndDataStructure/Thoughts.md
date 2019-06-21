## 思路总结

##### 1 Two Sum
HashMap办法，值作为key，index作为value；二分查找，先System.arraycopy复制一个新的array，然后把新的array排序，二分查找找到两个值，然后将两个值在原来的数组中找到indices；
可以用throw new IllegalArgumentException("No two sum solution")来检查输入让代码更健壮。
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        //HashMap
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (hashMap.containsKey(complement)) {
                return new int[]{hashMap.get(complement), i};
            }
            hashMap.put(nums[i], i);
        }
        throw new IllegalArgumentException("No two sum solution");

        //双指针
//        int len = nums.length;
//        List<Integer> list = new ArrayList<>();
//        int[] copiedArray = new int[len];
//        System.arraycopy(nums, 0, copiedArray, 0, len);
//
//        Arrays.sort(copiedArray);
//        int left = 0;
//        int right = len - 1;
//        while (left < right) {
//            int sum = copiedArray[left] + copiedArray[right];
//            if (sum == target) {
//                break;
//            } else if (sum < target) {
//                left++;
//            } else {
//                right--;
//            }
//        }
//        if (copiedArray[left] + copiedArray[right] != target) {
//            throw new IllegalArgumentException("No two sum solution");
//        }
//        for (int i = 0; i < len; i++) {
//            if (nums[i] == copiedArray[left] || nums[i] == copiedArray[right]) {
//                list.add(i);
//            }
//        }
//        int[] result = new int[2];
//        result[0] = list.get(0);
//        result[1] = list.get(1);
//        return result;
    }
}
```

##### 3 Longest Substring without Repeating Characters
双指针创建sliding window，利用HashMap<Character, Integer>, 遍历字符串的字符，key是字符串里的字符，value是记录该字符上一次出现的位置，left = Math.max(left, map.get(s.charAt(i)) + 1)更新左指针代表sliding window的左边界，右指针一直往前知道最末。

##### 5 Longest Panlindromic Substring
方法1：遍历字符串中的每一个字符，将这个字符和它的下一位作为center，两边扩展，记录一个最大的子字符串的长度；
方法2：DP的办法，二维DP。dp[i][j]表示从j到i是否是回文，判断i和j是否在同一位/相邻/不相邻的情况；
方法3：Manacher‘s算法，现在不要求；

##### 7 Reverse Integer
这道题不用单独设置一个flag来记录传入的数是否为正数或负数，只需要在while循环中设置while(x != 0)而不是while (x > 0)即可，另外返回值result的类型为long，最后case回来，因为数翻转后有可能超出Integer的范围，所以还要在while循环中检查result是否越界。

##### 9 Palindrome Number
用一个变量记录右半部分的数字，x每次减小代表左半部分，直到左半部分小于右半部分，最后检查两部分是否相等或者左半部分等于右半部分除以10（奇数位）. corner cases：0直接返回true，负数和末尾为0的正数直接返回false。

##### 15 3Sum
1)在暴力解法的基础上，枚举两个数a和b(O(N^2))，最后一个数用set来找是否有-(a+b)的存在，把找到的三个数存入结果; 2)先排序，然后三个索引，其中第一个索引套在外面，另外两个索引左右遍历Array，找到合适的triplets存入结果，时间同样为O(N^2)。

使用Set,这个用Java写不好去重，Python会比较方便
```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums) < 3:
            return []
        nums.sort()
        res = set()
        for i, v in enumerate(nums[:-2]):
            if i >= 1 and v == nums[i-1]:
                continue
            d = {}
            for x in nums[i+1:]:
                if x not in d:
                    d[-v-x] = 1
                else:
                    res.add((v, -v-x, x))
        return map(list,res)
```
嵌套后两边往中间走（推荐）
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums == null || nums.length < 3) {
            return new ArrayList<List<Integer>>();
        }
        List<List<Integer>> results = new ArrayList<>();
        HashSet<List<Integer>> noDups = new HashSet<>();

        Arrays.sort(nums);

        int len = nums.length;
        for (int first = 0; first < len - 2; first++) {
            int second = first + 1;
            int third = len - 1;

            while (second < third) {
                if (nums[second] + nums[third] == -nums[first]) {
                    List<Integer> oneResult = new ArrayList<>();
                    oneResult.add(nums[first]);
                    oneResult.add(nums[second]);
                    oneResult.add(nums[third]);

                    if (noDups.add(oneResult)) {
                        results.add(oneResult);
                    }

                    //如果找到相等的三联体，second和third就同时走一步，因为如果second或third单独走的话，肯定不会等于0或者就是和刚才找到的的三联体相重复
                    second++;
                    third--;
                } else if (nums[second] + nums[third] < -nums[first]) {
                    second++;
                } else {
                    third--;
                }
            }
        }
        return results;
    }
}
```

##### 17 Letter Combinations of a Phone Number
BFS做法，创建一个对应每个键的string array，依然用queue，考虑树形结构，按层次来，第一层为空，第二层为在空的基础上加上一个字符，第三层在第二层的基础上再加上一个字符，直到某一层节点字符串的长度等于所要求的长度就返回该层所有节点。

DFS做法，创建一个对应每个键的string array，递归树中，当字符串长度等于要求的长度时作为出口，否则还未达到长度的时候，依次找到输入的字符串对应的按键的字符，用offset控制是哪一个按键，进入下一层递归，直到长度符合。

##### 20 Valid Parentheses
Stack经典题，并且没有别的好的办法（比如用replace消掉成对的括号，时间复杂度为O^2)，遍历字符串的字符，如果是左括号，压入；如果是右括号，跟栈顶的元素比较，遍历完后判断一下栈为空即可，有个小技巧是另外再创建一个hashmap保存三种括号，右括号为key，左括号为value，这样遍历的时候写法会比较简洁。
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        Map<Character, Character> map = new HashMap<>();
        //右括号当作key，方便查找作为value的左括号
        map.put(')', '(');
        map.put('}', '{');
        map.put(']', '[');

        for (char ch : s.toCharArray()) {
            if (!map.containsKey(ch)) {//检查是否是左括号，因为key都是右括号
                stack.push(ch);
            } else if (stack.isEmpty() || stack.pop() != map.get(ch)){//是右括号就直接把map的value和栈顶元素对比
                return false;
            }
        }
     
        return stack.isEmpty();
    }
}
```
##### 21 Merge Two Sorted Lists

##### 22 Generate Parentheses
数学归纳法代码写起来复杂，所以还是用类似DFS的办法，朴素的DFS的办法就是有2n个格子，每个格子可以放左括号和右括号，然后检查每一个组合是否validate，这个时间复杂度为2^2n，改进的做法则是对DFS进行剪枝，如果在深度优先*搜索*的时候，添加左括号的时候发现左括号有剩余才可以继续进行搜索，添加右括号的时候发现右括号有剩余，并且右括号剩余比左括号多（不能等于，因为当前要添加的括号是右括号）的时候添加右括号。。其余的路径就被剪掉了。。最后当左括号和右括号都没剩的时候，说明合法，加入到结果，这种解法复杂度为2^n，但是比未优化的时候会快很多。
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> results = new ArrayList<>();
        generateParenthesisOneByOne(results, n, n, "");
        return results;
    }
    private void generateParenthesisOneByOne(List<String> results, int left, int right, String oneResult) {
        //左右括号都没剩余的，已经组装完一个合法的括号组合，这时候才可以加入到结果中
        if (left == 0 && right == 0) {
            results.add(oneResult);
            return;
        }

        if (left > 0) {//左括号还有剩余，可以继续加
            generateParenthesisOneByOne(results, left - 1, right, oneResult + "(");
        }

        if (right > left) {//严格来说这里的条件是right > 0 && right > left，因为right个括号还有剩余并且不能更多地放在left个括号之前
            generateParenthesisOneByOne(results, left, right - 1, oneResult + ")");
        }
    }
}
```

##### 31 Next Permutaion
将数组从后先前看，找到的第一个降序的数字，记下它的坐标p；然后第二次再从后向前查找，找到第一个比p坐标位置的数大的数，二者swap；然后将swap后的p后面的所有的数reverse，得到的数组即为next permutation。

corner case：第一遍找p坐标如果没找到（也就是说整个数组是降序），那说明该数组是最大的permutation，那就它的下一个排列就是最小的，直接reverse就行了。

##### 50 Pow

##### 56 Merge Intervals
先排序，然后根据第一个区间初始化start和end，然后遍历list，比较list中interval.start和刚才end的值，如果end >= interval.start，说明两个区间有重叠，这时将end更新为end和interval.end之间的较大值；如果end < interval.start，说明没有重叠区间，这时候将interval.start和interval.end直接实例化一个list加入到结果中。最后还要注意一下最后一个区间没有被遍历到，需要加入。

##### 62 Unique Paths
bottom up的办法，按照计算机的思维，先初始化最后一行和最后一列为1，从右下角开始考虑，然后递推公式为dp[i][j] = dp[i+1][j] + dp[i][j+1]，计算所有的路径总数，返回dp[0][0]。
```java
class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 0 || n == 0) {
            return 0;
        }
        //dp[i][j] = dp[i + 1][j] + dp[i][j + 1]
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {//
            dp[i][n - 1] = 1;
        }
        for (int j = 0; j < n; j++) {
            dp[m - 1][j] = 1;
        }
        for (int i = m - 2; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {
                dp[i][j] = dp[i + 1][j] + dp[i][j + 1];
            }
        }
        return dp[0][0];
    }
}
```
对于空间复杂度， 每次只需要用到之前一行（下边）当前列，以及之前一列（右边）当前行的信息，只需要用一个一维数组存之前一行的信息即可，然后一行一行往上递推。
```java
class Solution {
    public int uniquePaths(int m, int n) {
        if (m == 0 || n == 0) {
            return 0;
        }
        
        int[] dp = new int[n];
        
        dp[n - 1] = 1;//最右最下的位置初始化
        
        for (int i = m - 1; i >= 0; i--) {
            for (int j = n - 2; j >= 0; j--) {//列从n-2开始，因为已经初始化过
                dp[j] += dp[j + 1];//一行行往上递推
            }
        }
        return dp[0];//返回递推到第一行的最左边元素
    }
}
```
自顶向下的办法，DFS + 缓存，做备忘录
```java
class Solution {
    private int[][] memo;
    public int uniquePaths(int m, int n) {
        if (m <= 0 || n <= 0) {
            return 0;
        } 
        if (m == 1 || n == 1) {
            return 1;
        }
        memo = new int[m][n];
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }
        
        memo[0][0] = 1;//达到最底下就返回做初始化
        
        return topdown(m - 1, n - 1);
    }
    private int topdown(int x, int y) {
        if (x < 0 || y < 0) {
            return 0;
        }
        if (x == 0 && y == 0) {
            return memo[0][0];
        }
        
        if (memo[x][y] != -1) {//有记录，不用重新算 - 初始值为0
            return memo[x][y];
        } else {
            return memo[x][y] = topdown(x - 1, y) + topdown(x, y - 1);
        }
    }
}
```

##### 63 Unique Paths II
用自底向上，每次先判断一下格子是否是障碍物，是的话先设为0，然后同上，每个格子只跟它的右边和下面的两个格子相关，另外特殊处理最右边一列，最下面一行和最右下角的格子.
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null || obstacleGrid.length == 0 || obstacleGrid[0].length == 0) {
            return 1;//原地踏步算一条
        }
        int rows = obstacleGrid.length;
        int cols = obstacleGrid[0].length;

        int[][] dp = new int[rows][cols];

        for (int i = rows - 1; i >= 0; i--) {
            for (int j = cols - 1; j >= 0; j--) {
                if (obstacleGrid[i][j] == 1) {//有障碍物，注意这个条件要先检查
                    dp[i][j] = 0;//设为从当前点到终点的路径数为0
                } else {
                    if (i == rows - 1 && j == cols - 1) {//在右下角的终点处，自己到自己，一条路
                        dp[i][j] = 1; 
                    } else if (i == rows - 1) {//最后一列除了最右下角的格子
                        if (dp[i][j + 1] == 0) {//最后一列如果下面的路被堵住了，上面的格子均为0条路径
                            dp[i][j] = 0;
                        } else {
                            dp[i][j] = 1;
                        }
                    } else if(j == cols - 1) {//最后一行除了最右下角的格子
                        if (dp[i + 1][j] == 0) {//最后一行如果右面的路被堵住了，左面的格子均为0条路径
                            dp[i][j] = 0;
                        } else {
                            dp[i][j] = 1;
                        }
                    } else{
                        dp[i][j] = dp[i + 1][j] + dp[i][j + 1];//正常的递推式
                    }
                }
            }
        }
        return dp[0][0];
    }
}
```
JavaScript
```text
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    let rows = obstacleGrid.length, cols = obstacleGrid[0].length;
    let dp = new Array(rows).fill(0).map(_item => new Array(cols).fill(0)); 
    for (let i = rows - 1; i >= 0; --i) {
        for (let j = cols - 1; j >= 0; --j) {
            if (obstacleGrid[i][j] === 1) { 
                dp[i][j] = 0;
            } else if (i === rows - 1 && j === cols - 1) { // 终点
                dp[i][j] = 1;
            } else if (i === rows - 1) { 
                if (dp[i][j + 1] === 0) {
                    dp[i][j] = 0;
                } else {
                    dp[i][j] = 1;
                }
            } else if (j === cols - 1) {
                if (dp[i + 1][j] === 0) {
                    dp[i][j] = 0;
                } else {
                    dp[i][j] = 1;
                }
            } else {
                dp[i][j] = dp[i + 1][j] + dp[i][j + 1]; 
            }
        }
    }
    return dp[0][0];
};
```

##### 74 Search a 2D Matrix
把矩阵当作一个长的一维数组，start为0，end为最后一个元素，取到mid的值再换算成相应的index的时候，行数为mid对总行数相除，列数为mid对总列数取余。
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }

        int rows = matrix.length;
        int cols = matrix[0].length;

        int start = 0;
        int end = rows * cols - 1;

        while (start <= end) {//注意右等于符号
            int mid = start + (end - start) / 2;
            int midValue = matrix[mid / rows][mid % cols];
            if (target == midValue) {
                return true;
            } else if (target < midValue) {
                end = mid - 1;//注意-1
            } else {
                start = mid + 1;//注意+1
            }
        }
        return false;
    }
}
```
##### 98 Validate Binary Search Tree
1) 从root开始做一个中序遍历，记录前置结点，根据前置结点的值来检查遍历过程是否是”左根右“的升序，从而确定当前遍历到的结点是否合适；2）设定一个min，代表右子树里面的最小值，设定一个max，代表左子树里面的最大值，每次递归到当前结点为root时，判断当前结点是否在min和max之间。
中序遍历
```java
class Solution {
    TreeNode pre = null;
    public boolean isValidBST(TreeNode root) {
        return isValidBSTHelper(root);
    }
    private boolean isValidBSTHelper(TreeNode cur) {
        if (cur == null) {
            return true;
        }
        //检查左子树
        if (!isValidBSTHelper(cur.left)) {
            return false;
        }
        //检查当前结点
        if (pre != null && cur.val <= pre.val) {//Test cases中的[1,1]，[1,1,1]这样相等的不算BST，所以代码中加上等号，但根据BST定义[1,1]，[1,1,1]这样的其实应该算
            return false;
        }

        //更新前置结点
        pre = cur;

        //检查右子树
        return isValidBSTHelper(cur.right);
    }
}
```
设置一个min和max
```java
//为了过test cases还要考虑结点的值val越界Integer的问题，设作Long，感觉这样的test cases没什么意义，毕竟给TreeNode的定义val的类型为int
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }
    private boolean isValidBST(TreeNode cur, long min, long max) {
        if (cur == null) {
            return true;
        }
        if (cur.val <= min || cur.val >= max) {//Test cases中的[1,1]，[1,1,1]这样相等的不算BST，所以代码中加上等号，但根据BST定义[1,1]，[1,1,1]这样的其实应该算
            return false;
        }
        //左子树-的所有结点的最大值可为当前结点的值，所以max替换为cur.val；右子树-的所有结点的最小值最小可为当前结点的值，所以min替换成cur.val
        return isValidBST(cur.left, min, cur.val) && isValidBST(cur.right, cur.val, max);
    }
}
```

##### 125 Valid Palindrome
这道题使用Character.isLetterOrDigit()即可，注意如果对原始数据类型char转换大小写用Character.toLowerCase()，Character.toUpperCase()，与对象（比如string）直接调用的办法不同。
```java
class Solution {
    public boolean isPalindrome(String s) {
        if (s.isEmpty()) {
            return true;
        }
        char[] chs = s.toCharArray();
        int left = 0;
        int right = chs.length - 1;
        while (left <= right) {
            if (!Character.isLetterOrDigit(chs[left])) {
                left++;
            } else if (!Character.isLetterOrDigit(chs[right])) {
                right--;
            } else {
                if (Character.toLowerCase(chs[left]) != Character.toLowerCase(chs[right])) {
                    return false;
                }
                left++;
                right--;
            }
        }
        return true;
    }
}
```

##### 131 Parlindrome Partitioning
DFS的做法，检查从0到0的子串，剩余部分进入递归，并向右走一步，继续检查是否递归看能否加入到当前递归的结果中，如果最后走到了字符串最右，说明当次递归所有的字串都是合法的，加入到最终结果集。每个位置可能是回文也可能不是2^n，检查是否是回文n，所以时间复杂度为O(n * 2 ^ n)。
```java
class Solution {
    public List<List<String>> partition(String s) {
        if (s.isEmpty()) {
            return new ArrayList<List<String>>();
        }
        List<List<String>> results = new ArrayList<>();
        List<String> oneResult = new ArrayList<>();

        partitionDFS(s, 0, results, oneResult);

        return results;
    }
    private void partitionDFS(String s, int index, List<List<String>> results, List<String> oneResult) {
        if (index == s.length()) {//dfs到字符串的最后位置都是回文，加入到结果集
            results.add(new ArrayList<String>(oneResult));
        } else {
            for (int i = index; i < s.length(); i++) { //如果index还未到字符串最后，那它后面的每一个位置都需要检查是否从index到各个位置是否为回文，所以是for循环
                if (isPalindrome(s, index, i)) {//检查从当前位置开始算，后面所有字符串是否是回文
                    oneResult.add(s.substring(index, i + 1));
                    partitionDFS(s, i + 1, results, oneResult);//DFS的下一层是当前位置i的下一步，在未到s最后一个位置时所有字串都加入到oneResult
                    oneResult.remove(oneResult.size() - 1);//从某个index位置回溯到root的时候需要删除该位置为起点的所有子串
                }
            }
        }
    }
    private boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

##### 138 Copy List with Random Pointer
比较常用的办法是用一个hashmap做两次遍历，第一次遍历将hashmap的key设为当前的node，hashmap的value设为以当前node的val的值新创建的一个node（这时候该node还没有设置next和random）；第二次遍历的时候，通过hashmap的get方法将前一次遍历时创建的新node（hashmap的value）的next指针和random指针通过hashmap的key来赋值。时空复杂度都是O(n)。

还有不用额外空间的办法：待续。

##### 139 Word Break
自顶向下的动态规划题目，建立一个一维数组results，results[i]表示从头到i-1索引的子字符串可以在字典中找到单词，另外针对每个位置i，他之前的索引j也都检查过来是否可以组成，找到i位置就直接break到i+1，直到末尾，返回results[len]表示存的最后一个字符。
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        if (s.isEmpty()) {
            return true;
        }

        int len = s.length();
        boolean[] results = new boolean[len + 1];//results[i]表示从最初到i-1位置的子字符串是否可以又dict中组成，自顶向下
        results[0] = true;//0个字符可以由wordDict组成

        for (int i = 0; i < len; i++) {//每个位置可能性都是可能的单词组成,i表示的是多少个字符
            for (int j = 0; j <= i; j++) {//j位置到当前i位置是否可以组成单词
                String str = s.substring(j, i + 1);
                if (results[j] && wordDict.contains(str)) {//j到i组成单词，并且j以前的子字符串也可以组成单词
                    results[i + 1] = true;//自顶向下的记忆化存储
                    break;//当前位置可以组成一个单词，剩下j到i的字符不用一一查了，直接跳到i+1的位置
                }
            }
        }
        return results[len];
    }
}
```

##### 140 Word Break II

##### 146 LRU cache
为了保证O(1)，利用hashmap（取值） + double linked（存），put和get方法主要考虑已经存在或者不存在的两种情况
```java
class LRUCache {
    
    class Node {
        int key;
        int value;
        Node next;
        Node pre;
        public Node (int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    private HashMap<Integer, Node> map;
    private int capacity;
    private Node head;
    private Node tail;

    public LRUCache(int capacity) {
        map = new HashMap<>();
        this.capacity = capacity;
        head = null;
        tail = null;
    }
    
    public int get(int key) {
        Node node = map.get(key);
        if (node == null) {
            return -1;
        }
        if (node != tail) {
            if (node == head) {
                head = head.next;
            } else {
                node.pre.next = node.next;
                node.next.pre = node.pre;
            }
            tail.next = node;
            node.pre = tail;
            node.next = null;
            tail = node;
        }
        return node.value;
    }
    
    public void put(int key, int value) {
        Node node = map.get(key);
        if (node != null) {
            node.value = value;
            if (node != tail) {
                if (node == head) {
                    head = head.next;
                } else {//交换值
                    node.pre.next = node.next;
                    node.next.pre = node.pre;
                }
                tail.next = node;
                node.pre = tail;
                node.next = null;
                tail = node;
                
            }
        } else {
            Node newNode = new Node(key, value);
            if (capacity == 0) {
                Node temp = head;
                head = head.next;
                map.remove(temp.key);
                capacity++;
            }
            if (head == null && tail == null) {
                head = newNode;
            } else {
                tail.next = newNode;
                newNode.pre = tail;
                newNode.next = null;
            }
            tail = newNode;
            map.put(key, newNode);
            capacity--;
        }
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity)S;
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

##### 200 Number of Islands
DFS，遍历每一个二维数组里面的元素，当遇到‘1’时，利用DFS查找相同岛的元素，将所有的‘1’改成0。

##### 205 Isomorphic Strings
用两个256长度的数组（或者一个512长度的数组，比较前256位和后256位），每次对应的两个字符存同样的不为0的整数，再遇到的时候比较存的两个整数，不用就返回false，相同就一直比到字符串末尾。

##### 235 Lowest Common Ancestor of a Binary Search Tree
利用BST左<=根<=右的特性，递归到去当前结点，检查一下在哪个子树,O(N)。
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return root;
        }
        //当前结点等于p，q其中之一则直接返回当前结点
        if (root.val == p.val || root.val == q.val) {
            return root;
        }
        // if (root == null || root.val == p.val || root.val == q.val) {
        //    return root;
        //}
        if (root.val > Math.max(p.val, q.val)) {//当前结点的值比p和q都大，说明p和q都以在当前结点为root的左子树
            return lowestCommonAncestor(root.left, p, q);
        } else if (root.val < Math.min(p.val, q.val)) {//当前结点的值比p和q都小，说明p和q都以在当前结点为root的右子树
            return lowestCommonAncestor(root.right, p, q);
        } else {//p和q分别在以当前结点为root的左右子树里，那就直接返回当前结点
            return root;
        }
    }
}
```

##### 236 Lowest Common Ancestor of a Binary Tree
不是BST，直接不判断当前root的值和p，q值得大小问题，通过递归直接判断左右子树是否包含p或者q，如果p，q都在左子树，返回左子树，如果p，q都在右子树，返回右子树，一左一右则返回当前root,O(N)。。
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null || root.val == p.val || root.val == q.val) {
            return root;
        }

        //把左右子树是否包含p，q得结果存到left和right中
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        } else if (left == null) {
            return right;
        } else {
            return left;
        }
        //return left == null ? right : (right == null ? left : root);
    }
}
```

##### 239 Sliding Window Maximum
1）用一个k大小的最大堆，窗口移动时自动维护，每次取出堆顶的元素，因为维护的成本，这个时间复杂度为nlogk；2）题目要求线性复杂度，那做法就是利用deque，每次移动的窗口都将比新元素小的原来的元素踢出去，其实这也不是严格的线性复杂度，平均是线性，最坏n*k (每次窗口中的老元素都比新进的元素要大，除了最左边的一个都踢不走)。
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {

        if (nums == null || k <= 0) {
            return new int[0];
        }
        int len = nums.length;

        //如果原本元素个数少于k，直接查一遍
        if (len <= k) {
            int max = Integer.MIN_VALUE;
            for (int num : nums) {
                //max = num > max ? num : max;
                if (num > max) {
                    max = num;
                }
            }
            return new int[]{max};
        }

        int[] result = new int[len - k + 1];

        Deque<Integer> window
                = new ArrayDeque<Integer>(k);//队列中存的是元素的下标

        //刚开始窗口为空的时候，将第一个元素的下标default放到队列中去
        window.offer(0);

        //依次将每一个元素循环，放入到窗口中去
        for (int i = 0; i < len; i++) {

            //判断窗口中头部的元素的下标，从而知道该元素是否应该继续在本轮存在于窗口，或者根据窗口滑动应该被移除
            if (window.peek() < i - k + 1) {
                window.poll();
            }

            //新的元素nums[i]准备放入队列中，这时候要先和原本队列中的元素的下标
            Iterator<Integer> it = window.iterator();
            while(it.hasNext()) {
                //原先窗口中的元素只要比新来的元素小，就通通移除，反正没有这些较小元素的机会
                if (nums[it.next()] < nums[i]) {
                    it.remove();
                }
            }

            //每次循环将新元素的下标添加到窗口中
            if (i != 0) {
                window.offer(i);
            }

            //i >= k - 1表示至少遍历了k个元素了（可以开始查找最大数了），这时候把最头部（左边）的老大加入到结果中
            if (i >= k - 1) {
                result[i - k + 1] = nums[window.peek()];
            }
        }
        return result;
    }
}
```

##### 242 Valid Anagram
排序后比较是否相同比较费时；用一个26大小的数组来统计字符出现的次数，counts[ch - 'a']，第一个循环++，第二个循环--，第三次循环counts看是否有不等于0的字符，小优化是省掉第三个循环，在第二个循环的时候直接判断是否有字符出现的次数小于0，有的话直接返回false。用HashMap来统计也可以，同样的做法，如果follow up是unicode需要用到codePoints()方法来计算是占几个位置。

##### 289 Game of Life
这道题的难点是in place，利用状态机，使用两次遍历，第一次遍历将每个下一个generation为活细胞的转换成状态1或者状态3（死细胞总是0），这样不会影响后面细胞的计算，第二次遍历将每个细胞的状态对2进行取余，得到的结果就是下一个generation的细胞状态。单独写一个method来计算第一遍循环中每个细胞八个邻居的死活状态。

##### 338 Counting Bits
朴素做法就是从0开始循环到num，然后每次计算下循环到的数有几个二进制的1，存入到数组，这个计算过程可以通过对2取模最后看是否有余数或者n & n - 1每次挪掉最右边一个1的做法；改进要求是O(n)的话，就可以先创建一个数组，初始值为0，利用DP的自上而下的思想，利用i & i - 1的消除最右边一个1的做法作为index根据前一个数组元素找到下一个数组元素的做法。
```java
class Solution {
    public int[] countBits(int num) {
        int[] results = new int[num + 1];//从0到num
        Arrays.fill(results, 0);
        for (int i = 1; i <= num; i++) {
            results[i] = results[i & i - 1] + 1;//dp递推式，下一个元素是上一个元素+1（下一个元素和上一个元素的关系是相差一个二进制的1）
        }
        return results;
    }
}
```

##### 409 Longest Palindrome
使用一个256长度的数组来统计字符出现的次数，因为每两个字符可以组成一个回文，然后每个字符出现的次数（无论奇偶，地板除法）除以2再乘以2，就是偶数的最长回文，这时候再检查一下这个最长回文的长度是否等于原来的字符串，如果不等于（其实是小于，因为地板除法的缘故），说明有字符出现的次数被地板除法除掉了，可以拿一个字符回来放在回文串的正中。

##### 460 LFU Cache

##### 647 Palindromic Substrings
正常判断一个中心和两个中心的情况(i, i和i, i + 1)，注意下检查每个字符的循环中需要检查到最后一个字符，i+1虽然越界但checkPalindrome的方法中while循环会跳过越界的。

##### 696 Count Binary Substrings
创建两个变量分别保存前面一个数连续的长度和当前数连续的长度，for循环从index = 1开始，遇到相同的数curLength自增，遇到不同的数prevLength更新成curLength的数，curLength变为1.

##### 703

##### 887 Super Egg Drop
使用 dp[k][step] 来表示在给定 k 个鸡蛋的前提下移动 step 步能确定的最大层数：

* dp[0][1] = 0：0个鸡蛋经过一步最大只能确定0层，这是初始条件
* dp[k][1] = 1：k个鸡蛋只移动一次只能确定1层，即在1层只需要放一次鸡蛋便知道当前的 F，碎了 F为0；没碎 F=1。
* dp[1][i] = i：即一个鸡蛋必须从第一层开始一个个试，为了确定 F 得试 i 次。
* 当前楼层情况dp[k][step]=dp[k-1][step-1]+dp[k][step-1]+1，即当前情况=丢下去碎了，消耗一步能确定的层数+丢下去没碎，消耗一步能确定的层数+当前这一层
* N 层楼梯最多只需要进行 N 次便一定可以确定 F，即 F 最大只能是最高层 N
```java
class Solution {
    public int superEggDrop(int K, int N) {
        int[][] dp = new int[K + 1][N + 1];
        for (int steps = 1; steps <= N; steps++) { //每次消耗一步
            dp[0][steps] = 0; // 0 个鸡蛋
            for (int eggs = 1; eggs <= K; eggs++) {
                //在某一层，当前情况=（丢下去碎了eggs-1，消耗一步能确定的层数steps-1 + 丢下去没碎eggs，消耗一步能确定的层数，steps - 1）+ 当前这一层1
                dp[eggs][steps] = dp[eggs][steps - 1] + dp[eggs - 1][steps - 1] + 1;
                if (dp[eggs][steps] >= N) {//N 层楼梯最多只需要进行 N 次便一定可以确定 F，即 F 最大只能是最高层 N
                    return steps;
                }
            }
        }
        return N;
    }
}
```

##### 904 Fruit into Brasket 
用hashmap或者两个变量替换

##### 929 Unique Email Address
以email的@分成左右两部分，分别考虑。

##### 1005 Maximize Sum Of Array After K Negations
先排序，然后判断从左到右判断是否为负数，负数就转为正数，如果所有负数都转换完了K值还不为0，那就判读是否有0，有的话可以直接终止查找，没有0的话就判断最后转换的那个负数（已转换为正数）和第一个正数看哪个小，将值小的那个值判断下剩余K值的奇偶看是正还是负，相应取正负，最后将数组里面的所有值相加返回最后结果。

##### 1006 Clumsy Factorial
先把乘法和除法做好，然后加法，作为一个整体；然后判断是否是第一次，如果是赋值给临时变量，不是第一次就将下一轮的乘法和除法作为一个整体，被上一轮的临时变量值（乘法除法加法一起）减掉，注意corner cases比如1，5，9，10这样的值。

##### 1011 Capacity to Ship Packages Within D Days

```java
class Solution {
    public int shipWithinDays(int[] weights, int D) {
        int left = 0;
        int right = 0;
        for (int weight : weights) {
            left = Math.max(left, weight);
            right += weight;
        }
        while (left < right) {
            int mid = left + (right - left) / 2;
            int need = 1;
            int cur = 0;
            for (int weight : weights) {
                if (cur + weight  > mid) {
                    need += 1;
                    cur = 0;
                }
                cur += weight;
            }
            if (need > D) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
}
```
