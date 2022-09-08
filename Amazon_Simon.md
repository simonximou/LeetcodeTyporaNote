# Amazon_Simon



## Data Structure:

### Monotone Stack:

```py
for next_smaller in range(n+1):
            # we pop from the stack in order to satisfy the monotonically increasing order property
			# if we reach the end of the iteration and there are elements present in the stack, we pop all of them
            while stack and (next_smaller == n or nums[stack[-1]] > nums[next_smaller]):
                i = stack.pop()
                prev_smaller = stack[-1] if stack else -1
                submin += nums[i] * (next_smaller - i) * (i - prev_smaller)
            stack.append(next_smaller)

        
        # then calculate sum{ Max(subarray) } over all subarrays
        # sum{ Max(subarray) } = sum(f'(i) * nums[i]) ; i=0..n-1
        # where f'(i) is number of subarrays where nums[i] is the maximum value
        # f'(i) = (i - index of the previous larger value) - (index of the next larger value - i) * nums[i]
        # this time we use a monotonically decreasing stack.
        stack = []
        # we pop from the stack in order to satisfy the monotonically decreasing order property
			# if we reach the end of the iteration and there are elements present in the stack, we pop all of them
        for next_larger in range(n+1):
            while stack and (next_larger == n or nums[stack[-1]] < nums[next_larger]):
                i = stack.pop()
                prev_larger = stack[-1] if stack else -1
                submax += nums[i] * (next_larger - i) * (i - prev_larger)
            stack.append(next_larger)
```



## LC

### OA:Max Average Stock Price:

