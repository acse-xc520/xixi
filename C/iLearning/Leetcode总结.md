# Leetcode题型总结

[TOC]

  ## 0 概览

  基础篇

  - 数组，队列，栈

  - 链表
  - 树与递归
  - 哈希表
  - 双指针

  思想篇

  - 二分
  - 滑动窗口
  - 搜索（BFS，DFS，回溯）
  - 动态规划

  提高篇

  - 贪心
  - 分治
  - 位运算
  - KMP & RK
  - 并查集
  - 前缀树
  - 线段树
  - 堆

  ## 1 字符串

  ### 1.1 字符串类题目

  符串可以涉及非常多的考点：如递归、栈、hash、dfs、bfs、动态规划等，需要重点关注。

  - [ ] Leetcode 5.最长回文子串
  - [ ] Leetcode 7. 整数反转
  - [ ] Leetcode 8. 字符串转换整数 (atoi)
  - [ ] Leetcode 93.复原 IP 地址（dfs）
  - [ ] Leetcode 43.字符串相乘
  - [ ] Leetcode 227.基本计算器

### 1.2 题目解析

  **例：Leetcode 7. 整数反转**

  反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

  - 判断整数是否越界：`INT_MIN / 10 || ret > INT_MAX / 10`

  ```c
  int reverse(int x){
      int ret = 0;
      while (x != 0) {
          if (ret < INT_MIN / 10 || ret > INT_MAX / 10) {
              return 0;
          }
          //整数反转，需重点记住
          int tmp = x % 10; // 个位上的数
          ret = ret * 10 + tmp;
          x/=10;
      }
      return ret;
  
  }
  ```

  **例：Leetcode 8. 字符串转换整数 (atoi)：**

  - 如果开头有空格，指针后移；
  - 如果有“+”，指针后移，如果有“-”号用flag = -1标记；
    此题边界条件判断有所不同，因为只能使用 32 位 int，因此将 ret 乘 10 后再与 INT_MAX 比较可能会溢出，因此使用 ret 与 INT_MAX/10 比较：
  - 若 ret <  INT_MAX / 10 ，则 ret * 10 + dig 也一定小于 INT_MAX，不会溢出
  - 若 ret == INT_MAX / 10 ，只有 dig 比 8 小时不会溢出
  - INT_MAX 个位是 7，INT_MIN 个位是 8
  - INT_MIN 在 int 中会溢出，当 dig == 8 时直接当作溢出处理

  

  ## 2 数组、队列、堆、栈、哈希表类

基础知识：堆（Heap or Priority Queue）、栈（Stack）、队列（Queue）、哈希表类（Hashmap、Hashset）各个数据结构的基本原理，增删查改复杂度。

