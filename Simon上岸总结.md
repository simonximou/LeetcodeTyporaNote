# Simon刷题笔记

## Algos

1. Searching
   - Binary search
   - DFS
   - BFS
2. Ordering
   - Bubble sort
   - Selection Sort
   - Insertion Sort
   - Quick Sort
   - 
3. Structure
4. String
5. Similarity
6. Optimization



## Leetcode

### LinkedList

链表题型合集：https://zhuanlan.zhihu.com/p/43142694

#### LC number:

#### 单链表：

简单：

- [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)
- [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)
- [83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)
- [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)
- [203. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)
- [237. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)
- [876. 链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

中等

- [92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)
- [143. 重排链表](https://leetcode-cn.com/problems/reorder-list/)
- [82. 删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)
- [19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
- [148. 排序链表](https://leetcode-cn.com/problems/sort-list/)
- [86. 分隔链表](https://leetcode-cn.com/problems/partition-list/)
- [61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/)
- [142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)
- [147. 对链表进行插入排序](https://leetcode-cn.com/problems/insertion-sort-list/)
- [138. 复制带随机指针的链表](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)
- [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)
- [328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)
- [707. 设计链表](https://leetcode-cn.com/problems/design-linked-list/)
- [109. 有序链表转换二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/)
- [430. 扁平化多级双向链表](https://leetcode-cn.com/problems/flatten-a-multilevel-doubly-linked-list/)
- [725. 分隔链表](https://leetcode-cn.com/problems/split-linked-list-in-parts/)

困难

- [25. K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

#### 双链表：

简单：

- [21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
- [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

中级

- [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)
- [445. 两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)
- [1669. 合并两个链表](https://leetcode-cn.com/problems/merge-in-between-linked-lists/)

困难

- [23. 合并 K 个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

#### corner cases:

1. head = None
2. length = 1
3. Nonetype found while looping, pointer.next or pointer.next.next is Nonetype
4. duplicated nodes [1,1,1,1,1,1,1]

**143. Reorder List**

You are given the head of a singly linked-list. The list can be represented as:

```
L0 → L1 → … → Ln - 1 → Ln
```

*Reorder the list to be on the following form:*

```
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg)

```
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/09/reorder2-linked-list.jpg)

```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reorderList(self, head):
        #create a dummy head
        dummy = ListNode(0, None)
        dummy.next = head
        
        #First find the middle node
        slow, fast = head, head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        
        #then reverse the second half of the linked list
        prev = None
        while slow:
            temp = slow.next
            slow.next = prev
            prev = slow
            slow = temp 
        
        
        #then connect two parts of the linked list
        #*********Key part of the question******
        head1, head2 = head, prev
        
        
        while head1:
            temp = head1.next
            head1.next = head2
            head1 = head2
            head2 = temp
        return dummy.next
        
       
```



**92. Reverse Linked List II**

Medium

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return *the reversed list*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

```
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def reverseBetween(self, head, left, right):
        #[]
        
        #create a dummy head
        dummy = ListNode(0, None)
        dummy.next = head
        
        #move pointer to first of the reverse part
        cur, leftPrev = head, dummy
        for i in range(left - 1):
            cur = cur.next
            leftPrev = leftPrev.next
        
        #reverse the part
        prev = None
        for j in range(right - left + 1):
            temp = cur.next
            cur.next = prev
            prev = cur
            cur = temp
         
        #connect the disconnected/reversed part with two ends
        leftPrev.next.next = cur 
        leftPrev.next = prev
        
        return dummy.next
    
```

**206. Reverse Linked List**

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        while head:
            temp = head.next
            head.next = prev
            prev = head 
            head = temp
        return prev 
```

**876. Middle of the Linked List**

Given the `head` of a singly linked list, return *the middle node of the linked list*.

If there are two middle nodes, return **the second middle** node.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        #just loop, CORNER Case, think about fast.next.next and avoid NoneTypoe
        if not head:
            return
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if fast == None or fast.next == None:
                break 
        return slow
```

**203. Remove Linked List Elements**

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return *the new head*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

```
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        #just loop thru
        if not head:
            return
        
        #get to first node thats not val
        while head and head.val == val:
            head = head.next
            
        #create dummy head to return 
        dummy = head
        
        #main part of the program, remember CORNER CASES! sO many
        while head and head.next:
            if head.next.val == val:
                head.next = head.next.next
                #check again if next node is == val
                continue
            head = head.next
        return dummy
```

**82. Remove Duplicates from Sorted List II**

Given the `head` of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list*. Return *the linked list **sorted** as well*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return
        #create dummy head 
        dummy = ListNode(0, None)
        dummy.next = head
        prev = dummy
        
        #Loop thru the linked list and if find dup, do another while loop till find the different node
        #Remember whenever theres head.next or head.next.next consider it gets to None
        
        while head and head.next:
            if head.val == head.next.val:
                while head.next and head.val == head.next.val:
                    head = head.next
                prev.next = head.next
                head = head.next
            else:
                head = head.next
                prev = prev.next
        
        
        return dummy.next
```

**19. Remove Nth Node From End of List**

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        #use two pointers, fast go n foward and when fast goes to end, slow is at the removing node
        
        #create dummy head
        dummy = ListNode(0, None)
        dummy.next = head
        slow, fast = dummy, dummy
        for i in range(n):
            fast = fast.next
            
        #in position
        while fast and fast.next:
            slow = slow.next
            fast = fast.next
            
        slow.next = slow.next.next
        
        return dummy.next
```

**86. Partition List**

Medium

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

```
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        """
        classic linked list, one loop done. partition then merge together
        """
        #create two empty head
        if not head:
            return head
        list_s1 = list_s2 = ListNode(0, None)
        list_l1 = list_l2 = ListNode(0, None)
        
        #loop, if partition using the key value put into two linked lists
        while head:
            if head.val < x:
                list_s1.next = head
                list_s1 = list_s1.next
            else:
                list_l1.next = head
                list_l1 = list_l1.next            
            head = head.next
        
        #merge together
        list_s1.next = list_l2.next
        list_l1.next = None
        return list_s2.next
                
```

**61. Rotate List**

Medium

Given the `head` of a linked list, rotate the list to the right by `k` places.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        """
        Linked list. two pointer
        """
        #corner cases
        if k == 0:
            return head
        if not head:
            return 
        if not head.next:
            return head
        
        temp = head
        count = 1
        while temp.next:
            temp = temp.next
            count += 1
        slow = fast = head
        k = k%count
        if k == 0:
            return head
            
        for i in range(k):
            fast = fast.next
        
        while fast.next:
            slow = slow.next
            fast = fast.next
            
        temp = slow.next
        fast.next = head
        slow.next = None
        return temp
```

**725. Split Linked List in Parts**

Medium

Given the `head` of a singly linked list and an integer `k`, split the linked list into `k` consecutive linked list parts.

The length of each part should be as equal as possible: no two parts should have a size differing by more than one. This may lead to some parts being null.

The parts should be in the order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal to parts occurring later.

Return *an array of the* `k` *parts*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/06/13/split1-lc.jpg)

```
Input: head = [1,2,3], k = 5
Output: [[1],[2],[3],[],[]]
Explanation:
The first element output[0] has output[0].val = 1, output[0].next = null.
The last element output[4] is null, but its string representation as a ListNode is [].
```





### **Tree**

<img src="https://camo.githubusercontent.com/05f375896b965b6c1b2ead25c838b5b3385d18a112878d8e9d3dabacaf2cce8f/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303231393139303830393435312e706e67" alt="img" style="zoom:50%;" />



#### 遍历

简单

- [145. 二叉树的后序遍历]
- [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
- [589. N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/)
- [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)
- [590. N 叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)
- 

中等

- [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)
- [103. 二叉树的锯齿形层序遍历](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)
- [107. 二叉树的层序遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)

94. **Binary Tree Inorder Traversal**

Given the `root` of a binary tree, return *the inorder traversal of its nodes' values*.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
Input: root = [1,null,2,3]
Output: [1,3,2]
```

```python
class Solution(object):
    
    def inorderTraversal(self, root):
        # typical DFS
        # base case 1: empty
        if not root:
            return []
        
        # base case 2: no child 
        if not root.left and not root.right:
            return [root.val]
        
        # recursion
        left = self.inorderTraversal(root.left)
        right = self.inorderTraversal(root.right)
        
        # process return result
        res = left + [root.val] + right
        return res
    
    
    
    def inorderTraversal(self, root):
        #we can also use iteration mathod to traverse without using recursion
        #create a stack
        if not root:
            return
        stack = [root]
        res = []
        
        #loop thru the stack and push node val into res[] and add child node while pop
        while(stack):
            node = stack.pop()
            res.append(node.val)
            #push right first because we want to pop left first out
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
        return res
        
```



144. **Binary Tree Preorder Traversal**

Given the `root` of a binary tree, return *the preorder traversal of its nodes' values*.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
Input: root = [1,null,2,3]
Output: [1,2,3]
```

```python
class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root is None:
            return []
        
        stack, output = [root, ], []
        
        while stack:
            root = stack.pop()
            if root is not None:
                output.append(root.val)
            if root.right is not None:
                stack.append(root.right)
            if root.left is not None:
                stack.append(root.left)
        
        return output
    
    def myidea():
        #DFS recursion
        #Base case 1: empty
        if not root:
            return []
        
        #Base case 2: has not child node
        if not root.left and not root.right:
            return [root.val]
        
        #recursion 
        left = self.preorderTraversal(root.left)
        right = self.preorderTraversal(root.right)
        res = [root.val] + left + right
        return res
    
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        #when not using recursion we use iteration method
        if not root:
            return
        #cant put root in stack because its preorder
        stack = []
        res = []
        cur = root
        
        #loop down to left leaf to right leaf and pop
        while cur or stack:
            #first traverse all the way to the end 
            if cur:
                stack.append(cur)
                cur = cur.left
            else:
                cur = stack.pop()
                res.append(cur.val)
                cur = cur.right
        return res
        
        
        
        
        
        
        
```



145. **Binary Tree Postorder Traversal**

Given the `root` of a binary tree, return *the postorder traversal of its nodes' values*.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/28/pre1.jpg)

```
Input: root = [1,null,2,3]
Output: [3,2,1]
```

```python
class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
                # typical DFS
        
        # base case 1: empty
        if not root:
            return []
        
        # base case 2: no child 
        if not root.left and not root.right:
            return [root.val]
        
        # recursion
        left = self.postorderTraversal(root.left)
        right = self.postorderTraversal(root.right)
        
        # process return result
        res = left + right + [root.val]
        return res
```

366. **Find Leaves of Binary Tree**

Given the `root` of a binary tree, collect a tree's nodes as if you were doing this:

- Collect all the leaf nodes.
- Remove all the leaf nodes.
- Repeat until the tree is empty.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/16/remleaves-tree.jpg)

```
Input: root = [1,2,3,4,5]
Output: [[4,5,3],[2],[1]]
Explanation:
[[3,5,4],[2],[1]] and [[3,4,5],[2],[1]] are also considered correct answers since per each level it does not matter the order on which elements are returned.
```

```python
class Solution(object):

    def findLeaves(self, root):
        # we should label the diff left layer
        # and store the left and label by hashmap
        # key is label(layer), value is the list of left
        layer_to_left = defaultdict(list)
    
        # we should use a helper function to process the label(layer)
        def helper(node, layer):
            # base case:left or empty
            if not node:
                return None
            if not node.left and not node.right:
                layer_to_left[layer].append(node.val)
                return layer
            
            # recursion
            left = helper(node.left, layer)
            right = helper(node.right, layer)
            
            # process the result
            layer = max(left, right) + 1
            layer_to_left[layer].append(node.val)
            
            return layer
        
        helper(root, 0)
        return layer_to_left.values()
```



#### 构造

简单

- [108. 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

中等

- [105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
- [106. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
- [114. 二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)
- [889. 根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)
- [1008. 前序遍历构造二叉搜索树](https://leetcode-cn.com/problems/construct-binary-search-tree-from-preorder-traversal/)

困难

- [297. 二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

#### 路径 | 深度 | 翻转

简单

- [104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
- [101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)
- [226. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)
- [543. 二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)
- [257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)
- [110. 平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)
- [617. 合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)
- [100. 相同的树](https://leetcode-cn.com/problems/same-tree/)
- [112. 路径总和](https://leetcode-cn.com/problems/path-sum/)
- [111. 二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

中等

- [236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- [222. 完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)
- [113. 路径总和 II](https://leetcode-cn.com/problems/path-sum-ii/)
- [437. 路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)
- [129. 求根节点到叶节点数字之和](https://leetcode-cn.com/problems/sum-root-to-leaf-numbers/)
- [662. 二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)
- [114. 二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)
- [199. 二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)
- [116. 填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)
- [515. 在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)

困难

- [124. 二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)
- [297. 二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

\104. Maximum Depth of Binary Tree

Easy

6837124Add to ListShare

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        Classic tree depth problem, two solution algos,
        either recursive call or iterative
        """
        
        #recursive:
        """
        setting base case return 0 when it reaches to the leaf node,
        at each leave it will ++ because it is the max of the level + 1
        using less memory but possible stack overflow
        """
        if not root:
            return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
    
    
        #iterative
        """
        using stack to iterate thru the tree
        at after each level save the num of node of next level and when finish with next level do +1
        compare to the recursive method use more memory because using deque
        
        """
        if not root:
            return 0
        stack = deque([root])
        num_of_level = 1
        level = 0
        
        while(stack):
            temp_node = stack.popleft()
            if(temp_node.left):
                stack.append(temp_node.left)
            if(temp_node.right):
                stack.append(temp_node.right)
            num_of_level -= 1
            if(num_of_level == 0):
                num_of_level = len(stack)
                level += 1
            
        return level
        
```

\110. Balanced Binary Tree

Easy

5658311Add to ListShare

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of *every* node differ in height by no more than 1.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        # recursive method:
        # if subtree is unbalanced, then the entire tree is unbalanced
        # recursing till leaf node, check the depth of each subtree
        
        return self.checker(root) != -1
    
    def checker(self, root):
        #base case
        if not root:
            return 0
        
        #recursive left and right
        left = self.checker(root.left)
        if (left == -1):
            return -1
        right = self.checker(root.right)
        if(right == -1):
            return -1
        
        #return -1 if unbalanced, return depth if balanced
        if(abs(left - right) >= 2):
            return -1
        return max(left, right) + 1
    
```

\543. Diameter of Binary Tree

Easy

7686487Add to ListShare

Given the `root` of a binary tree, return *the length of the **diameter** of the tree*.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
```

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    
    # first create a globle max that can be used in each function 
    max_depth = 0
        
        
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        binary tree depth problem
        using recursion 
        max(left, right) + 1 is the max depth
        """
        self.depth(root)
        return self.max_depth
        
    #helper function for recursive solution
    def depth(self, root):
        #base case:
        if not root:
            return 0
        
        #recursive call for each subtree
        left_depth = self.depth(root.left)
        right_depth = self.depth(root.right)
        
        #
        self.max_depth = max(self.max_depth, left_depth + right_depth)
        return max(left_depth, right_depth)+1
        
```

\226. Invert Binary Tree

Easy

8160110Add to ListShare

Given the `root` of a binary tree, invert the tree, and return *its root*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        classic binary tree invert/traverse
        """
        #base case
        if not root:
            return None
        
        #set temp to root.left because will change it later
        temp = root.left
        root.left = self.invertTree(root.right)
        #recursively change each root.left and right
        root.right = self.invertTree(temp)
        
        return root
```

\617. Merge Two Binary Trees

Easy

6455241Add to ListShare

You are given two binary trees `root1` and `root2`.

Imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not. You need to merge the two trees into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of the new tree.

Return *the merged tree*.

**Note:** The merging process must start from the root nodes of both trees.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/05/merge.jpg)

```
Input: root1 = [1,3,2,5], root2 = [2,1,3,null,4,null,7]
Output: [3,4,5,5,4,null,7]
```

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def mergeTrees(self, root1, root2):
        """
        :type root1: TreeNode
        :type root2: TreeNode
        :rtype: TreeNode
        """
        #recursion, no base case because will return None
        if(root1 and root2):
            root = TreeNode(root1.val + root2.val)
            root.left = self.mergeTrees(root1.left, root2.left)
            root.right = self.mergeTrees(root1.right, root2.right)
        else:
            #base case
            return root1 or root2
        
        return root
        
```

\112. Path Sum

Easy

5353779Add to ListShare

Given the `root` of a binary tree and an integer `targetSum`, return `true` if the tree has a **root-to-leaf** path such that adding up all the values along the path equals `targetSum`.

A **leaf** is a node with no children.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum1.jpg)

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
Output: true
Explanation: The root-to-leaf path with the target sum is shown.
```

```PYTHON
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def hasPathSum(self, root, targetSum):
        """
        :type root: TreeNode
        :type targetSum: int
        :rtype: bool
        """
        #classic recursion
        #base case
        if not root:
            return False
        #base case 2: when return true 
        if not root.left and not root.right and root.val == targetSum:
            return True
        
        #recursive steps
        return self.hasPathSum(root.left, targetSum - root.val) or self.hasPathSum(root.right, targetSum - root.val)
```

\437. Path Sum III

Medium

7423359Add to ListShare

Given the `root` of a binary tree and an integer `targetSum`, return *the number of paths where the sum of the values along the path equals* `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg)

```
Input: root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
Output: 3
Explanation: The paths that sum to 8 are shown.
```

```py
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    
    
    def pathSum(self, root, targetSum):
        """
        :type root: TreeNode
        :type targetSum: int
        :rtype: int
        """
        #init
        if not root:
            return 0
        
        #using 
        return self.helper(root, targetSum)+ self.pathSum(root.left, targetSum)+ self.pathSum(root.right, targetSum)
        
        
        
    #define helper ,ethod to treverse the binary tree by recursion
    def helper(self, root, targetSum):
        #base case
        if not root:
            return 0
        res = 0
        if root.val == targetSum:
            res += 1
        
        #recursive steps
        res += self.helper(root.left, targetSum - root.val)
        res += self.helper(root.right, targetSum - root.val)
        
        return res
        
```







#### 二叉搜索树

简单

- [108. 将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

中等

- [98. 验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)
- [96. 不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)
- [95. 不同的二叉搜索树 II](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)
- [173. 二叉搜索树迭代器](https://leetcode-cn.com/problems/binary-search-tree-iterator/)
- [230. 二叉搜索树中第 K 小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)
- [99. 恢复二叉搜索树](https://leetcode-cn.com/problems/recover-binary-search-tree/)

\669. Trim a Binary Search Tree

Medium

4751237Add to ListShare

Given the `root` of a binary search tree and the lowest and highest boundaries as `low` and `high`, trim the tree so that all its elements lies in `[low, high]`. Trimming the tree should **not** change the relative structure of the elements that will remain in the tree (i.e., any node's descendant should remain a descendant). It can be proven that there is a **unique answer**.

Return *the root of the trimmed binary search tree*. Note that the root may change depending on the given bounds.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/09/trim1.jpg)

```
Input: root = [1,0,2], low = 1, high = 2
Output: [1,null,2]
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def trimBST(self, root, low, high):
        """
        :type root: TreeNode
        :type low: int
        :type high: int
        :rtype: TreeNode
        """
        #Use recursion
        #three situations to handle for each case
        #1 root.val < low
        #2 root.val > high
        #3 root.val witin in low and high
        
        if not root:
            return None
        if root.val > high:
            return self.trimBST(root.left, low, high)
        if root.val < low:
            return self.trimBST(root.right, low, high)
        root.left = self.trimBST(root.left, low, high)
        root.right = self.trimBST(root.right, low, high)
        
        return root
    #there is a iterative way to solve but too complicated
```

\230. Kth Smallest Element in a BST

Medium

7038128Add to ListShare

Given the `root` of a binary search tree, and an integer `k`, return *the* `kth` *smallest value (**1-indexed**) of all the values of the nodes in the tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg)

```
Input: root = [3,1,4,null,2], k = 1
Output: 1
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        #use recursion, inorder traversal
        #BST in order traversal will result a sorted number list
        #we can use an array to store all the value or use count and val to represent res
        res = []
        self.traversal(root, res)
        return res[k-1]
        
    #tree traversal
    def traversal(self, root, res):
        if not root:
            return 
        self.traversal(root.left, res)
        res.append(root.val)
        self.traversal(root.right, res)
        
```

\538. Convert BST to Greater Tree

Medium

4262159Add to ListShare

Given the `root` of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus the sum of all keys greater than the original key in BST.

As a reminder, a *binary search tree* is a tree that satisfies these constraints:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/05/02/tree.png)

```
Input: root = [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
Output: [30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
```

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.count = 0
    
    def convertBST(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        self.helper(root)
        return root
        
        
    #helper recursion function that traverse BST from right to left
    def helper(self, root):
        if not root:
            return
        self.helper(root.right)
        self.count += root.val
        root.val = self.count
        self.helper(root.left)
```

\235. Lowest Common Ancestor of a Binary Search Tree

Easy

5653183Add to ListShare

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png)

```
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        #recursive solution:
        #two cases, when rootval is greater or smaller than both cases:
         #LCA must be on the over side of the tree
        #when twoo nodes are on the opposite side,
         #LCA is root
        if p.val > root.val and q.val > root.val:    
            return self.lowestCommonAncestor(root.right, p, q)
        # If both p and q are lesser than parent
        elif p.val < root.val and q.val < root.val:    
            return self.lowestCommonAncestor(root.left, p, q)
        # We have found the split point, i.e. the LCA node.
        else:
            return root
        
        
        #Iterative solution:
        #silimar to recursive 
        # while root:
        #     if root.val > p.val and root.val > q.val:
        #         root = root.left
        #     elif root.val < p.val and root.val < q.val:
        #         root = root.right
        #     else:
        #         return root
```

**\*236. Lowest Common Ancestor of a Binary Tree***

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

```python
class Solution(object): 
    def lowestCommonAncestor(self, root, p, q):
        """
        DFS, recursion on the tree, if found both node, return root, else return the the found node since the other one must be down in the same brunch
        """
        # if itself is what we are looking for, return
        if root == p or root == q:
            return root
        
        # do left and right recursion
        left = right = None
        if root.left:
            left = self.lowestCommonAncestor(root.left, p, q)
        if root.right:
            right = self.lowestCommonAncestor(root.right, p, q)
            
        # if noth children has target, return root, otherwise return the one that has target since the other one must down the same tree
        if left and right:
            return root
        else:
            return left or right 
```

\108. Convert Sorted Array to Binary Search Tree

Easy

6338357Add to ListShare

Given an integer array `nums` where the elements are sorted in **ascending order**, convert *it to a **height-balanced** binary search tree*.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

```
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        #using recursion to build BST
        
        if len(nums) == 0:
            return
        node = TreeNode()
        mid = len(nums)
        node.val = nums[mid//2]
        node.left = self.sortedArrayToBST(nums[:mid//2])
        node.right = self.sortedArrayToBST(nums[mid//2+1:])
        return node
```

\109. Convert Sorted List to Binary Search Tree

Medium

4560114Add to ListShare

Given the `head` of a singly linked list where elements are **sorted in ascending order**, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/linked.jpg)

```
Input: head = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: One possible answer is [0,-3,9,-10,null,5], which represents the shown height balanced BST.
```

```py
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[TreeNode]
        """
        #base case: if head is the only node then it is a leaf node 
        if not head:
            return
        if not head.next:
            return TreeNode(head.val)
        
        #find mid of the list, so we can pass to the next level
        #prev use one node before slow to cut off the left part 
        fast, slow , prev = head, head, None
        while fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next
            
        #slow is root we find
        node = TreeNode(slow.val)
        #node.right 
        right_head = slow.next
        
        #cut off node.left
        if prev:
            prev.next = None
        
        #recursive call to find node.left and right 
        node.left = self.sortedListToBST(head)
        node.right = self.sortedListToBST(right_head)
        return node
```

\653. Two Sum IV - Input is a BST

Easy

3648203Add to ListShare

Given the `root` of a Binary Search Tree and a target number `k`, return *`true` if there exist two elements in the BST such that their sum is equal to the given target*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/21/sum_tree_1.jpg)

```
Input: root = [5,3,6,2,4,null,7], k = 9
Output: true
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def findTarget(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: bool
        """
        #1. hashset method 2. sorted array method
        #1. use hash set to check in each step if the compliment is in the set 
        #2. use preorder traversal to get sorted array and go from there
        hashSet = set()
        return self.dfs(root, hashSet, k)
    
    def dfs(self, root, hashSet, k):
        #base case
        if not root:
            return False
        if k - root.val in hashSet:
            return True
        
        #add to set
        hashSet.add(root.val)
        return self.dfs(root.left, hashSet, k) or self.dfs(root.right, hashSet, k)
```



#### 字典树

简单

- [720. 词典中最长的单词](https://leetcode-cn.com/problems/longest-word-in-dictionary/)

中等

- [208. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)
- [692. 前 K 个高频单词](https://leetcode-cn.com/problems/top-k-frequent-words/)
- [421. 数组中两个数的最大异或值](https://leetcode-cn.com/problems/maximum-xor-of-two-numbers-in-an-array/)

困难

- [212. 单词搜索 II](https://leetcode-cn.com/problems/word-search-ii/)

#### 线段树

中等

- [1353. 最多可以参加的会议数目](https://leetcode-cn.com/problems/maximum-number-of-events-that-can-be-attended/)
- [307. 区域和检索 - 数组可修改](https://leetcode-cn.com/problems/range-sum-query-mutable/)

困难

- [315. 计算右侧小于当前元素的个数](https://leetcode-cn.com/problems/count-of-smaller-numbers-after-self/)
- [493. 翻转对](https://leetcode-cn.com/problems/reverse-pairs/)
- [218. 天际线问题](https://leetcode-cn.com/problems/the-skyline-problem/)
- [715. Range 模块](https://leetcode-cn.com/problems/range-module/)
- [850. 矩形面积 II](https://leetcode-cn.com/problems/rectangle-area-ii/)
- [1157. 子数组中占绝大多数的元素](https://leetcode-cn.com/problems/online-majority-element-in-subarray/)
- [699. 掉落的方块](https://leetcode-cn.com/problems/falling-squares/)
- [327. 区间和的个数](https://leetcode-cn.com/problems/count-of-range-sum/)

### DFS

**695. Max Area of Island**

You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The **area** of an island is the number of cells with a value `1` in the island.

Return *the maximum **area** of an island in* `grid`. If there is no island, return `0`.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/05/01/maxarea1-grid.jpg)

```
Input: grid = [[0,0,1,0,0,0,0,1,0,0,0,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,1,1,0,1,0,0,0,0,0,0,0,0],[0,1,0,0,1,1,0,0,1,0,1,0,0],[0,1,0,0,1,1,0,0,1,1,1,0,0],[0,0,0,0,0,0,0,0,0,0,1,0,0],[0,0,0,0,0,0,0,1,1,1,0,0,0],[0,0,0,0,0,0,0,1,1,0,0,0,0]]
Output: 6
Explanation: The answer is not 11, because the island must be connected 4-directionally.
```

```python
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        Classic DFS
        loop through all the elements in the matrix, if meet a "1" call dfs                   function,and find all the 1s that connects it and return a area to the               variable result. Every time find a new island just compare the island area
         """
        #dfs
        def helper(matrix, area, row, col):
            area += 1
            matrix[row][col] = 0
            for a, b in ([1,0],[0,1],[-1,0],[0,-1]):
                if 0 <= row+a < len_row and 0 <= col+b < len_col and matrix[row+a][col+b] == 1:
                    area = helper(matrix, area, row+a, col+b)
            return area
        
        
        #loop through the matrix
        len_row, len_col = len(grid), len(grid[0])
        res = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1:
                    area = 0
                    res = max(res, helper(grid, area, i, j))
        return res
```

**200. Number of Islands**

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

```python
class Solution(object):
    def numIslands(self, grid):
        """
        DFS similar to 695. loop through all the elements and when meet "1" call dfs function and turn all the connected 1s into 0s 
        """
        # define dfs functions
        def helper(grid, row, col):
            grid[row][col] = "0"
            for a,b in ([1,0],[0,1],[-1,0],[0,-1]):
                if 0<=row+a<len_row and 0<=col+b<len_col and grid[row+a][col+b] == "1":
                    helper(grid, row+a, col+b)
            
        
        len_row, len_col = len(grid), len(grid[0])
        res = 0
        for i in range(len_row):
            for j in range(len_col):
                if grid[i][j] == "1":
                    res += 1
                    helper(grid, i, j)
        return res 
```



**130. Surrounded Regions**

Given an `m x n` matrix `board` containing `'X'` and `'O'`, *capture all regions that are 4-directionally surrounded by* `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```

```python
class Solution(object):
    def solve(self, board):
        """
        DFS solution: loop through the outer part of an matrix that connects with the boundary, any island connects to it are not surrounded by water and others are. 
        """
        # loop through the outer do dfs on every "O"
        for i in [0, len(board) - 1]:
            for j in range(len(board[0])):
                if board[i][j] == "O":
                    self.dfs(board, i, j)
        for i in range(len(board)):
            for j in [0, len(board[0]) - 1]:
                if board[i][j] == "O":
                    self.dfs(board, i, j)
        
        # loop through the matrix and change all the rest to "X" and the marked into "O"
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == "O":
                    board[i][j] = "X"
                elif board[i][j] == "*":
                    board[i][j] = "O"
        
        
        #dfs
    def dfs(self, board, row, col):
        board[row][col] = "*"
        for a,b in ([1,0],[0,1],[-1,0],[0,-1]):
            if 0 <= row+a < len(board) and 0 <= col+b < len(board[0]) and board[row+a][col+b] == "O":
                self.dfs(board, row+a, col+b)
```

- [ ] **417. Pacific Atlantic Water Flow**

There is an `m x n` rectangular island that borders both the **Pacific Ocean** and **Atlantic Ocean**. The **Pacific Ocean** touches the island's left and top edges, and the **Atlantic Ocean** touches the island's right and bottom edges.

The island is partitioned into a grid of square cells. You are given an `m x n` integer matrix `heights` where `heights[r][c]` represents the **height above sea level** of the cell at coordinate `(r, c)`.

The island receives a lot of rain, and the rain water can flow to neighboring cells directly north, south, east, and west if the neighboring cell's height is **less than or equal to** the current cell's height. Water can flow from any cell adjacent to an ocean into the ocean.

Return *a **2D list** of grid coordinates* `result` *where* `result[i] = [ri, ci]` *denotes that rain water can flow from cell* `(ri, ci)` *to **both** the Pacific and Atlantic oceans*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/06/08/waterflow-grid.jpg)

```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

```python
class Solution(object):
    def pacificAtlantic(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[List[int]]
        """
        if not matrix: return []
        self.directions = [(1,0),(-1,0),(0,1),(0,-1)]
        m = len(matrix)
        n = len(matrix[0])
        p_visited = [[False for _ in range(n)] for _ in range(m)]
        
        a_visited = [[False for _ in range(n)] for _ in range(m)]
        result = []
        
        for i in range(m):
            # p_visited[i][0] = True
            # a_visited[i][n-1] = True
            self.dfs(matrix, i, 0, p_visited, m, n)
            self.dfs(matrix, i, n-1, a_visited, m, n)
        for j in range(n):
            # p_visited[0][j] = True
            # a_visited[m-1][j] = True
            self.dfs(matrix, 0, j, p_visited, m, n)
            self.dfs(matrix, m-1, j, a_visited, m, n)
            
        for i in range(m):
            for j in range(n):
                if p_visited[i][j] and a_visited[i][j]:
                    result.append([i,j])
        return result
                
                
    def dfs(self, matrix, i, j, visited, m, n):
        # when dfs called, meaning its caller already verified this point 
        visited[i][j] = True
        for dir in self.directions:
            x, y = i + dir[0], j + dir[1]
            if x < 0 or x >= m or y < 0 or y >= n or visited[x][y] or matrix[x][y] < matrix[i][j]:
                continue
            self.dfs(matrix, x, y, visited, m, n)
```





### Backtracking

![](https://camo.githubusercontent.com/3bcac8ab20d3edb4151fb58a0b7c09bcf33b70bfd4a422bd74215429dd697fd6/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303231393139323035303636362e706e67)

------



#### 回溯法解决的问题

回溯法，一般可以解决如下几种问题：

- 组合问题：N个数里面按一定规则找出k个数的集合
- 切割问题：一个字符串按一定规则有几种切割方式
- 子集问题：一个N个数的集合里有多少符合条件的子集
- 排列问题：N个数按一定规则全排列，有几种排列方式
- 棋盘问题：N皇后，解数独等等

**相信大家看着这些之后会发现，每个问题，都不简单！**

另外，会有一些同学可能分不清什么是组合，什么是排列？

**组合是不强调元素顺序的，排列是强调元素顺序**。

例如：{1, 2} 和 {2, 1} 在组合上，就是一个集合，因为不强调顺序，而要是排列的话，{1, 2} 和 {2, 1} 就是两个集合了。

记住组合无序，排列有序，就可以了。

------



#### 如何理解回溯法

**回溯法解决的问题都可以抽象为树形结构**，是的，我指的是所有回溯法的问题都可以抽象为树形结构！

因为回溯法解决的都是在集合中递归查找子集，**集合的大小就构成了树的宽度，递归的深度，都构成的树的深度**。

递归就要有终止条件，所以必然是一棵高度有限的树（N叉树）。

这块可能初学者还不太理解，后面的回溯算法解决的所有题目中，我都会强调这一点并画图举相应的例子，现在有一个印象就行。

------



#### 回溯法模板

- 回溯函数模板返回值以及参数

在回溯算法中，我的习惯是函数起名字为backtracking，这个起名大家随意。

回溯算法中函数返回值一般为void。

再来看一下参数，因为回溯算法需要的参数可不像二叉树递归的时候那么容易一次性确定下来，所以一般是先写逻辑，然后需要什么参数，就填什么参数。

但后面的回溯题目的讲解中，为了方便大家理解，我在一开始就帮大家把参数确定下来。

回溯函数伪代码如下：

```
void backtracking(参数)
```

- 回溯函数终止条件

既然是树形结构，那么我们在讲解[二叉树的递归](https://programmercarl.com/二叉树的递归遍历.html)的时候，就知道遍历树形结构一定要有终止条件。

所以回溯也有要终止条件。

什么时候达到了终止条件，树中就可以看出，一般来说搜到叶子节点了，也就找到了满足条件的一条答案，把这个答案存放起来，并结束本层递归。

所以回溯函数终止条件伪代码如下：

```
if (终止条件) {
    存放结果;
    return;
}
```

- 回溯搜索的遍历过程

在上面我们提到了，回溯法一般是在集合中递归搜索，集合的大小构成了树的宽度，递归的深度构成的树的深度。

如图：

[![回溯算法理论基础](https://camo.githubusercontent.com/f65ca647f31913496481cd1aff144040bd7ee4f6bc30accd370bc78b4b265d13/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303133303137333633313137342e706e67)](https://camo.githubusercontent.com/f65ca647f31913496481cd1aff144040bd7ee4f6bc30accd370bc78b4b265d13/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303133303137333633313137342e706e67)

注意图中，我特意举例集合大小和孩子的数量是相等的！

回溯函数遍历过程伪代码如下：

```
for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
    处理节点;
    backtracking(路径，选择列表); // 递归
    回溯，撤销处理结果
}
```

for循环就是遍历集合区间，可以理解一个节点有多少个孩子，这个for循环就执行多少次。

backtracking这里自己调用自己，实现递归。

大家可以从图中看出**for循环可以理解是横向遍历，backtracking（递归）就是纵向遍历**，这样就把这棵树全遍历完了，一般来说，搜索叶子节点就是找的其中一个结果了。

分析完过程，回溯算法模板框架如下：

模板：

```python
def backtrack(candidate):
    if find_solution(candidate):
        output(candidate)
        return
    
    # iterate all possible candidates.
    for next_candidate in list_of_candidates:
        if is_valid(next_candidate):
            # try this partial candidate solution
            place(next_candidate)
            # given the candidate, explore further.
            backtrack(next_candidate)
            # backtrack
            remove(next_candidate)
```

------



77. **Combinations**

Given two integers `n` and `k`, return *all possible combinations of* `k` *numbers out of the range* `[1, n]`.

You may return the answer in **any order**.

**Example 1:**

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```python
class Solution:
     	"""
        classic backtracking problem. Listing all the combinations. Thinking it as a tree traversal.
        """
    def combine(self, n: int, k: int) -> List[List[int]]:
        res = []
        path = []
        
        def backtracking(n, k, next_index):
            if len(path) == k:
                res.append(path.copy())
                return
            for i in range(next_index, n+1):
                path.append(i)
                backtracking(n,k,i+1)
                path.pop()
            
        backtracking(n,k,1)
        return res
    ### Remember python does not create new object when appending a list, if you change the original list, the list in res will be changed too.
```

**216. Combination Sum III**

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

- Only numbers `1` through `9` are used.
- Each number is used **at most once**.

Return *a list of all possible valid combinations*. The list must not contain the same combination twice, and the combinations may be returned in any order.

 

**Example 1:**

```
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        res = []
        
        def backtrack(num, path, target):
            if len(path) == k:
                if target == 0:
                    res.append(path.copy())
                return
            
            for i in range(num + 1, 10):
                if i <= target:
                    path.append(i)
                    backtrack(i, path, target - i)
                    path.pop()
        
        backtrack(0, [], n)
        return res
```

**17. Letter Combinations of a Phone Number**

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

 

**Example 1:**

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        """
        Backtracking, imaging a tree to leaf node
        """
        if not digits:
            return 
        mapping = {'2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl', 
                   '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'}
        res = []
        lenth = len(digits)
        
        def backtracking(start_index, path, digits):
            if len(path) == lenth:
                res.append("".join(path))
                return
            letters = mapping[digits[start_index]]
            for letter in letters:
                path.append(letter)
                backtracking(start_index+1, path, digits)
                path.pop()
                
        
        backtracking(0,[],digits)
        return res
```



**39. Combination Sum**

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

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []
        candidates = sorted(candidates)
        lenth = len(candidates)
        def backtracking(remaining, path, start_index):
            if remaining == 0:
                res.append(path.copy())
                return
            
            for i in range(start_index, lenth):
                if candidates[i] > remaining:
                    break
                backtracking(remaining - candidates[i], path + [candidates[i]], i)
                              
        backtracking(target, [], 0)
        return res
```



**40. Combination Sum II**

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

```python
class Solution:
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



**131. Palindrome Partitioning**

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

 

**Example 1:**

```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

```python
class Solution(object):
    def partition(self, s):
        res = []
        length = len(s)
        
        def backtracking(path, start_index):
            if start_index == length:
                res.append(path[:])
                return
            
            for i in range(start_index, length):
                temp = s[start_index:i + 1]
                if not temp == temp[::-1]:
                    continue
                else:
                    path.append(temp)
                backtracking(path, i + 1)
                path.pop()
        backtracking([], 0)
        return res
        
```



**93. Restore IP Addresses**

A **valid IP address** consists of exactly four integers separated by single dots. Each integer is between `0` and `255` (**inclusive**) and cannot have leading zeros.

- For example, `"0.1.2.201"` and `"192.168.1.1"` are **valid** IP addresses, but `"0.011.255.245"`, `"192.168.1.312"` and `"192.168@1.1"` are **invalid** IP addresses.

Given a string `s` containing only digits, return *all possible valid IP addresses that can be formed by inserting dots into* `s`. You are **not** allowed to reorder or remove any digits in `s`. You may return the valid IP addresses in **any** order.

 

**Example 1:**

```
Input: s = "25525511135"
Output: ["255.255.11.135","255.255.111.35"]
```

```

```



**78. Subsets**

Given an integer array `nums` of **unique** elements, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = [[]]
        
        def backtracking(path, start_index):
            if start_index == len(nums):
                return
            for i in range(start_index, len(nums)):
                path.append(nums[i])
                res.append(path.copy())
                backtracking(path, i+1)
                path.pop()
                
        backtracking([], 0)
        return res
```

**90. Subsets II**

Given an integer array `nums` that may contain duplicates, return *all possible subsets (the power set)*.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

 

**Example 1:**

```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums = sorted(nums)
        def backtracking(path, start_index):
            res.append(path.copy())
            if start_index == len(nums):
                return
            for i in range(start_index, len(nums)):
                if i > start_index and nums[i] == nums[i - 1]:
                        continue
                path.append(nums[i])
                backtracking(path, i+1)
                path.pop()
                
        backtracking([], 0)
        return res
```

**\491. Increasing Subsequences**

Given an integer array `nums`, return all the different possible increasing subsequences of the given array with **at least two elements**. You may return the answer in **any order**.

The given array may contain duplicates, and two equal integers should also be considered a special case of increasing sequence.

**Example 1:**

```
Input: nums = [4,6,7,7]
Output: [[4,6],[4,6,7],[4,6,7,7],[4,7],[4,7,7],[6,7],[6,7,7],[7,7]]
```

```

```

**\46. Permutations**

Given an array `nums` of distinct integers, return *all the possible permutations*. You can return the answer in **any order**.

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        res = []
        
        def backtracking(path, used):
            if len(path) == len(nums):
                res.append(path.copy())
                return
            for i in nums:
                if i not in used:
                    path.append(i)
                    used.add(i)
                    backtracking(path, used)
                    used.remove(i)
                    path.pop()
            
        backtracking([], set())
        return res
```



### BFS

**200. Number of Islands**

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

```python
from collections import deque
class Solution(object):
    def numIslands(self, grid):
        if not grid:
            return 0
        res = 0
        check = [[False for _ in range(len(grid[0]))] for _ in range(len(grid))]
        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == "1" and check[row][col] == False:
                    res +=1 
                    self.bfs(check, row, col, grid)
        return res
        
        
    def bfs(self, check, row, col, grid):
        queue = deque([(row, col)])
        while queue:
            row, col = queue.popleft()
            if 0 <= row < len(grid) and 0 <= col < len(grid[0]) and grid[row][col] == "1" and check[row][col] == False:
                check[row][col] = True
                queue.append([(row + 1, col), (row, col + 1), (row - 1, col), (row, col - 1)])
```

**130. Surrounded Regions**

Given an `m x n` matrix `board` containing `'X'` and `'O'`, *capture all regions that are 4-directionally surrounded by* `'X'`.

A region is **captured** by flipping all `'O'`s into `'X'`s in that surrounded region.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/xogrid.jpg)

```
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Surrounded regions should not be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```

```python
class Solution(object):
    def solve(self, board):
        if not board:
            return [[]]
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == "O":
                    self.bfs(board, i, j)
        return board
    def bfs(self, board, i, j):
        print 1
        if board[i + 1][j] == "O":
            board[i][j] = "X"
            self.bfs(board, i+1, j)
        if board[i - 1][j] == "O":
            board[i][j] = "X"
            self.bfs(board, i-1, j)
        if board[i][j] == "O":
            board[i][j+1] = "X"
            self.bfs(board, i, j+1)
        if board[i][j-1] == "O":
            board[i][j] = "X"
            self.bfs(board, i, j-1)
```



### Greedy

#### 什么是贪心

**贪心的本质是选择每一阶段的局部最优，从而达到全局最优**。

这么说有点抽象，来举一个例子：

例如，有一堆钞票，你可以拿走十张，如果想达到最大的金额，你要怎么拿？

指定每次拿最大的，最终结果就是拿走最大数额的钱。

每次拿最大的就是局部最优，最后拿走最大数额的钱就是推出全局最优。

#### 贪心一般解题步骤

贪心算法一般分为如下四步：

- 将问题分解为若干个子问题
- 找出适合的贪心策略
- 求解每一个子问题的最优解
- 将局部最优解堆叠成全局最优解

**455. Assign Cookies**

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.

Each child `i` has a greed factor `g[i]`, which is the minimum size of a cookie that the child will be content with; and each cookie `j` has a size `s[j]`. If `s[j] >= g[i]`, we can assign the cookie `j` to the child `i`, and the child `i` will be content. Your goal is to maximize the number of your content children and output the maximum number.

**Example 1:**

```
Input: g = [1,2,3], s = [1,1]
Output: 1
Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
```

```python
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        """
        Greedy, not too sure about the point of this question
        """
        g = sorted(g)
        s = sorted(s)
        res, pointer = 0,0
        for i in range(len(s)):
            if(pointer < len(g) and s[i] >= g[pointer]):
                res += 1
                pointer += 1
        return res
                
```



**376. Wiggle Subsequence**

A **wiggle sequence** is a sequence where the differences between successive numbers strictly alternate between positive and negative. The first difference (if one exists) may be either positive or negative. A sequence with one element and a sequence with two non-equal elements are trivially wiggle sequences.

- For example, `[1, 7, 4, 9, 2, 5]` is a **wiggle sequence** because the differences `(6, -3, 5, -7, 3)` alternate between positive and negative.
- In contrast, `[1, 4, 7, 2, 5]` and `[1, 7, 4, 5, 5]` are not wiggle sequences. The first is not because its first two differences are positive, and the second is not because its last difference is zero.

A **subsequence** is obtained by deleting some elements (possibly zero) from the original sequence, leaving the remaining elements in their original order.

Given an integer array `nums`, return *the length of the longest **wiggle subsequence** of* `nums`.

 

**Example 1:**

```
Input: nums = [1,7,4,9,2,5]
Output: 6
Explanation: The entire sequence is a wiggle sequence with differences (6, -3, 5, -7, 3).
```

**Example 2:**

```
Input: nums = [1,17,5,10,13,15,10,5,16,8]
Output: 7
Explanation: There are several subsequences that achieve this length.
One is [1, 17, 10, 13, 10, 16, 8] with differences (16, -7, 3, -3, 6, -8).
```

```python
class Solution:
    def wiggleMaxLength(self, nums: List[int]) -> int:
    
        res, cur_diff, pre_diff = 1, 0, 0
        for i in range(len(nums) - 1):
            cur_diff = nums[i+1] - nums[i]
            if cur_diff * pre_diff <= 0 and cur_diff != 0:
                res += 1
                pre_diff = cur_diff
        return res
            
        
```

**53. Maximum Subarray**

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

A **subarray** is a **contiguous** part of an array.

 

**Example 1:**

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        """
        暴力n2， 局部可以如果count《 0就从下一个开始因为加上前面也会拉低sum
        """
        res, count = -99999, 0
        for i in nums:
            count += i
            if count > res: 
                res = count
            if count < 0:
                count = 0
                continue
        return res
            
                
            
```

**122. Best Time to Buy and Sell Stock II**

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return *the **maximum** profit you can achieve*.

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Total profit is 4 + 3 = 7.
```

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        """
        记住局部最优解就是全局最优解
        """
        res = 0
        for i in range(len(prices) - 1):
            temp = prices[i + 1] - prices[i]
            if temp > 0:
                res += temp
        return res
```

**55. Jump Game**

You are given an integer array `nums`. You are initially positioned at the array's **first index**, and each element in the array represents your maximum jump length at that position.

Return `true` *if you can reach the last index, or* `false` *otherwise*.

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        if len(nums) <= 1:
            return 1
        covered, i = 0, 0
        #  python不支持动态修改for循环中变量,使用while循环
        while i <= covered:
            covered = max(covered, i + nums[i])
            if covered >= len(nums) - 1:
                return True
            i += 1
        return False
```

\45. Jump Game II

Given an array of non-negative integers `nums`, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

You can assume that you can always reach the last index.

**Example 1:**

```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2. Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

```python
class Solution:
    def jump(self, nums: List[int]) -> int:
        """
        think this question as BFS where you add nodes into Queue for each step and find the largest step. then add all the possible next step into queue and find the largest
        """
        jump, max_jump, last_position, i = 0, 0, 0, 0
        while last_position < len(nums) - 1:
            max_jump = max(max_jump, i + nums[i])
            if last_position == i:
                last_position = max_jump
                jump += 1
            i += 1
        return jump 
            
```









### Sorting

#### Bubble sort:

- distribute the original input array into many different "buckets" and then apply sorting to each bucket then put them back together.

- imagine as bubble going up a pipe(largest will go up first and so on)

- Time: O(n^2)  Space: O(n)

  ```java
  package com.ys.sort;
  
  public class BubbleSort {
  	public static int[] sort(int[] array) {
  		// 这里for循环表示总共需要比较多少轮
  		for (int i = 1; i < array.length-1; i++) {
  			// 设定一个标记，若为true，则表示此次循环没有进行交换，也就是待排序列已经有序，排序已经完成。
  			boolean flag = true;
  			// 这里for循环表示每轮比较参与的元素下标
  			// 对当前无序区间array[0......length-i]进行排序
  			// j的范围很关键，这个范围是在逐步缩小的,因为每轮比较都会将最大的放在右边
  			for (int j = 0; j < array.length - i; j++) {
  				if (array[j] > array[j + 1]) {
  					int temp = array[j];
  					array[j] = array[j + 1];
  					array[j + 1] = temp;
  					flag = false;
  				}
  			}
  			if (flag) {
  				break;
  			}
  			// 第 i轮排序的结果为
  			System.out.print("第" + i + "轮排序后的结果为:");
  			display(array);
  
  		}
  		return array;
  
  	}
  }
  ```

  

#### Selection Sort:

- loop through the input array and exchange the ith element with smallest 

- Time: O(n^2)  Space: O(n) (but space twice as big as bubble)

  ```java
  package com.ys.sort;
  
  public class ChoiceSort {
  	public static int[] sort(int[] array) {
  		// 总共要经过N-1轮比较
  		for (int i = 0; i < array.length - 1; i++) {
  			int min = i;
  			// 每轮需要比较的次数
  			for (int j = i + 1; j < array.length; j++) {
  				if (array[j] < array[min]) {
  					min = j;// 记录目前能找到的最小值元素的下标
  				}
  			}
  			// 将找到的最小值和i位置所在的值进行交换
  			if (i != min) {
  				int temp = array[i];
  				array[i] = array[min];
  				array[min] = temp;
  			}
  			// 第 i轮排序的结果为
  			System.out.print("第" + (i + 1) + "轮排序后的结果为:");
  			display(array);
  		}
  		return array;
  	}
  ```

  

#### Insertion Sort:

- have pointers moving right of the array. Left would be sorted and right are unsorted. While moving right, if the element on the right of the pointer is smaller than the element on the left of the pointer(largest sorted element), start moving it to the left. If it is still smaller than the second largest, move largest right and keep moving left until find its space.
- Time: O(n^2)  Space: O(n)

```java
public class InsertSort {
	public static int[] sort(int[] array) {
		int j;
		// 从下标为1的元素开始选择合适的位置插入，因为下标为0的只有一个元素
，默认是有序的
		for (int i = 1; i < array.length; i++) {
			int tmp = array[i];// 记录要插入的数据
			j = i;
			while (j > 0 && tmp < array[j - 1]) {// 从已经排序的序列最右边的开
始比较，找到比其小的数
				array[j] = array[j - 1];// 向后挪动
				j--;
			}
			array[j] = tmp;// 存在比其小的数，插入
		}
		return array;
	}

```



## Interview related 

### Project review Interview 

这类面试就是通过你聊过去参与过的一个project来看看你的system design skill, communication skill，team work和time management。
这类面试的问题提问方向可以根据project timeline大概分为三类：

project前

project中

project后

大眼一看可能觉得很废话，我们可以每一个都分开仔细看看。
**project前**
project前会有很多准备工作。首先要了解为什么会有这个project。project的目标是什么。这里可能是对旧的系统的scale做个提升。也可以是新的feature。这里我们可以套用system design interview时经常用的框架（可以参考一下table）。这个design的时候有什么tradeoff，有没有想过其他的solution。为啥最后选择了你们最终选择的design。这里最好准备你们最终的system design graph列好每一个service和component，标注每一部分都是干嘛的。如果是对旧系统做个提升的话，最好也画一下旧系统的graph。
**Functional requirement**

api
database and schema

**None Functional requirement (老生常谈）**

performance
scale
resilientcy
consistency
cost
length of time given to the project

**project中**
遇到了什么困难？如何解决？如果牵扯到其他组，如何和其他组合作？和别的组有conflict，怎么解决的? 最后达成了什么共识？做了什么test? 有没有做scalability test？有没有setup monitor？有没有在规定时间内完成计划？有没有超额完成任务？-baidu 1point3acres

**project后**
你从project里面学到了什么？怎么确保完成了project？有没有符合最初设定的QPS？怎么monitor error?你在project中是怎么解决scale的问题的？如果你们系统使用人数迅速增长，哪一个部分会是比较容易出现问题的？针对出现的这些问题，有什么解决方案？如果你对你这个project做个retro，你觉得你想improve什么地方？