![192634ubj0cg7cgggpcl00.jpg](https://codaio.imgix.net/docs/m5fzh3MwOp/blobs/bl-U1nH5dzwGR/ddbd59bb71bb3151abc517afaa80f4eb395602c6645695087cda184812716f18261e9142185eb410033e3c8d92cafc5c7d58f6c089783dac81246f9905af64f36d1735cfb5cd36f8b4990fd0dafdca941d16193b32bc3b185c38a20d00f55a6b2bdabee0?auto=format%2Ccompress&fit=max)



* Sliding window
* while the length of the window is greater than k or the stock price has already existed in the window
* remove the left element until the length of the window < k or the stock price is removed from the window

```python
# Sliding Window

def obssum(stockPrice, k):
    left = 0
    res = -1
    curSum = 0
    window = set()
    n = len(stockPrice)
    if n < k:
        return res
    for right in range(n):
        while left < right and (len(window) >= k or stockPrice[right] in window):
            curSum -= stockPrice[left]
            window.remove(stockPrice[left])
            left += 1
        curSum += stockPrice[right]
        window.add(stockPrice[right])
        if len(window) == k:
            res = max(res,curSum)
    return res
```



```py
def obssum(stockPrice, k):
  	if len(stockPrice) < k:
      	return -1
    maxSum = -1
    for i in range(0, len(stockPrice) - k + 1):
        if len(set(stockPrice[i:i+k])) == k:
            maxSum = max(maxSum, sum(stockPrice[i:i+k]))
    return maxSum
  
```

### OA: Move Location

![img](https://oss.1point3acres.cn/forum/202201/25/143842g6qauymuuc5u8vr2.jpeg)

keep a set to store the current location

* if the location exists in moved from, remove it from the set, add the corresponding index element into the set

* finally return the sorted set 

  ```py
  def findLoc(locations, movedFrom, movedTo):
      currLocations = set(locations)
      
      i = 0
      while i < len(movedFrom):
          currLocations.remove(movedFrom[i])
          currLocations.add(movedTo[i])
          i += 1
      return sorted(list(currLocations))
  
  locations = [1, 7, 6, 8]
  movedFrom = [1, 7, 2]
  movedTo = [2, 9, 5]
  
  res = findLoc(locations, movedFrom, movedTo)
  print(res)
  ```

### 102. Binary Tree Level Order 

Given the `root` of a binary tree, return a list with the max value of each level* in ascending order. (i.e., from left to right, level by level).

 https://www.1point3acres.com/bbs/thread-916192-1-1.html

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [3,15,20]
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
def levelOrder(self, root):
        """
        BFS, for each level do DFS way
        """
        #BFS
        #use a variable to store max value in each level 
            #after each level append into res 
        #return sorted res
        #Time:O(NLOGN)
        #Space:O(N)
        if not root:
            return []
        res = []
        que = collections.deque([root])
        while que:
            max_level = -float("inf")
            #for each level
            for i in range(len(que)):
                #get each node
                cur = que.popleft()
                #update maxVal of current level
                max_level = max(max_level, cur.val)
                #append child nodes into que
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
            #append into res
            res.append(max_level)
            
        return sorted(res)
                    
```



### **314.Binary Tree Vertical Order Traversal**

Given the `root` of a binary tree, return an ascending ordering list with the max value of each of ****the vertical order traversal*** of its nodes' values*. (i.e., from left to right, level by level from leaf to root).

https://www.1point3acres.com/bbs/thread-916192-1-1.html

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [7,9,15,20]
```

```PY
 def verticalOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        root level == 0, each left level-1, right level+1
        hashmap to store each level maximum
        Time: O(NLOGN)
        Space: O(n)
        """
        if not root:
            return []
        mapping = collections.defaultdict(int)
        res = []
        que = collections.deque()
        level = 0
        que.append((root,level))
        while que:
            for i in range(len(que)):
                cur, cur_level = que.popleft()
                mapping[cur_level] = max(mapping[cur_level], cur.val)
                if cur.left:
                    que.append((cur.left, cur_level-1))
                if cur.right:
                    que.append((cur.right, cur_level+1))
        print mapping
        for key,val in mapping.items():
            res.append(val)
        return sorted(res)
                
```

### 141. Linked List Cycle

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

Return `true` *if there is a cycle in the linked list*. Otherwise, return `false`.

 https://www.1point3acres.com/bbs/thread-915369-1-1.html

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
```

```py
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        #use slow and fast pointer
        while head:
            next = head.next
            if next == head:
                return true
            else:
                head.next = head
            head = next
        return False
```



\142. Linked List Cycle II

Medium

8262566Add to ListShare

Given the `head` of a linked list, return *the node where the cycle begins. If there is no cycle, return* `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

```py
 def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        #Time: O(n+k)
        #Space: O(1)
        #base case
        if not head or not head.next:
            return None
        fast, slow = head, head
        #while valid
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            #loop found, two pointer meet
            if slow == fast:
                #restart one from head, to find n steps
                slow2 = head
                while slow2 != fast:
                    #if we wanted to disconnext circle
                    #temp = fast
                    slow2 = slow2.next
                    fast = fast.next
                #if we wanted to disconnext circle
                # temp.next = None
                return slow2
        #no loop
        return None
```

### \200. Number of Islands

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

**Example 1:**

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

```py
def numIslands(self, grid):
        """
        Better BFS VERSION
        """
        if not grid:
            return 0
        que = collections.deque()
        row,col = len(grid),len(grid[0])
        res = 0
        for i in range(row):
            for j in range(col):
                if grid[i][j] == "1":
                    que.append((i,j))
                    res += 1
                    while que:
                        cur_row, cur_col = que.popleft()
                        if 0<=cur_row<row and 0<=cur_col<col and grid[cur_row][cur_col] == "1":
                            grid[cur_row][cur_col] = "0"
                            que.append((cur_row+1,cur_col))
                            que.append((cur_row,cur_col+1))
                            que.append((cur_row-1,cur_col))
                            que.append((cur_row,cur_col-1))
        
        return res
        
        
        #         """
#         DFS similar to 695. loop through all the elements and when meet "1" call dfs function and turn all the connected 1s into 0s 
#         """
#         # define dfs functions
#         def helper(grid, row, col):
#             grid[row][col] = "0"
#             for a,b in ([1,0],[0,1],[-1,0],[0,-1]):
#                 if 0<=row+a<len_row and 0<=col+b<len_col and grid[row+a][col+b] == "1":
#                     helper(grid, row+a, col+b)
            
        
#         len_row, len_col = len(grid), len(grid[0])
#         res = 0
#         for i in range(len_row):
#             for j in range(len_col):
#                 if grid[i][j] == "1":
#                     res += 1
#                     helper(grid, i, j)
#         return res 
```

### Employee 

```
Data Structure
让我随便选几个DS， 描述他们是干什么的， 然后time complexity啥的。
我说stack，heap， graph， linkedlist， trie
说完后，老哥开了codepad

Coding
上来给我几个array:
uid: 12, 23, 32,1
name: blah blah blah,
type: f, p, f, p, p (fulltime/partime)
start_date: 2012/05, 2012/04, ...
然后说要实现通过uid来获得employee的信息，我就建了个class Employee， 然后用hashmap， key是uid， 然后value是那个Emloyee class。
然后老哥说要我获取employee的name，但不想给developer直接到map的access。然后我就写了个getter function， 然后把map标了private。
然后老哥说能不能从data structure 方面优化我之前写的那个Employee class。一开始不知道啥意思， 然后他hint了下，然后我说可以用enum来代表employee type。然后他说OK， 然后问我这个enum的好处在哪。我说it's good for readability and it's safe so that ppl don't pass in junks
```

### \347. Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

```py
def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        #Heap problem
        #use int dict to find frequency, -1 for finding item, then push into heap, pop in res
        
        dic = collections.defaultdict(int)
        
        for i in nums:
            if i in dic:
                dic[i] -= 1
            else:
                dic[i] = -1
        
        #now we have a dict holding item and freq
        heap = []
        for key in dic:
            heapq.heappush(heap, (dic[key], key))
            
        #now ew have a heap with sorted freq, since -1, appeared more will be at the front
        res = []
        counter = 0
        while counter < k:
            res.append(heapq.heappop(heap)[-1])
            counter +=1 
        return res
```

\1010. Pairs of Songs With Total Durations Divisible by 60

Medium

3324128Add to ListShare

You are given a list of songs where the `ith` song has a duration of `time[i]` seconds.

Return *the number of pairs of songs for which their total duration in seconds is divisible by* `60`. Formally, we want the number of indices `i`, `j` such that `i < j` with `(time[i] + time[j]) % 60 == 0`.

 

**Example 1:**

```
Input: time = [30,20,150,100,40]
Output: 3
Explanation: Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
```

```py
class Solution(object):
    def numPairsDivisibleBy60(self, time):
        """
        :type time: List[int]
        :rtype: int
        """
        #hashmap to store all the reminder count 
        #only need one loop since we dont want to avoid double count 
        hashmap = collections.defaultdict(int)
        res = 0
        for i in time:
            if i%60 ==0:
                res += hashmap[0]
            else:
                res += hashmap[60-i%60]
            hashmap[i%60] += 1
        return res
        #Time: O(n)
        #Space: O(n)
```

### \33. Search in Rotated Sorted Array

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of* `target` *if it is in* `nums`*, or* `-1` *if it is not in* `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

```py
def search(self, nums, target):
        if not (nums or taget):
            return -1
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) // 2
            if nums[start] <= nums[mid]:
                if target <= nums[mid] and target >= nums[start]:
                    end = mid
                else:
                    start = mid
            else:
                if target <= nums[end] and target >= :
                    start = mid
                else:
                    end = mid
        if nums[start] == target:
            return start
        elif nums[end] == target:
            return end
        else:
            return -1
```

### \863. All Nodes Distance K in Binary Tree

Medium

6881134Add to ListShare

Given the `root` of a binary tree, the value of a target node `target`, and an integer `k`, return *an array of the values of all nodes that have a distance* `k` *from the target node.*

You can return the answer in **any order**.

 

**Example 1:**

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/06/28/sketch0.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, k = 2
Output: [7,4,1]
Explanation: The nodes that are a distance 2 from the target node (with value 5) have values 7, 4, and 1.
```

```py
def distanceK(self, root, target, k):
        """
        :type root: TreeNode
        :type target: TreeNode
        :type k: int
        :rtype: List[int]
        """
        """
        Use a DFS to build the map, keys are node.val and values are connexted nodes
        Then use a BFS to find the k far nodes
        """
        res = []
        mapping = self.dfs(root, collections.defaultdict(list), None)
        #bfs to find the 
        print mapping
        que = collections.deque()
        que.append((target.val, 0))
        visited = set()
        visited.add(target.val)
        while que:
            cur, level = que.popleft()
            if level == k:
                res.append(cur)
            else:
                for neibor in mapping[cur]:
                    if neibor not in visited:
                        que.append((neibor,level+1))
                        visited.add(neibor)
        return res
        
    def dfs(self,root, mapping, parent):
        if not root:
            return
        #add parent and child node into mapping
        if parent != None:
            mapping[root.val].append(parent)
        if root.left:
            mapping[root.val].append(root.left.val)
            self.dfs(root.left, mapping, root.val)
        if root.right:
            mapping[root.val].append(root.right.val)
            self.dfs(root.right, mapping, root.val)
        return mapping
```

### \105. Construct Binary Tree from Preorder and Inorder Traversal

Medium

10385280Add to ListShare

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return *the binary tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

```py
def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        """
        first for loop preorder because the parent node will at the front
        second find each parent node in inorder to identify where they are 
        third dfs left and right of each parent node
        """
        #base case
        if not preorder or not inorder:
            return None
        if len(preorder) == 1:
            return TreeNode(preorder[0])
        
        #find the index of root
        root = TreeNode(preorder[0])
        root_index = inorder.index(preorder[0])
        #recursive steps
        root.left = self.buildTree(preorder[1:root_index+1], inorder[:root_index])
        root.right = self.buildTree(preorder[root_index+1:], inorder[root_index+1:])
        return root
```

### \253. Meeting Rooms II

Medium

5814117Add to ListShare

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of conference rooms required*.

 

**Example 1:**

```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: 2
```

```py
def minMeetingRooms(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: int
        """
        """
        Find maximum overlaps 
        or we can use heap, 
        """
        #use array to store all the start and end time
        start = [0] * len(intervals)
        end = [0] * len(intervals)
        for i in range(len(intervals)):
            start[i] = intervals[i][0]
            end[i] = intervals[i][1]
        #sort the arrays, so we have start and end time in order. Allows us to compare each start time with end time
        start = sorted(start)
        end = sorted(end)

        #compare each start time with last end time, if start<end, we need one more room
        room = 0
        endPt = 0
        for startPt in start:
            #if start < end, we need one more room because overlap
            if startPt < end[endPt]:
                room += 1
            else:
                endPt+=1
        
        return room
```

### \207. Course Schedule

Medium

10614414Add to ListShare

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

 

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.
```

```py
def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        """
        topological sort because each node a 
        """
        #First create a graph with all the adjacent vertex
        graph = collections.defaultdict(list)
        indegree = [0] * numCourses
        #store each vertex's indegree at the same time in array
            #use a variable to check if there is indegree 0
             #if not, return False
        for i, j in prerequisites:
            graph[i].append(j)
            indegree[j] += 1
        
        #initialize que
        que = collections.deque()
        for course, degree in enumerate(indegree):
            if degree == 0:
                que.append(course)
        if not que:
            return False
        
        #do BFS on indegree 0's
            #for all adjacency list, indgree -1
            #if indegree == 0: append to que
        while que:
            cur = que.popleft()
            for x in graph[cur]:
                indegree[x] -= 1
                if indegree[x] == 0:
                    que.append(x)

        #return if there is still vertex left in que
        return sum(indegree) == 0
        
```

\210. Course Schedule II

Medium

7462254Add to ListShare

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

- For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return *the ordering of courses you should take to finish all courses*. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

 

**Example 1:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```

```py
 def findOrder(self, numCourses, prerequisites):
        """
        same thing as 207 where you use topological sort to do
        bfs + indegree + hashmap
        
        """
        res = []
        graph = defaultdict(list)
        indegree = [0] * numCourses
        for pre in prerequisites:
            indegree[pre[0]] += 1
            graph[pre[1]].append(pre[0])
        queue = collections.deque()
        has_zero = False
        for n in range(numCourses):
            if indegree[n] == 0:
                queue.append(n)
                has_zero = True
        if has_zero == False:
            return []
        while queue:
            course = queue.popleft()
            res.append(course)
            for neighbor in graph[course]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    queue.append(neighbor)
        if sum(indegree) != 0:
            return []
        return res
```

### \349. Intersection of Two Arrays

Easy

33311969Add to ListShare

Given two integer arrays `nums1` and `nums2`, return *an array of their intersection*. Each element in the result must be **unique** and you may return the result in **any order**.

 

**Example 1:**

```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

```py
def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        res = set()
        for i in nums1:
            if i in nums2:
                res.add(i)
        return res
```

```py
Follow up: if sorted, time O(n) space O(1)
def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        num1 = sorted(nums1)
        num2 = sorted(nums2)
        res = []
        left, right = 0, 0
        len1, len2 = len(nums1), len(nums2)
        while left < len1 and right < len2:
            tempL, tempR = num1[left], num2[right]
            #if left == right:
            if tempL == tempR:
                #push into res
                if not res or res[-1] != tempL:
                    res.append(tempR)
                #left++ right++ till next number
                left += 1
                right += 1
                    
            #else if left < right:
            elif tempL < tempR:
                left += 1
            else:
                #right++ till next number
                right += 1
        return res
                
```

### \146. LRU Cache

Medium

14431571Add to ListShare

Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.

Implement the `LRUCache` class:

- `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

 

**Example 1:**

```
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

```py
#since we want O(1) get and put, intuitively we should use a dict to store key and vals
#also since we want to evict the least revcent used key, we would need to store the time relation
#array would not fit becasue we need O(n) to delete
#here we will use linked list on each node in the dicts to connext their relations
#

class Node(object):
    def __init__(self, k, v):
        self.key = k
        self.val = v
        self.next = None
        self.prev = None
        

        
        
class LRUCache(object):
    
    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.dict = {}
        self.capa = capacity
        self.head = Node(0,0)
        self.tail = Node(0,0)
        self.head.next = self.tail
        self.tail.prev = self.head
        
    #add the node at the front of our doubly linked list 
    def _add(self, node):
        n = self.head.next
        n.prev = node
        self.head.next = node
        node.next = n
        node.prev = self.head
        
        
    #delete the node wherever it is         
    def _delete(self, node):
        n = node.next
        p = node.prev
        n.prev = p
        p.next = n
        
        
    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        #return val is exist + put it at the front
        #else return -1
        if key in self.dict:
            res = self.dict[key]
            self._delete(res)
            self._add(res)
            return res.val
        else:
            return -1

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: None
        """
        #update if in the dict
        if key in self.dict:
            res = self.dict[key]
            self._delete(res)
        node = Node(key, value)
        #else add into cache
        self._add(node)
        self.dict[key] = node
        #if overflow
        if self.capa < len(self.dict):
            #delete the least recent
            n = self.tail.prev
            self._delete(n)
            del self.dict[n.key]
```

### **$2104. Sum of Subarray Ranges**

Medium

107256Add to ListShare

You are given an integer array `nums`. The **range** of a subarray of `nums` is the difference between the largest and smallest element in the subarray.

Return *the **sum of all** subarray ranges of* `nums`*.*

A subarray is a contiguous **non-empty** sequence of elements within an array.

 

**Example 1:**

```
Input: nums = [1,2,3]
Output: 4
Explanation: The 6 subarrays of nums are the following:
[1], range = largest - smallest = 1 - 1 = 0 
[2], range = 2 - 2 = 0
[3], range = 3 - 3 = 0
[1,2], range = 2 - 1 = 1
[2,3], range = 3 - 2 = 1
[1,2,3], range = 3 - 1 = 2
So the sum of all ranges is 0 + 0 + 0 + 1 + 1 + 2 = 4.
```

```py
def subArrayRanges(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        """
        Solution1:
        two for loops and mark max min which updating res, O(n^2)
        
        Solution2 O(n):
        since sum of all subarray ranges = sum(max of subarr) - sum(min of subarr),
        and sum of all max/min of subarray can be solved each by mono stack, we could just go thru two times for each
        """
        # the answer will be sum{ Max(subarray) - Min(subarray) } over all possible subarray
        # which decomposes to sum{Max(subarray)} - sum{Min(subarray)} over all possible subarray
        # so totalsum = maxsum - minsum
        # we calculate minsum and maxsum in two different loops
        n = len(nums)
        res = 0
        submax = submin = 0
        stack = []
        
        
        # first calculate sum{ Min(subarray) } over all subarrays
        # sum{ Min(subarray) } = sum(f(i) * nums[i]) ; i=0..n-1
        # where f(i) is number of subarrays where nums[i] is the minimum value
        # f(i) = (i - index of the previous smaller value) * (index of the next smaller value - i) * nums[i]
        # we can claculate these indices in linear time using a monotonically increasing stack.
        #find submin by using monotone stack, and get rid of them
        for next_smaller in range(n+1):
            # we pop from the stack in order to satisfy the monotonically increasing order property
			# if we reach the end of the iteration and there are elements present in the stack, we pop all of them
            while stack and (next_smaller == n or nums[stack[-1]] > nums[next_smaller]):
                i = stack.pop()
                prev_smaller = stack[-1] if stack else -1
                submin += nums[i] * (next_smaller - i) * (i - prev_smaller)
            stack.append(next_smaller)

        
        # then calculate sum{ Max(subarray) } over all subarrays
        # sum{ Max(subarray) } = sum(f'(i) * nums[i]) ; i=0..n-1
        # where f'(i) is number of subarrays where nums[i] is the maximum value
        # f'(i) = (i - index of the previous larger value) - (index of the next larger value - i) * nums[i]
        # this time we use a monotonically decreasing stack.
        stack = []
        # we pop from the stack in order to satisfy the monotonically decreasing order property
			# if we reach the end of the iteration and there are elements present in the stack, we pop all of them
        for next_larger in range(n+1):
            while stack and (next_larger == n or nums[stack[-1]] < nums[next_larger]):
                i = stack.pop()
                prev_larger = stack[-1] if stack else -1
                submax += nums[i] * (next_larger - i) * (i - prev_larger)
            stack.append(next_larger)
        
        
        
        
        return submax - submin
```

\907. Sum of Subarray Minimums

Medium

3949264Add to ListShare

Given an array of integers arr, find the sum of `min(b)`, where `b` ranges over every (contiguous) subarray of `arr`. Since the answer may be large, return the answer **modulo** `109 + 7`.

 

**Example 1:**

```
Input: arr = [3,1,2,4]
Output: 17
Explanation: 
Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4]. 
Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.
Sum is 17.
```

```py
def sumSubarrayMins(self, arr):
        """
        :type arr: List[int]
        :rtype: int
        """
        """
        use monotone stack to find all the local mins
        """
        n = len(arr)
        stack = []
        sumMin = 0
        for next_smaller in range(n+1):
            while stack and (next_smaller == n or arr[stack[-1]] > arr[next_smaller]):
                cur = stack.pop()
                prev_smaller = stack[-1] if stack else -1
                sumMin += arr[cur]*(cur-prev_smaller)*(next_smaller-cur)     
            stack.append(next_smaller)
        return sumMin% (10**9+7)
        # arr = [0] + arr
        # stack = [0]
        # res = [0]*(len(arr))
        # for next_smaller in range(len(arr)):
        #     while arr[stack[-1]] > arr[next_smaller]:
        #         stack.pop()
        #     j = stack[-1]
        #     res[next_smaller] = res[j] + arr[next_smaller]*(next_smaller - j)
        #     stack.append(next_smaller)   
        # return sum(res)% (10**9+7)
        
```

\39. Combination Sum

Medium

12582260Add to ListShare

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

 

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

```py
def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        """
        about all the combinations, backtracking
        at every candidate, we can choose from all the candidate
        """
        res = []
        self.backtracking([], candidates, target, res)
        return res
        
    def backtracking(self, cur, arr, target, res):
        #base case
        if target<0:
            return
        
        #if we found the correct combo
        if target == 0:
            res.append(cur)
            
        #dfs all the other choices
        for i in range(len(arr)):
            self.backtracking(cur+[arr[i]], arr[i:], target-arr[i], res)
    
```

### \1472. Design Browser History

Medium

1505111Add to ListShare

You have a **browser** of one tab where you start on the `homepage` and you can visit another `url`, get back in the history number of `steps` or move forward in the history number of `steps`.

Implement the `BrowserHistory` class:

- `BrowserHistory(string homepage)` Initializes the object with the `homepage` of the browser.
- `void visit(string url)` Visits `url` from the current page. It clears up all the forward history.
- `string back(int steps)` Move `steps` back in history. If you can only return `x` steps in the history and `steps > x`, you will return only `x` steps. Return the current `url` after moving back in history **at most** `steps`.
- `string forward(int steps)` Move `steps` forward in history. If you can only forward `x` steps in the history and `steps > x`, you will forward only `x` steps. Return the current `url` after forwarding in history **at most** `steps`.

 

**Example:**

```
Input:
["BrowserHistory","visit","visit","visit","back","back","forward","visit","forward","back","back"]
[["leetcode.com"],["google.com"],["facebook.com"],["youtube.com"],[1],[1],[1],["linkedin.com"],[2],[2],[7]]
Output:
[null,null,null,null,"facebook.com","google.com","facebook.com",null,"linkedin.com","google.com","leetcode.com"]
[lc, gg, fb, yb, ln, ]
	 	 ^
Explanation:
BrowserHistory browserHistory = new BrowserHistory("leetcode.com");
browserHistory.visit("google.com");       // You are in "leetcode.com". Visit "google.com"
browserHistory.visit("facebook.com");     // You are in "google.com". Visit "facebook.com"
browserHistory.visit("youtube.com");      // You are in "facebook.com". Visit "youtube.com"
browserHistory.back(1);                   // You are in "youtube.com", move back to "facebook.com" return "facebook.com"
browserHistory.back(1);                   // You are in "facebook.com", move back to "google.com" return "google.com"
browserHistory.forward(1);                // You are in "google.com", move forward to "facebook.com" return "facebook.com"
browserHistory.visit("linkedin.com");     // You are in "facebook.com". Visit "linkedin.com"
browserHistory.forward(2);                // You are in "linkedin.com", you cannot move forward any steps.
browserHistory.back(2);                   // You are in "linkedin.com", move back two steps to "facebook.com" then to "google.com". return "google.com"
browserHistory.back(7);                   // You are in "google.com", you can move back only one step to "leetcode.com". return "leetcode.com"
```

```py


class BrowserHistory(object):
	"""
	用一个list加上两个pointer解决
	一个pointer points to current index
	另一个pointer points to 最右边的网页
	"""
    def __init__(self, homepage):
        """
        :type homepage: str
        """
        self.page = [""]*5000
        self.cur = self.right = 0
        self.page[self.cur] = homepage
        
        

    def visit(self, url):
        """
        :type url: str
        :rtype: None
        """
        self.cur += 1
        self.page[self.cur] = url
        self.right = self.cur

    def back(self, steps):
        """
        :type steps: int
        :rtype: str
        """
        self.cur = max(0, self.cur-steps)
        return self.page[self.cur]
        

    def forward(self, steps):
        """
        :type steps: int
        :rtype: str
        """
        self.cur = min(self.right, self.cur + steps)
        return self.page[self.cur]
```

\39. Combination Sum

Medium

12607260Add to ListShare

Given an array of **distinct** integers `candidates` and a target integer `target`, return *a list of all **unique combinations** of* `candidates` *where the chosen numbers sum to* `target`*.* You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

 

**Example 1:**

```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

```py
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        """
        about all the combinations, backtracking
        at every candidate, we can choose from all the candidate
        """
        res = []
        self.backtracking([], candidates, target, res)
        return res
        
    def backtracking(self, cur, arr, target, res):
        #base case
        if target<0:
            return
        
        #if we found the correct combo
        if target == 0:
            res.append(cur)
            
        #dfs all the other choices
        for i in range(len(arr)):
            self.backtracking(cur+[arr[i]], arr[i:], target-arr[i], res)
    
        
```

\40. Combination Sum II

Medium

6405160Add to ListShare

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

 

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

```py
def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        candidates = sorted(candidates)
        lenth = len(candidates)
        #[1, 1, 2, 5, 6, 7, 10]
        def backtracking(remaining, path, start_index):
            if remaining == 0:
                res.append(path.copy())
                return
            
            for i in range(start_index, lenth):
                if candidates[i] > remaining:
                    break
                if i > start_index and candidates[i] == candidates[i-1]:
                    continue 
                backtracking(remaining - candidates[i], path + [candidates[i]], i+1)
                              
        backtracking(target, [], 0)
        return res
```

\451. Sort Characters By Frequency

Medium

4514190Add to ListShare

Given a string `s`, sort it in **decreasing order** based on the **frequency** of the characters. The **frequency** of a character is the number of times it appears in the string.

Return *the sorted string*. If there are multiple answers, return *any of them*.

 

**Example 1:**

```
Input: s = "tree"
Output: "eert"
Explanation: 'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

```py
"""
O(nlogn)
O(N): counter + bucket sort
"""

def frequencySort(self, s):
        """
        :type s: str
        :rtype: str
        """
        #use a dict to hold the freq and item
        dict = collections.Counter(s)
        heap = []
        
        #put item and freq into maxheap, so sorted 
        for v, t in dict.items():
            heap.append((-t, v))
        heapq.heapify(heap)
        #now we have a sorted heap with elements 
        #just put everything into res
        res = []
        while heap:
            i, j = heapq.heappop(heap)
            res.append(j * -i)
            
        return ''.join(res)
        # since we first use dict, cost O(n), then we heapify which also cost O(n)
        # heappop cost O(nlogk)  where k is the number of distinct character
```

\129. Sum Root to Leaf Numbers

Medium

460587Add to ListShare

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

- For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.

Return *the total sum of all root-to-leaf numbers*. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

```
Input: root = [1,2,3]
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

```py
class Solution(object):
    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        
        self.res = 0
        def dfs(root, cur):
            if not root:
                return
            if not root.left and not root.right:
                self.res += int(cur+str(root.val))
            dfs(root.left, cur+str(root.val))
            dfs(root.right, cur+str(root.val))
            
        dfs(root,"")
        return self.res
```

### \295. Find Median from Data Stream

Hard

7775140Add to ListShare

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

- For example, for `arr = [2,3,4]`, the median is `3`.
- For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

- `MedianFinder()` initializes the `MedianFinder` object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far. Answers within `10-5` of the actual answer will be accepted.

 

**Example 1:**

```
Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
```

```py
class MedianFinder(object):

    def __init__(self):
        self.small = []  # the smaller half of the list, max heap (invert min-heap)
        self.large = []  # the larger half of the list, min heap

    def addNum(self, num):
        if len(self.small) == len(self.large):
            heappush(self.large, -heappushpop(self.small, -num))
        else:
            heappush(self.small, -heappushpop(self.large, num))
        print self.small
        print self.large
    def findMedian(self):
        if len(self.small) == len(self.large):
            return float(self.large[0] - self.small[0]) / 2.0
        else:
            return float(self.large[0])
```

### \56. Merge Intervals

Medium

15327552Add to ListShare

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

 

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

```py
def merge(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: List[List[int]]
        """
        res = []
        intervals = sorted(intervals)
        for i in range(1, len(intervals)):
            if intervals[i][0] <= intervals[i-1][1]:
                intervals[i][0] = intervals[i-1][0]
                intervals[i][1] = max(intervals[i][1], intervals[i-1][1])
            else:
                res.append(intervals[i-1])
        res.append(intervals[-1])
        return res
```

### \128. Longest Consecutive Sequence

Medium

12465525Add to ListShare

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence.*

You must write an algorithm that runs in `O(n)` time.

 

**Example 1:**

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

```py
####hashset, loop thru nums and if the cur_num-1 not in set, we found a start of steak and keep checking if the next is in set and update best#####
def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        num_set = set(nums)
        best = 1
        for i in num_set:
            
            if i-1 not in num_set:
                cur = i
                cur_streak = 1
                while(cur+1 in num_set):
                    cur_streak += 1
                    cur+=1
                best = max(cur_streak, best)
        return best
```

\15. 3Sum

Medium

201091902Add to ListShare

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

 

**Example 1:**

```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
```

```py
def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        #sort, then use a pointer start from left to right -2:
        #pointer + left + right == 0: append
        #if left+right < pointer :left ++ else right ++
        
        nums = sorted(nums)
        res = []
        for i, num in enumerate(nums):
            if i > 0 and nums[i-1] == num:
                continue
            l,r = i+1, len(nums)-1
            while l < r:
                sums = nums[l] + nums[r] + num
                if sums > 0:
                    r -= 1
                elif sums < 0:
                    l += 1
                else:
                    res.append([nums[i],nums[l],nums[r]])
                    l+=1
                    while nums[l] == nums[l-1] and l < r:
                        l+=1
        return res
        
```

### \424. Longest Repeating Character Replacement

Medium

5588220Add to ListShare

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return *the length of the longest substring containing the same letter you can get after performing the above operations*.

 

**Example 1:**

```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```

```py
def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        #use dict to store #of each element, if maxLetter - k > len(dict) we have more than k changed
        dic = collections.defaultdict(int)
        max_len = 0
        max_letter = 0
        left = 0
        for i in range(len(s)):
            dic[s[i]] += 1
            max_letter = max(max_letter, dic[s[i]])
            while i-left+1-k>max_letter:
                dic[s[left]] -= 1
                left += 1
            max_len = max(max_len, i-left+1)
        return max_len

        
```

### $76. Minimum Window Substring

Hard

11630555Add to ListShare

Given two strings `s` and `t` of lengths `m` and `n` respectively, return *the **minimum window substring** of* `s` *such that every character in* `t` *(**including duplicates**) is included in the window. If there is no such substring**, return the empty string* `""`*.*

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

 

**Example 1:**

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

```

```

### \33. Search in Rotated Sorted Array

Medium

165101005Add to ListShare

There is an integer array `nums` sorted in ascending order (with **distinct** values).

Prior to being passed to your function, `nums` is **possibly rotated** at an unknown pivot index `k` (`1 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,5,6,7]` might be rotated at pivot index `3` and become `[4,5,6,7,0,1,2]`.

Given the array `nums` **after** the possible rotation and an integer `target`, return *the index of* `target` *if it is in* `nums`*, or* `-1` *if it is not in* `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

