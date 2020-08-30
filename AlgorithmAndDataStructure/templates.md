#### 二分
迭代
```java
int binarySearch(int[] nums, int target, int low, int high) {
    // 在 while 循环里，判断搜索的区间范围是否有效
    while (low <= high) {
        // 计算正中间的数的下标
        int middle = low + (high - low) / 2;
    
    // 判断正中间的那个数是不是要找的目标数 target。如果是，就返回下标 middle
    if (nums[middle] == target) {
        return middle;
    }
    
    // 如果发现目标数在左边，调整搜索区间的终点为 middle - 1；否则，调整搜索区间的起点为 middle + 1
    if (target < nums[middle]) {
        high = middle - 1;
      } else {
        low = middle + 1;
      }
    }

    // 如果超出了搜索区间，表明无法找到目标数，返回 -1  
    return -1;
}
```
递归
```java
// 二分搜索函数的定义里，除了要指定数组 nums 和目标查找数 target 之外，还要指定查找区间的起点和终点位置，分别用 low 和 high 去表示。
int binarySearch(int[] nums, int target, int low, int high) {
        // 为了避免无限循环，先判断，如果起点位置大于终点位置，表明这是一个非法的区间，已经尝试了所有的搜索区间还是没能找到结果，返回 -1。 

if (low > high) { // 等于还可以查一下
        return -1;
    }
    // 取正中间那个数的下标 middle。
    int middle = low + (high - low) / 2;
    
    // 判断一下正中间的那个数是不是要找的目标数 target，是，就返回下标 middle。    
    if (nums[middle] == target) {
        return middle;
    }
    
    // 如果发现目标数在左边，就递归地从左半边进行二分搜索。
    if (target < nums[middle]) {
        return binarySearch(nums, target, low, middle - 1);
      } else {
        return binarySearch(nums, target, middle + 1, high);
    }//否则从右半边递归地进行二分搜索。
}
```

#### 递归

```java
function fn(n) {
    // 第一步：判断输入或者状态是否非法？
    if (input/state is invalid) {
        return;
    }

    // 第二步：判读递归是否应当结束?
    if (match condition) {
        return some value;
    }

    // 第三步：缩小问题规模
    result1 = fn(n1)
    result2 = fn(n2)
    ...

    // 第四步: 整合结果
    return combine(result1, result2)
}
```

#### 回溯Backtracking
```java
function fn(n) {

    // 第一步：判断输入或者状态是否非法？
    if (input/state is invalid) {
        return;
  }

    // 第二步：判读递归是否应当结束?
    if (match condition) {
        return some value;
  }

    // 遍历所有可能出现的情况
    for (all possible cases) {
  
        // 第三步: 尝试下一步的可能性
        solution.push(case)
        // 递归
        result = fn(m)

        // 第四步：回溯到上一步
        solution.pop(case)
    
    }
    
}
```

#### Quick Sort
```java
void sort(int[] A, int lo, int hi) {
  // 判断是否只剩下最后一个元素
  if (lo >= hi) return;
  
  // 从中间将数组分成两个部分
  int mid = lo + (hi - lo) / 2;
  
  // 分别递归地将左右两半排好序
  sort(A, lo, mid);
  sort(A, mid + 1, hi);

  // 将排好序的左右两半合并  
  merge(A, lo, mid, hi);
}

void merge(int[] nums, int lo, int mid, int hi) {
    // 复制一份原来的数组
    int[] copy = nums.clone();
  
    // 定义一个 k 指针表示从什么位置开始修改原来的数组，i 指针表示左半边的起始位置，j 表示右半边的起始位置
    int k = lo, i = lo, j = mid + 1;
  
    while (k <= hi) {
        if (i > mid) {
            nums[k++] = copy[j++];
        } else if (j > hi) {
          nums[k++] = copy[i++];
        } else if (copy[j] < copy[i]) {
          nums[k++] = copy[j++];
        } else {
          nums[k++] = copy[i++];
        }
    }
}
```

#### Quick Sort
```java
void sort(int[] nums, int lo, int hi) {
    if (lo >= hi) return; // 判断是否只剩下一个元素，是，则直接返回
    
    // 利用 partition 函数找到一个随机的基准点
    int p = partition(nums, lo, hi);
    
    // 递归地对基准点左半边和右半边的数进行排序
    sort(nums, lo, p - 1);
    sort(nums, p + 1, hi);
}

int partition(int[] nums, int lo, int hi) {
    // 随机选择一个数作为基准值，nums[hi] 就是基准值
    swap(nums, randRange(lo, hi), hi);

    int i, j;

    // 从左到右用每个数和基准值比较，若比基准值小，则放到指针 i 所指向的位置。循环完毕后，i 指针之前的数都比基准值小
    for (i = lo, j = lo; j < hi; j++) {
        if (nums[j] <= nums[hi]) {
            swap(nums, i++, j);
        }
    }

    // 末尾的基准值放置到指针 i 的位置，i 指针之后的数都比基准值大
    swap(nums, i, j);

    // 返回指针 i，作为基准点的位置
    return i;
}
```