### 2.1 数组类题目

  - [ ] [Leetcode 283. 移动零](https://leetcode.cn/problems/move-zeroes/)
  - [x] [Leetcode 36. 有效的数独](https://leetcode.cn/problems/valid-sudoku/solution/)
  - [ ] [Leetcode 48. 旋转图像](https://leetcode.cn/problems/rotate-image/) 
  - [x] [Leetcode 387. 字符串中的第一个唯一字符](https://leetcode.cn/problems/first-unique-character-in-a-string/) 【数组 + 哈希】

  **例：Leetcode 48. 旋转图像**

  旋转关系：`matrixNew[col][n−row−1] = matrix[row][col]`

  由于不能使用额外空间，因此考虑每一次原地交换四个位置

  ```c
  // matrix[i][j]                          matrix[j][matrixSize-1-i]
  // matrix[matrixSize-1-j][i]             matrix[matrixSize-1-i][matrixSize-1-j]
  
  void rotate(int** matrix, int matrixSize, int* matrixColSize){
      for (int row = 0; row < matrixSize / 2; row++) {
          for (int col = 0; col < (matrixSize + 1) / 2; col++) {
              int tmp = matrix[row][col];
              matrix[row][col] = matrix[matrixSize - col - 1][row];
              matrix[matrixSize - col - 1][row] = matrix[matrixSize - row - 1][matrixSize - col - 1];
              matrix[matrixSize - row - 1][matrixSize - col - 1] = matrix[col][matrixSize - row - 1];
              matrix[col][matrixSize - row - 1] = tmp;
          }
      }
  }
  ```

  ### 2.2 队列类题目

  - Leetcode 225. Implement Stack using Queues
  - Leetcode 346. Moving Average from Data Stream
  - Leetcode 281. Zigzag Iterator
  - Leetcode 1429. First Unique Number
  - Leetcode 54. Spiral Matrix
  - Leetcode 362. Design Hit Counter

  - Leetcode 950. 按递增顺序显示卡牌 https://leetcode.cn/problems/reveal-cards-in-increasing-order/

  ### 2.3 Stack题目

  - Leetcode 155. Min Stack (follow up Leetcode 716 Max Stack)
  - Leetcode 232. Implement Queue using Stacks
  - Leetcode 150. Evaluate Reverse Polish Notation
  - Leetcode 224. Basic Calculator II (I, II, III, IV)
  - Leetcode 20. Valid Parentheses
  - Leetcode 1472. Design Browser History
  - Leetcode 1209. Remove All Adjacent Duplicates in String II
  - Leetcode 1249. Minimum Remove to Make Valid Parentheses
  - Leetcode 735. Asteroid Collision
  - 

  ### 2.4 Heap／Priority Queue题目

  - Leetcode 973. K Closest Points
  - Leetcode 347. Top k Largest Elements
  - Leetcode 23. Merge K Sorted Lists
  - Leetcode 264. Ugly Number II
  - Leetcode 1086. High Five
  - Leetcode 88. Merge Sorted Arrays
  - Leetcode 692. Top K Frequent Words
  - Leetcode 378. Kth Smallest Element in a Sorted Matrix
  - Leetcode 295. Find Median from Data Stream （标准解法是双heap，但是SortedDict会非常容易）
  - Leetcode 767. Reorganize String
  - Leetcode 1438. Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit (这个题用单调双端队列、TreeMap、双heap都可以)
  - Leetcode 895. Maximum Frequency Stack

  ### 2.5 Hashmap/ Hashset题目

  - [x] Leetcode 1. Two Sum
  - [ ] Leetcode 146. LRU Cache (Python中可以使用OrderedDict来代替)
  - [ ] Leetcode 128. Longest Consecutive Sequence
  - [ ] Leetcode 73. Set Matrix Zeroes
  - [ ] Leetcode 380. Insert Delete GetRandom O(1)
  - [ ] Leetcode 49. Group Anagrams
  - [ ] Leetcode 350. Intersection of Two Arrays II
  - [ ] Leetcode 299. Bulls and Cows
  - [ ] Leetcode 348 Design Tic-Tac-Toe
  - [ ] [Leetcode 451. 根据字符出现频率排序](https://leetcode.cn/problems/sort-characters-by-frequency/) 
  - [x] [Leetcode 1603. 设计停车系统](https://leetcode.cn/problems/design-parking-system/) 【设计 + 哈希】

  参考资料

  [HASH表攻略]( https://leetcode.cn/circle/article/u4Jvw7/)

  [leecode刷题算法总结----哈希表（C语言）](https://blog.csdn.net/weixin_43701705/article/details/122754362)

  ### 2.6 题目解析

  [Leetcode 451. 根据字符出现频率排序](https://leetcode.cn/problems/sort-characters-by-frequency/) 

  ```c
  #define MAX_NUM 128
  
  int g_hashTable[MAX_NUM];
  
  // 如果个数不等，按个数降序排序；否则，按字符升序排序
  int cmp(const void *a, const void *b)
  {
      char a1 = *(char *)a;
      char b1 = *(char *)b;
      if (g_hashTable[a1] != g_hashTable[b1]) {
          return g_hashTable[b1] - g_hashTable[a1];
      }
      return a1 - b1;
  }
  
  char * frequencySort(char * s)
  {
      if (s == NULL) {
          return NULL;
      }
      int len = strlen(s);
      memset(g_hashTable, 0, sizeof(int) * MAX_NUM);
  
      for (int i = 0; i < len; i++) {
          g_hashTable[s[i]]++;
      }
      qsort(s, len, sizeof(char), cmp);
  
      return s;
  }
  ```

  ## 3 深度优先搜索（DFS）

  http://3ms.huawei.com/hi/group/2915663/wiki_6653068.html

  ### 3.1 DFS的基本结构

  DFS就是深度优先遍历，DFS通常用于图的遍历，从一个图来讲，DFS的步骤分为如下几步

  （1）访问顶点v；

  （2）依次从v的未被访问的邻接点u出发，对图进行遍历，直至图中和v有路径相通的顶点都被访问；

  （3）如果图中还有未遍历的节点，则这些节点都与上面遍历的节点不连通。继续遍历即可。

  DFS实质就是一种枚举，不过借助递归实现；

  ```c
  void dfs(int step)
  {
      // 判断边界；
      for（int i = 1; i <= n; ++i){ // 尝试每一种可能；
          dfs(step + 1);            // 继续下一步
      }
      return；
  }
  ```

  #### DFS伪代码

  ```c
  // 模板
  void dfs(int x,int y)
  {
  		if(达到出口||无法继续)
  		{
  			相应操作;
  			return；
  		}
  
  		if（对应x方向的下一步可以继续）
  		{
  			   添加标记;//给该位置记上标记，如果后续递归调用碰到了这个点，则该方向不能继续下一步
  			   dfs(x+1,y);//调用递归
  			   取消标记;//上一步对应的递归操作全部结束，则要取消标记对后续操作的影响
  		}
  
  		else if（对应y方向的下一步可以继续）{
  			   添加标记;
  			   dfs(x,y+1);
  			   取消标记;
  		}
  }
  ```

  #### 写题技巧

  3.1）何时使用DFS

  显然DFS是递归的一种，因此首先判断该题是否可以递归，可以使用递归简单来讲就是有没有一直重复一个操作，所以从这点来看，在二叉树类的题中，有重复操作时，优先考虑DFS。
  图，DFS就是图论的算法，图的表示有两种方法，一种是邻接表，一种是邻接矩阵，在我们刷题的时候，其实leetcode中这两种是都有的，但是邻接表并不是按链表形式组织的，主要以邻接矩阵为主，但是总体思想是一样的。
  连接，顺序，有的时候题目不会直接给你图，这个时候有迷惑性，例如leetcode207 课程表，332安排行程，这类课程表，这种题其实也是DFS的一种，1门课连接着1门课，一个城市连接一个城市，我们需要按顺序进行遍历的时候。
  当然还有一些，我这里没法都总结出来，总的来说就是上面的几点，二叉树，图，连接，顺序，遍历。
  3.2）标准套路

  说了这么多了，最后我总结两个个DFS的套路模板，理解好了这个可以根据情况修改使用。

  **3.2.1）** 第一个是基于地图的

  ```c
  	void dfs(int **graph, int x, int y, int *res, int **isUsed)
  	{
  	    if(这里先写边界判断，例如x<0, y <0, isUsed[x][y],还有根据你的情况写退出条件){
  	        res = ****;//一般这里会修改结果，根据情况分析，也可能在底下修改
  	    }
  	    isUsed[x][y] = true; //进来第一步先写record
  	    //这中间写一些题目要求的处理，可能是各种。
  	    ///********
  	    //******
  	    // res = ???
  	    dfs(graph, x + 1, y, balabala, &balabala, isUsed);//然后从该点（x,y）作为起点开                                            				//始，向后继续dfs
  	    dfs(graph, x - 1, y, balabala, &balabala, isUsed);
  	    dfs(graph, x, y + 1, balabala, &balabala, isUsed);
  	    dfs(graph, x, y - 1, balabala, &balabala, isUsed);
  	    //上下左右dfs。
  	 
  	int main()
  	{
  		int **graph; //一个地图；
  
  	    int balabala = 0;  //这是你dfs在里面要改的东西，我们dfs既然进去肯定是要做什么的，根据你//的情况，在dfs里面修改，也有可能在dfs跑完之后修改。
  
  	    //我们DFS遍历的时候，为了防止走回头路，需要有一个记录，记录之前是否来过，在某些情况下可以在	//原数组上修改，为了通用模板，还是申请一个。
  	    bool **isUsed = malloc(sizeof(bool*) * M);
  	    for(int i = 0; i < M; ++i){
  	        usUsed[i] = nalloc(sizeof(bool) * N);
  	        memset(&usUsed[i], 0, sizeof(bool) * N); //考试别忘了安全函数
  	    }
  	    //这是单起始点的写法，假设起始点是 (x,y)
  	    dfs(graph, x, y, &balabala, isUsed);
  	    
  	    //这是整个图都要遍历的写法，二选一，根据题意。
  	    
  	    for(int i = 0; i < M; ++i){
  	        for(int j = 0; j < N; ++j){
  	            dfs(graph, i, j, &balabala, isUsed);
  	        }
  	    }
  	    
  	}
  ```

  这个可以用于leetcode 200 岛屿数量，写写看。

  **3.2.2）** 基于图连接的，基于连接的和基于图的不一样，基于图的只能从自己向周围扩撒，它的坐标总是相邻的，居于连接的是从一个连接到另一个，我们使用邻接矩阵来表示。

  ```c
  	void dfs(int **graph, int x, int *res, int **isUsed)
  	{
  	    if(这里先写边界判断，例如x<0, y <0, isUsed[x][y],还有根据你的情况写退出条件){
  	        res = ****;//一般这里会修改结果，根据情况分析、、也可能在底下修改
  	    }
  	    isUsed[x][y] = true; //进来第一步先写record
  	    //这中间写一些题目要求的处理，可能是各种。
  	    ///********
  	    //******
  	    // res = ???
  		//for(遍历i点所有连接的点，进行dfs)
  	    for(int i = 0; i < M; ++i){
  	        if(garph[x][i] == 1) // x与i点连接，继续dfs
  	        	dfs(graph, i,  &balabala, isUsed);
  	    }
  	 
  	int main()
  	{
  		int **graph; //邻接矩阵，M行，M列，1代表有连接，0代表无连接；
  	    
  	    int balabala = 0;  //这是你dfs在里面要改的东西，我们dfs既然进去肯定是要做什么的，根据你						//的情况，在dfs里面修改，也有可能在dfs跑完之后修改。
  	    
  	    //与上面类似，此时只需要一维数组保存即可
  	    bool *isUsed = malloc(sizeof(bool) * M);
  	    memset(&usUsed[i], 0, sizeof(bool) * N); //考试别忘了安全函数
  	 
  	    //这是单起始点的写法，假设起始点是 (x)
  	    dfs(graph, x, &balabala, isUsed);
  	    
  	    //这是整个图都要遍历的写法，二选一，根据题意。
  	    
  	    for(int i = 0; i < M; ++i){
  	           dfs(graph, i,  &balabala, isUsed);
  	        }
  	    }
  	    
  	}
  ```

  ### 3.2 基于树的 DFS

  - 94.二叉树的中序遍历 https://leetcode.cn/problems/binary-tree-inorder-traversal/
  - 513.找树左下角的值 https://leetcode.cn/problems/find-bottom-left-tree-value/
  - Leetcode 543 Diameter of Binary Tree (分治)
  - Leetcode 124 Binary Tree Maximum Path Sum (分治)
  - Leetcode 226 Invert Binary Tree (分治)
  - Leetcode 101 Symmetric Tree (回溯 or 分治)
  - Leetcode 951 Flip Equivalent Binary Trees (分治)
  - Leetcode 236 Lowest Common Ancestor of a Binary Tree (相似题：235、1650) (回溯 or 分治)
  - Leetcode 105 Construct Binary Tree from Preorder and Inorder Traversal (分治)
  - Leetcode 104 Maximum Depth of Binary Tree (回溯 or 分治)
  - Leetcode 987 Vertical Order Traversal of a Binary Tree
  - Leetcode 1485 Clone Binary Tree With Random Pointer
  - Leetcode 572 Subtree of Another Tree (分治)
  - Leetcode 863 All Nodes Distance K in Binary Tree
  - Leetcode 1110 Delete Nodes And Return Forest (分治)

  例1：94.二叉树的中序遍历

  ```c
  #define MAX_SIZE 101
  
  void inorder(struct TreeNode* root, int* resSize, int *res)
  {
      if(!root) {
          return;
      }
      inorder(root->left, resSize, res);
      res[(*resSize)++] = root->val;
      inorder(root->right, resSize, res);
  }
  
  int* inorderTraversal(struct TreeNode* root, int* returnSize)
  {
      int *res = (int *)malloc(sizeof(int) * MAX_SIZE);
      *returnSize = 0;
      inorder(root, returnSize, res);
      return res;
  }
  ```

  ### 3.3 基于网格的 DFS

  #### 岛屿类问题

  - 200.岛屿数量  (Easy)  https://leetcode.cn/problems/number-of-islands/      （完成）
  - 463.岛屿的周长 （Easy）https://leetcode.cn/problems/island-perimeter/       （完成）
  - 695.岛屿的最大面积 （Medium）https://leetcode.cn/problems/max-area-of-island/ (完成)
  - 827.最大人工岛 （Hard）

  #### 结合并查集

  - 547.省份数量 https://leetcode.cn/problems/number-of-provinces/

  ```c
  void dfs(int **isConnected, int *visited, int cityNum, int cityIndex)
  {
      for (int i = 0; i < cityNum; i++) {
          // 查找与该城市相连的城市
          if (isConnected[cityIndex][i] == 1 && visited[i] == 0) {
              visited[i] = 1;
              dfs(isConnected, visited, cityNum, i);
          }
      }
  }
  
  int findCircleNum(int** isConnected, int isConnectedSize, int* isConnectedColSize)
  {
      int cityNum = isConnectedSize; // 城市个数
      int visited[cityNum];
      memset(visited, 0, sizeof(visited));
      int provinceNum = 0;
      for (int i = 0; i < cityNum; i++) {
          if (visited[i] == 0){ // 该城市未被访问过
              dfs(isConnected, visited, cityNum, i);
              provinceNum++;
          }
      }
      return provinceNum;
  }
  ```

  #### 如何在网格上做 DFS

  网格问题是这样一类搜索问题：有 m×n 个小方格，组成一个网格，每个小方格与其上下左右四个方格认为是相邻的，要在这样的网格上进行某种搜索。这种题目乍一看可能有点麻烦，实际上非常简单，尤其是用 DFS 的方法。题目没有限制的话，我们尽量用 DFS 来写代码。

  下面我们一步步地构造出方格类 DFS 的代码。

  首先，每个方格与其上下左右的四个方格相邻，则 DFS 每次要分出四个岔：

  ```c
  // 基本的 DFS 框架：每次搜索四个相邻方格
  void dfs(int** grid, int r, int c) {
      dfs(grid, r - 1, c); // 上边相邻
      dfs(grid, r + 1, c); // 下边相邻
      dfs(grid, r, c - 1); // 左边相邻
      dfs(grid, r, c + 1); // 右边相邻
  }
  ```

  但是，对于网格边缘的方格，上下左右并不都有邻居。

  一种做法是在**递归调用之前判断方格的位置**，例如位于左边缘，则不访问其左邻居。但这样一个一个判断写起来比较麻烦，我们可以用“先污染后治理”的方法，先做递归调用，再在每个 DFS 函数的开头判断坐标是否合法，不合法的直接返回。同样地，我们还需要判断该方格是否有岛屿（值是否为 1），否则也需要返回。

  ```c
  // 处理方格位于网格边缘的情况
  void dfs(char **grid, int row, int col, int i, int j)
  {
      // 若坐标不合法直接返回
      if ( i < 0 || j < 0 || i >= row || j >= col || grid[i][j] != '1'){
          return;
      }
      grid[i][j] = '0';
      dfs(grid, row, col, i+1, j);
      dfs(grid, row, col, i-1, j);
      dfs(grid, row, col, i, j+1);
      dfs(grid, row, col, i, j-1);
  }
  ```

  但是这样还有一个问题：DFS 可能会不停地“兜圈子”，永远停不下来，如下图所示：

  那么我们需要标记遍历过的方格，保证方格不进行重复遍历。标记遍历过的方格并不需要使用额外的空间，只需要改变方格中存储的值就可以。
  在这道题中，

  - 0 表示非岛屿（不可遍历）
  - 1 表示岛屿（可遍历）
  - 2 表示已遍历过的岛屿

  这样，我们就得到了网格 **DFS 遍历的框架代码**：

  ```c
  // 标记已遍历过的岛屿，不做重复遍历
  void dfs(char **grid, int row, int col, int i, int j)
  {
      // 若坐标不合法直接返回，已遍历过（值为2）的岛屿在这里会直接返回，不会重复遍历
      if ( i < 0 || j < 0 || i >= row || j >= col || grid[i][j] != '1'){
          return;
      }
      grid[i][j] = 2; // 将方格标记为"已遍历"
      dfs(grid, row, col, i+1, j);
      dfs(grid, row, col, i-1, j);
      dfs(grid, row, col, i, j+1);
      dfs(grid, row, col, i, j-1);
  }
  ```

  ### 3.4 题目解析

  例1：463.求岛屿的周长
  求岛屿的周长其实有很多种方法，如果用 DFS 遍历来求的话，有一种很简单的思路：**岛屿的周长就是岛屿方格和非岛屿方格相邻的边的数量**。注意，这里的非岛屿方格，既包括水域方格，也包括网格的边界。我们可以画一张图，看得更清晰：

  [外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-LyIOJD5M-1655917816196)(http://image.huawei.com/tiny-lts/v1/images/3f98149038753eecccd4c700fdc6cf0e_1200x500.jpg@900-0-90-f.jpg)]

  将这个“相邻关系”对应到 DFS 遍历中，就是：每当在 DFS 遍历中，从一个岛屿方格走向一个非岛屿方格，就将周长加 1。代码如下：

  ```c
  #define LAND 1
  #define SEA 0
  
  const int g_dx[4] = {0,1,0,-1};
  const int g_dy[4] = {1,0,-1,0};
  
  int dfs(int** grid, int row, int col, int i, int j)
  {
      //进入水区或边界则周长加一
      if (i < 0 || j < 0 || i >= row || j >= col || grid[i][j] == SEA){
          return 1;
      }
  
      //已查找过查找过的不计算
      if (grid[i][j] == 2){
          return 0;
      }
  
      //标记已经被查找过的陆地
      grid[i][j] = 2;
      return dfs(grid, row, col, i + 1, j) +
             dfs(grid, row, col, i - 1, j) +
             dfs(grid, row, col, i, j + 1) +
             dfs(grid, row, col, i, j - 1);
  }
  
  int islandPerimeter(int** grid, int gridSize, int* gridColSize){
      int row = gridSize;
      for (int i = 0; i < row; i ++){
          int col = gridColSize[i];
          for (int j = 0; j < col; j++){
              if (grid[i][j] == LAND){
                  return dfs(grid, row, col, i, j);
              }
          }
      }
      return 0;
  }
  ```

  例2：695.岛屿最大面积

  ```c
  int dfs(int** grid, int row, int col, int i, int j)
  {
      if (i < 0 || j < 0 || i >= row || j >= col || grid[i][j] != 1){
          return 0;
      }
      grid[i][j] = 2;
      return dfs(grid, row, col, i - 1, j) + 
             dfs(grid, row, col, i + 1, j) +
             dfs(grid, row, col, i, j - 1) +
             dfs(grid, row, col, i, j + 1) + 1;
  }
  
  int maxAreaOfIsland(int** grid, int gridSize, int* gridColSize)
  {
      int row, col;
      row = gridSize;
      int ret = 0;
      for (int i = 0; i < row; i++){
          col = gridColSize[i];
          for (int j = 0; j < col; j++){
              if (grid[i][j] == 1) {
                  int area = dfs(grid, row, col, i, j);
                  ret = fmax(ret, area);
              }
          }
      }
      return ret;
  }
  ```

  例3：200.岛屿数量

  ```c
  #define LAND 1
  #define SEA  0
  
  void dfs(char **grid, int row, int col, int i, int j)
  {
      if ( i < 0 || j < 0 || i >= row || j >= col || grid[i][j] == '0'){
          return;
      }
      grid[i][j] = '0';
      dfs(grid, row, col, i+1, j);
      dfs(grid, row, col, i-1, j);
      dfs(grid, row, col, i, j+1);
      dfs(grid, row, col, i, j-1);
  }
  
  int numIslands(char** grid, int gridSize, int* gridColSize)
  {
      int ret = 0;
      for (int i = 0; i < gridSize; i++){
          for (int j = 0; j < gridColSize[i]; j++){
              if (grid[i][j] == '1'){
                  dfs(grid, gridSize, gridColSize[i], i, j);
                  ret++;
              }
          }
      }
      return ret;
  }
  ```

  参考资料：

  https://leetcode.cn/problems/island-perimeter/solution/tu-jie-jian-ji-er-qiao-miao-de-dfs-fang-fa-java-by/
  https://leetcode.cn/problems/number-of-islands/solution/dao-yu-lei-wen-ti-de-tong-yong-jie-fa-dfs-bian-li-/

  ## 4 广度优先搜索 BFS

  ### 4.1 基础知识

  常见的BFS用来解决什么问题？(1) 简单图（有向无向皆可）的最短路径长度，注意是长度而不是具体的路径（2）拓扑排序 （3） 遍历一个图（或者树）

  ### 4.2 BFS 基本模板

  分为需要记录层数和不需要记录层数，多数情况下时间复杂度空间复杂度都是O（N+M），N为节点个数，M为边的个数

  ### 4.3 BFS 题目

  #### 基于树的BFS

  **不需要专门一个set来记录访问过的节点**

  Leetcode 102 Binary Tree Level Order Traversal
  Leetcode 103 Binary Tree Zigzag Level Order Traversal
  Leetcode 297 Serialize and Deserialize Binary Tree （很好的BFS和双指针结合的题）
  Leetcode 314 Binary Tree Vertical Order Traversal

  #### 基于图的BFS

  **一般需要一个set来记录访问过的节点**

  - Leetcode 200. Number of Islands
  - Leetcode 133. Clone Graph
  - Leetcode 127. Word Ladder
  - Leetcode 490. The Maze
  - Leetcode 323. Connected Component in Undirected Graph
  - Leetcode 130. Surrounded Regions
  - Leetcode 752. Open the Lock
  - Leetcode 815. Bus Routes
  - Leetcode 1091. Shortest Path in Binary Matrix
  - Leetcode 542. 01 Matrix
  - Leetcode 1293. Shortest Path in a Grid with Obstacles Elimination
  - Leetcode 417. Pacific Atlantic Water Flow

  ### 拓扑排序

  https://zh.wikipedia.org/wiki/%E6%8B%93%E6%92%B2%E6%8E%92%E5%BA%8F

  - Leetcode 207 Course Schedule （I, II）
  - Leetcode 444 Sequence Reconstruction
  - Leetcode 269 Alien Dictionary
  - Leetcode 310 Minimum Height Trees
  - Leetcode 366 Find Leaves of Binary Tree

  ## 5 二叉树

  ### 5.1 基础知识

  http://data.biancheng.net/view/195.html

  #### 5.1.1 二叉树的遍历方式

  二叉树主要有两种遍历方式：
  深度优先遍历：先往深走，遇到叶子节点再往回走。

  - 前序遍历（递归法，迭代法）
  - 中序遍历（递归法，迭代法）
  - 后序遍历（递归法，迭代法）

  1. 先序遍历：每遇到一个节点，先访问，然后再遍历其左右子树
  2. 中序遍历：第一次经过时不访问，等遍历完左子树之后再访问，然后遍历右子树
  3. 后序遍历：第一次和第二次经过时都不访问，等遍历完该节点的左右子树之后，最后访问该节点

  广度优先遍历：一层一层的去遍历。

  - 层次遍历（迭代法）

  #### 5.1.2 二叉树的性质

  叶子结点: 一棵树当中没有子结点的节点（即度为0）。

  1. 二叉树中，第 i 层最多有 2^i - 1 个结点。
  2. 如果二叉树的深度为 K，那么此二叉树最多有 2^k - 1 个结点。
  3. 二叉树中，终端结点数（叶子结点数）为 n0，度为 2 的结点数为 n2，则 n0=n2+1。

  ### 5.2 二叉树类题目

  - leetcode102. 二叉树的层序遍历 https://leetcode.cn/problems/binary-tree-level-order-traversal/

  ## 6 排序 Sort

  ### 6.1 基础知识

  快速排序（Quick Sort），归并排序（Merge Sort）的原理与代码实现。需要能讲明白代码中每一行的目的。快速排序时间复杂度平均状态下 O（NlogN），空间复杂度O（1），归并排序最坏情况下时间复杂度O（NlogN），空间复杂度O（N）

  - 稳定排序：如果 a 原本在 b 的前面，且 a == b，每次排序之后 a 都在 b 的前面，则为稳定排序。
  - 非稳定排序：如果 a 原本在 b 的前面，且 a == b，每次排序之后 a 可能不在 b 的前面，则为非稳定排序。
  - 原地排序：原地排序就是指在排序过程中不申请多余的存储空间，只利用原来存储待排数据的存储空间进行比较和交换的数据排序。
  - 非原地排序：需要利用额外的存储空间来辅助排序。
    <p align="center">
      <img src="http://image.huawei.com/tiny-lts/v1/images/bc042640ccee897a57d4b765b16b5c5a_1926x1144.jpg@900-0-90-f.jpg" alt="图片描述"/>
    </p>

  #### 6.1.1 冒泡排序

  ```c
  void bubble_sort(int arr[], int n) {
      for (int i = 0; i < n - 1; i++) {                //N个数共需进行N-1轮
          int flag = 0;
          for (int j = 0; j < n - i - 1; j++) {         //第i轮需要比较N-i-1次
              if (arr[j] > arr[j + 1]) {               //若前面一个元素大于后面一个元素，则交换
                  int tmp = arr[j];
                  arr[j] = arr[j + 1];
                  arr[j + 1] = tmp;
                  flag = 1;                              //若进行了数据交换，则flag赋值为1
              }
              if (flag == 0) break;  //如果没有进行数据交换，则结束排序
          }
      }
  }
  ```

  #### 6.1.2 快速排序

  ### 6.2 排序类题目

  入门题目：

  - Leetcode 148. Sort List
  - Leetcode 56. Merge Intervals
  - Leetcode 27. Remove elements

  进阶题目：

  - Leetcode 179. Largest Number
  - Leetcode 75. Sort Colors
  - Leetcode 215. Kth Largest Element （可以用堆的解法替代）
  - Leetcode 4. Median of Two Sorted Arrays
    注意：后两题是与快速排序非常相似的快速选择（Quick Select）算法，面试中很常考

  参考资料：

  ### 6.N 参考资料

  [一文搞定常见的链表问题]( https://leetcode.cn/problems/linked-list-cycle/solution/yi-wen-gao-ding-chang-jian-de-lian-biao-wen-ti-h-2/)

  1. [十大排序算法](https://github.com/hustcc/JS-Sorting-Algorithm)

  

  ## 7 并查集

  ## 8 双指针

  常见双指针算法分为三类，

  - 同向（即两个指针都相同一个方向移动）
  - 背向（两个指针从相同或者相邻的位置出发，背向移动直到其中一根指针到达边界为止）
  - 相向（两个指针从两边出发一起向中间移动直到两个指针相遇）

  ### 8.1 背向双指针

  基本上全是回文串的题

  - Leetcode 409. Longest Palindrome
  - Leetcode 125. Valid Palindrome
  - Leetcode 5. Longest Palindromic Substring
  - Leetcode 647. Palindromic Substrings

  ### 8.2 相向双指针

  以two sum为基础的一系列题

  - Leetcode 1. Two Sum (这里使用的是先排序的双指针算法，不同于hashmap做法)
  - Leetcode 167. Two Sum II - Input array is sorted
  - Leetcode 15. 三数之和 （完成）
  - Leetcode 16. 最接近的三数之和 https://leetcode.cn/problems/3sum-closest/ （完成）
  - Leetcode 18. 4Sum
  - Leetcode 454. 4Sum II
  - Leetcode 277. Find the Celebrity
  - Leetcode 11. Container With Most Water

  **Leetcode.16 最接近的三数之和**

  排序 + 双指针 去重：

  ```c
  while (left < right && nums[left] == nums[++left]);   // 去重
  while (left < right && nums[right] == nums[--right]); // 去重
  ```

  ### 8.3 同向双指针

  个人觉得最难的一类题，可以参考下这里 TimothyL：Leetcode 同向双指针/滑动窗口类代码模板

  - Leetcode 283. Move Zeroes
  - Leetcode 26. Remove Duplicate Numbers in Array
  - Leetcode 395. Longest Substring with At Least K Repeating Characters
  - Leetcode 340. Longest Substring with At Most K Distinct Characters
  - Leetcode 424. Longest Repeating Character Replacement
  - Leetcode 76. Minimum Window Substring
  - Leetcode 3. Longest Substring Without Repeating Characters
  - Leetcode 1004 Max Consecutive Ones III

  ## 9 链表

  ### 9.1 基础知识

  链表如何实现，如何遍历链表。链表可以保证头部尾部插入删除操作都是O（1），查找任意元素位置O（N）

  求链表长度

  ```c
  int length(struct ListNode* head)
  {
      if(head == NULL) {
          return 0;
      }
      return length(head->next) + 1;
  }
  ```

  ### 9.2 链表类基础题目

  - Leetcode 2. 两数相加 https://leetcode.cn/problems/add-two-numbers/  
  - 剑指 Offer 18. 删除链表的节点 https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/
  - Leetcode 206. Reverse Linked List
  - Leetcode 876. Middle of the Linked List

  例：剑指 Offer 18. 删除链表的节点

  ```c
  struct ListNode* deleteNode(struct ListNode* head, int val)
  {
      struct ListNode* curr = head;
      if (curr->val == val) {
          return curr->next;
      }
      while (curr) {
          if (curr->next->val == val) {
              curr->next = curr->next->next;
              break;
          }
          curr = curr->next;
      }
      return head;
  }
  ```

  注意：快慢指针和链表反转几乎是所有链表类问题的基础，尤其是反转链表，代码很短，建议直接背熟。

  进阶题目:

  - Leetcode 160. Intersection of Two Linked Lists
  - Leetcode 141. Linked List Cycle (Linked List Cycle II)
  - Leetcode 92. Reverse Linked List II
  - Leetcode 328. Odd Even Linked List

  ### 9.3 参考资料

  [一文搞定常见的链表问题]( https://leetcode.cn/problems/linked-list-cycle/solution/yi-wen-gao-ding-chang-jian-de-lian-biao-wen-ti-h-2/)

  

  ## 10 哈希表

  ### 10.1 基础知识

  哈希表是一种使用哈希函数组织数据，以支持快速插入和搜索的数据结构。

  有两种不同类型的哈希表：哈希集合和哈希映射。

  - **哈希集合**是集合数据结构的实现之一，用于存储非重复值。
  - **哈希映射**是映射数据结构的实现之一，用于存储(key, value)键值对。

  在标准模板库的帮助下，哈希表是易于使用的。大多数常见语言（如Java，C ++ 和 Python）都支持哈希集合和哈希映射。