```py
def search(self, nums, target):
        left, right = 0, len(nums)-1
        #first findout which kind it is 
        while left < right:
            mid = (left + right)//2
            if nums[mid] == target:
                return mid
        #case1
        #[4,5,6,7,8,9,1,2,3]
            elif nums[left] <= nums[mid]:
                if target < nums[left] or target > nums[mid]:
                    left = mid+1
                else:
                    right = mid
        
        
        #case2
        #[7,8,9,1,2,3,4,5,6]
            else:
                if target < nums[mid] or target > nums[right]:
                    right = mid
                else:
                    left = mid+1
        if nums[left] == target:
            return left
        return -1

```

### \23. Merge k Sorted Lists

Hard

13485513Add to ListShare

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

*Merge all the linked-lists into one sorted linked-list and return it.*

 

**Example 1:**

```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

```py
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        n = len(lists)
        if n == 0:
            return None
        interval = 1 #starts with 1 but * 2 everytime
        while interval < n:
            for i in range(0, n - interval, interval*2):
                mergedList = self.mergeTwoLists(lists[i], lists[i+interval])
                lists[i] = mergedList
            interval *= 2
        return lists[0]
                
        
    def mergeTwoLists(self, head1, head2):
        #remember to renew pointer to next
        dummy = pointer = ListNode(None)
        #link while one of the linkedlist is empty
        while head1 and head2:
            if head1.val <= head2.val:
                pointer.next = head1
                head1 = head1.next
            else:
                pointer.next = head2
                head2 = head2.next
            pointer = pointer.next
        #take care of the other one
        while head1:
            pointer.next = head1
            head1 = head1.next
            pointer = pointer.next
        while head2:
            pointer.next = head2
            head2 = head2.next
            pointer = pointer.next
            
        return dummy.next