#### Top Sort
```java
void sort() {
    Queue<Integer> q = new LinkedList(); // 定义一个队列 q

    // 将所有入度为 0 的顶点加入到队列 q
    for (int v = 0; v < V; v++) {
        if (indegree[v] == 0) q.add(v);
    }

    // 循环，直到队列为空
    while (!q.isEmpty()) {
        int v = q.poll();
        // 每次循环中，从队列中取出顶点，即为按照入度数目排序中最小的那个顶点
        print(v);

        // 将跟这个顶点相连的其他顶点的入度减 1，如果发现那个顶点的入度变成了 0，将其加入到队列的末尾
        for (int u = 0; u < adj[v].length; u++) {
            if (--indegree[u] == 0) {
                q.add(u);
            }
        }
    }
}
```

#### DFS
```java
boolean dfs(int maze[][], int x, int y) {
    // 第一步：判断是否找到了B
    if (x == B[0] && y == B[1]) {
        return true;
    } 

    // 第二步：标记当前的点已经被访问过
    maze[x][y] = -1;

    // 第三步：在四个方向上尝试
    for (int d = 0; d < 4; d++) {
        int i = x + dx[d], j = y + dy[d];

        // 第四步：如果有一条路径被找到了，返回true
        if (isSafe(maze, i, j) && dfs(maze, i, j)) {
            return true;
        }
    }

    // 付出了所有的努力还是没能找到B，返回false
    return false;
  
}
```

DFS的非递归实现
```java
boolean dfs(int maze[][], int x, int y) {
    // 创建一个Stack
    Stack<Integer[]> stack = new Stack<>();

    // 将起始点压入栈，标记它访问过
    stack.push(new Integer[] {x, y});
    maze[x][y] = -1;
    
    while (!stack.isEmpty()) {
        // 取出当前点
        Integer[] pos = stack.pop();
        x = pos[0]; y = pos[1];
      
        // 判断是否找到了目的地
        if (x == B[0] && y == B[1]) {
          return true;
        }
    
        // 在四个方向上尝试  
        for (int d = 0; d < 4; d++) {
            int i = x + dx[d], j = y + dy[d];
            
        if (isSafe(maze, i, j)) {
            stack.push(new Integer[] {i, j});
            maze[i][j] = -1;
            }
        }
    }
    return false;
}
```

#### BFS
```java
void bfs(int[][] maze, int x, int y) {
    // 创建一个队列queue，将起始点A加入队列中
    Queue<Integer[]> queue = new LinkedList<>();
    queue.add(new Integer[] {x, y});
  
    // 只要队列不为空就一直循环下去  
    while (!queue.isEmpty()) {
        // 从队列的头取出当前点
        Integer[] pos = queue.poll();
        x = pos[0]; y = pos[1];
      
        // 从四个方向进行BFS
        for (int d = 0; d < 4; d++) {
            int i = x + dx[d], j = y + dy[d];
        
            if (isSafe(maze, i, j)) {
                // 记录步数（标记访问过）
                maze[i][j] = maze[x][y] + 1;
                // 然后添加到队列中  
                queue.add(new Integer[] {i, j});
                // 如果发现了目的地就返回  
                if (i == B[0] && j == B[1]) return;
            }
        }
    }
}
```

#### Union Find
```java
class UF {
    // 连通分量个数
    private int count;
    // 存储一棵树
    private int[] parent;
    // 记录树的“重量”
    private int[] size;

    public UF(int n) {
        this.count = n;
        parent = new int[n];
        size = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    public void union(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        if (rootP == rootQ)
            return;

        // 小树接到大树下面，较平衡
        if (size[rootP] > size[rootQ]) {
            parent[rootQ] = rootP;
            size[rootP] += size[rootQ];
        } else {
            parent[rootP] = rootQ;
            size[rootQ] += size[rootP];
        }
        count--;
    }

    public boolean connected(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        return rootP == rootQ;
    }

    private int find(int x) {
        while (parent[x] != x) {
            // 进行路径压缩
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }

    public int count() {
        return count;
    }
}
```

#### Trie
以LC 208为例
```java
class Trie {
    
    private boolean is_string;
    private Trie[] next;

    /** Initialize your data structure here. */
    public Trie() {
        is_string = false;
        next = new Trie[26];
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        Trie root = this;
        char[] w = word.toCharArray();
        for (char x : w) {
            if (root.next[x - 'a'] == null) { // 当前节点的下一个节点不存在，说明是新来的，新建一个
                root.next[x - 'a'] = new Trie();
            }
            // 移动索引到当前节点
            root = root.next[x - 'a'];
        }
        root.is_string = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        Trie root = this;
        char[] w = word.toCharArray();
        for (char x : w) { // 挨个节点查找
            if (root.next[x - 'a'] == null) { // 没找到
                return false;
            }
            root = root.next[x - 'a']; // 移动索引并准备检查下一个节点
        }
        return root.is_string;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        Trie root = this;
        char[] p = prefix.toCharArray();
        for (char x : p) {
            if (root.next[x - 'a'] == null) { // 没找到
                return false;
            }
            root = root.next[x - 'a'];
        }
        return true;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