```

### \572. Subtree of Another Tree

Easy

5926322Add to ListShare

Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of` subRoot` and `false` otherwise.

A subtree of a binary tree `tree` is a tree that consists of a node in `tree` and all of this node's descendants. The tree `tree` could also be considered as a subtree of itself.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/04/28/subtree1-tree.jpg)

```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```

```py
class Solution(object):
    def isSubtree(self, root, subRoot):
        """
        :type root: TreeNode
        :type subRoot: TreeNode
        :rtype: bool
        """
        if not root:
            return False
        if self.isSame(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)

        
    def isSame(self, root, sub):
        if not root and not sub:
            return True
        if not root or not sub:
            return False
        if root.val != sub.val:
            return False
        return self.isSame(root.left, sub.left) and self.isSame(root.right, sub.right)
```

### \98. Validate Binary Search Tree

Medium

11189951Add to ListShare

Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```
Input: root = [2,1,3]
Output: true
```

```py
class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        def dfs(root, low, high):
            if not root:
				# empty node or empty tree
                return True
            
            if low < root.val < high:
				# check if all tree nodes follow BST rule
                return dfs(root.left, low, root.val) and dfs(root.right, root.val, high)
            
            else:
				# early reject when we find violation
                return False 
        
        return dfs(root, -sys.maxsize, sys.maxsize)
```

### \105. Construct Binary Tree from Preorder and Inorder Traversal

Medium

10473281Add to ListShare

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return *the binary tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

```py
def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        """
        first for loop preorder because the parent node will at the front
        second find each parent node in inorder to identify where they are 
        third dfs left and right of each parent node
        """
        #base case
        if not preorder or not inorder:
            return None
        if len(preorder) == 1:
            return TreeNode(preorder[0])
        
        #find the index of root
        root = TreeNode(preorder[0])
        root_index = inorder.index(preorder[0])
        #recursive steps
        root.left = self.buildTree(preorder[1:root_index+1], inorder[:root_index])
        root.right = self.buildTree(preorder[root_index+1:], inorder[root_index+1:])
        return root
```

### \124. Binary Tree Maximum Path Sum

Hard

10884575Add to ListShare

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return *the maximum **path sum** of any **non-empty** path*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

```py
class Solution(object):
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        """
        Greedy approach 
        maxPath = max(left+right+root, max(left+root, right+root))
        globlePath = max(globlePath, maxPath)
        pass(max(left+root, right+root))
        """
        self.globleMax = -sys.maxint
        def dfs(root):
            if not root:
                return 0
            left =max(dfs(root.left), 0)
            right = max(dfs(root.right), 0)
            self.globleMax = max(self.globleMax, left+right+root.val)
            return max(left+root.val, right+root.val)
        dfs(root)
        return self.globleMax
```

### \297. Serialize and Deserialize Binary Tree

Hard

7397275Add to ListShare

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Clarification:** The input/output format is the same as [how LeetCode serializes a binary tree](https://support.leetcode.com/hc/en-us/articles/360011883654-What-does-1-null-2-3-mean-in-binary-tree-representation-). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg)

```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```

```py
def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        """
        USE bfs to traverse the tree and build the str
        [1,2,3,null,null,4,5] = "1/2/3/n/n/4/5"
        each level, append child into res
        """
        if not root:
            return ""
        que = collections.deque()
        que.append(root)
        res = [str(root.val)]
        while que:
            cur = que.popleft()
            if cur.left:
                que.append(cur.left)
                res.append(str(cur.left.val))
            else:
                res.append("#")
            if cur.right:
                que.append(cur.right)
                res.append(str(cur.right.val)) 
            else:
                res.append("#")
        while res[-1] == "#":
            res.pop()
        return ' '.join(res)

    
    
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        """
        same way use BFS
        1/2/3/n/n/4/5 = [1,2,3,null,null,4,5]
        if its a "n", we dont push into queue to avoid 
        """
        if not data:
            return
        arr = data.split(" ")
        que = collections.deque()
        i = 1
        root = TreeNode(int(arr[0]))
        que.append(root)
        n = len(arr)
        while que and i < n:
            for _ in range(len(que)):
                cur = que.popleft()
                
                if i < n and arr[i] != "#":
                    left = TreeNode(int(arr[i]))
                    cur.left = left
                    que.append(left)
                i+=1
                if i < n and arr[i] != "#":
                    right = TreeNode(int(arr[i]))
                    cur.right = right
                    que.append(right)
                i+=1
        return root
```

\973. K Closest Points to Origin

Medium

6238225Add to ListShare

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the **X-Y** plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

The distance between two points on the **X-Y** plane is the Euclidean distance (i.e., `√(x1 - x2)2 + (y1 - y2)2`).

You may return the answer in **any order**. The answer is **guaranteed** to be **unique** (except for the order that it is in).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/03/closestplane1.jpg)

```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation:
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest k = 1 points from the origin, so the answer is just [[-2,2]].
```

```py
 def kClosest(self, points, k):
        """
        :type points: List[List[int]]
        :type k: int
        :rtype: List[List[int]]
        """
        maxHeap = []
        #we have coordinates, needed to transform into distance 
        #use an array to store all the distances, (distance, index) O(n) 
            #use Minheap to maintain only k items
        #Nlogk
        for index, coor in enumerate(points):
            if len(maxHeap) == k:
                if (-math.sqrt((coor[0])**2 + (coor[1])**2)) > maxHeap[0][0]:
                    heapq.heapreplace(maxHeap, (-math.sqrt((coor[0])**2 + (coor[1])**2), index))
            else:
                heapq.heappush(maxHeap, (-math.sqrt((coor[0])**2 + (coor[1])**2), index))
            
        #return heap[0]
        res = []
        #append into res O(n)
        for i,j in maxHeap:
            res.append(points[j])
        return res
        
```

\133. Clone Graph

Medium

64442714Add to ListShare

Given a reference of a node in a **[connected](https://en.wikipedia.org/wiki/Connectivity_(graph_theory)#Connected_graph)** undirected graph.

Return a [**deep copy**](https://en.wikipedia.org/wiki/Object_copying#Deep_copy) (clone) of the graph.

Each node in the graph contains a value (`int`) and a list (`List[Node]`) of its neighbors.

```
class Node {
    public int val;
    public List<Node> neighbors;
}
```

```py
def cloneGraph(self, node):
        """
        :type node: Node
        :rtype: Node
        """
        #use a dfs approach
        #each node we create a new node object and put into hashmap, 
        #for each neibor, add neibor into new node neibor, dfs
        mapping = {}
        def dfs(node):
            if node in mapping:
                return mapping[node]
            new = Node(node.val)
            mapping[node] = new
            for neibor in node.neighbors:
                new.neighbors.append(dfs(neibor))
            return new
        if not node:
            return 
        return dfs(node)
```

\253. Meeting Rooms II

Medium

5863119Add to ListShare

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of conference rooms required*.

 

**Example 1:**

```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: 2
```

```

```



## BQ

### Intro

Hi, my name is Xi Zhang, I am currently a masters student studying at northeastern university majoring Computer science. And I obtained my undergraduate degree in Mathematics and Economics at the university of San Diego. 

During my undergrad degree, like I said I was double majoring math and econ, I was concentrated in Data Science track where I have learned many courses related to machine learning, data analytics and data mining, which involved a lot of coding in python and Rstudio. That's where I discovered my true passion and interest in computer science and started learning data structures and started doing some front and back end projects.

Then I worked at a company called Intelisolv corporation as a software engineer intern. During my internship, I mainly worked on help building the company website and a partial project about mobile app.

Then with a solid cs background, I was successfully admitted to NEU for MSCS. During my masters I've studied courses that are fundamental for CS such as data structures, algorithms and OOD(which ill be TA ). In order to get more experience, I have done several real life projects during my masters program including an android book reader app and a full stack real estate ecommercial website.

My passion and personal goal is to make a positive impact on society with my profession and knowledge, with that being said, I hope I can join amazon to learn deeper cs knowledge and have some industry level experience. 





**Intern**

Lucky to get the job thru a former alumni of undergrad college, who was also the founder of the company

start up, involved in improving company commercial web(back end) + bitcoin trading app(basic help)

since starting up, so no specific project, just call senior/tech lead and see what I could help

**if specific**: dived into React ________

​					iimplemented atomic CSS

​					changeed Loading page into three parts, which will allow user to load much faster



#### **without much information, quick decision, ownership: Senior proj**

#### **tight deadline, out of responsibility, help peer: intern**

#### **miss deadline, challenging, mistake, take risk: OOD**





### /Quick decision without much information/6

LP: bias for action, learn and be curious 

I would like to talk about what happened when I was doing my senior thesis paper in undergrad school.

when I was in undergrad, I was studying econ/data science track. There was a final project towards the end of my degree. The project required us to gather row data from the internet and process then analyze them,  in the end present with some economic insights. at first, I wanted to do a project about the marriage rate change for the past decades and find out what could be the reason. after almost 1/3 of the semester where I already had  proposal done and in the process of mining the data, I found out that I was actually were running short on dataset since most of the datasets found online were either not reliable or didn't have enough infos in it. 

At the moment, I could either stick with it and try to get best out of it, which will work, but quality not as expected. Or I can quickly change to a new topic, will be rushing for the rest of the time and I don't know if it will work. So for this situation I had only little information about future outcome, tough choice. Good thing is that if the new topic doesn't work, I could still change back to the original topic. Which allows me to pursue the best outcome while maintaining risk.

handled by first gather as much information as possible information about a possible new project in just hours and had a emergency meeting with prof to discuss the  -> finally chose to change project because 1. I was committed to give my best on this project, even though there will be tons of work to do if I switch topic, it will come out better and I could have learned more 2. I had only little time to decide, out of instinct I choose some that would naturally give the best result-> wildfire -> did some regression, correlation mtx, test on variable and different type of correlations. ->

**outcome**: quickly react when emergency situation happens, gather most useful info for decision making and try to get best of it, fully commit to what Im doing





### /Made a mistake and how did you fix it. /2

LP: bias for action, deliver result, ownership

same as quick decision, didnt realize the dataset wasn't reliable 



**outcome**: quickly react when emergency situation happens, gather most useful info for decision making and try to get best of it, if commited then put everything that you ever could, responsibility 





### /tight deadline/7

LP: Customer obsession/deliver result/earn trust

 **Bias for action 和 dive deep**



Intern->we were on schedule for a bitcoin trading+price analysis app -> we had skeleton done but wanted to build better UX ->had 4 weeks to finish, only passed a week and were cutted to 2 weeks -> -> needed to earn trust since new company ->  focus on deadline and learn-> instead I spend day and night on that project(bug) and youtube/udemy, many questions wanted to ask senior but due to deadline only schedule one meet to ask unfinishable task-> successfully deployed the program ->

**Outcome** learned a big deal about working under pression, feel and understood the "customers are god". learned that if you are commited to it, then deliver the best result

detail: I could have just do my part, but instead i took some task from senior because he was frustrated my role is to create a price chart with given data, seniors will add more pages/versions into my graph like weeks, month so customers can choose from





### /help peer/2

LP: earn trust, learn and be curious



same as tight deadline and responsibility, but a twist where I could have just do my part, but instead i took some task from senior because he was frustrated my role is to create a price chart with given data, seniors will add more pages/versions into my graph like weeks, month so customers can choose from

**outcome:** good way to learn new stuff, earn trust from teammate, build better working relationship



**Outcome**: learned a big deal about working under pression, feel and understood the "customers are god". learned that if you are commited to it, then deliver the best result. And further sensitized my curiosity for new knowlege after completing challenge









### /out of responsibility/6

LP: ownership, deliever result, learn and be curious

 **Bias for action 和 dive deep**



same as tight deadline, but a twist where I could have just do my part, but instead i took some task from senior because he was frustrated my role is to create a price chart with given data, seniors will add more pages/versions into my graph like weeks, month so customers can choose from





**Outcome**: learned a big deal about working under pression, feel and understood the "customers are god". learned that if you are commited to it, then deliver the best result. And further sensitized my curiosity for new knowlege after completing challenge









### /challenging project/4

LP: deliver result/ownership/quick action/Long term

same as missed deadline















### /The project you did that reflects your ownership

senior project







### /miss ‍‌‍‌‍‌‍‍‌‌‍‌‌‍‌‌‍‍‍‌deadline

LP: customer/ result/ trust

OOD -> three people on a maze game project -> MVC where I was in charge of model part. ->Since the model part is the foundation of the entire project, had to finished it quick. -> first implemented using hashmap and array to generate the random maze and locations and stuff. -> then when everytime was almost wrapped up, after talking to TAs and some other classmates, I found out that there were actually a better way to generate the maze using node and Union Find. Which will reduce time from O(n2) to O(n). -> But since its already only a day or two before the deadline, its risky to change the structure of the entire model, which could possible interfere with the view part thats being done by other teammates -> saved the back up, if couldn't do it , submit the old version, which will pass. -> want to finish with the highest standard, would not feel right if submitted with the O(n2). -> In the end I successfully implemented it -> learned to always keep highest standard, if committed to it, then put everything that we could 

The closest story I can think of was when I was taking this CS course. I was designing a maze-like game using JAVA





### Question to Ask Interviwers

What do you think are the most important qualities for someone to be really successful in this position?
What are the common career paths in this department?
What is the typical day at Amazon?
