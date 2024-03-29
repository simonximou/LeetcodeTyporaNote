# Simon刷题笔记



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

#### Intro

1. ⼆叉树算法设计的总路线：把当前节点要做的事做好，其他的交给递归 框架，不⽤当前节点操⼼。

2. 如果当前节点会对下⾯的⼦节点有整体影响，可以通过辅助函数增⻓参 数列表，借助参数传递信息。 

3. 在⼆叉树框架之上，扩展出⼀套 BST 遍历框架：

   ```java
   oid BST(TreeNode root, int target) {
       if (root.val == target)
       	// 找到⽬标，做点什么
       if (root.val < target)
       	BST(root.right, target);
       if (root.val > target)
       	BST(root.left, target);
   }
   
   ```

   

#### 遍历

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

- https://leetcode-cn.com/problems/recover-binary-search-tree/)

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

530. Minimum Absolute Difference in BST

Easy

2041118Add to ListShare

Given the `root` of a Binary Search Tree (BST), return *the minimum absolute difference between the values of any two different nodes in the tree*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/05/bst1.jpg)

```
Input: root = [4,2,6,1,3]
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
    def getMinimumDifference(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        #in order recursive
        res = []
        def dfs(root, res):
            if not root:
                return
            dfs(root.left, res)
            res.append(root.val)
            dfs(root.right, res)
        
        dfs(root, res)
        diff = sys.maxint
        
        #打擂台
        for i in range(1, len(res)):
            diff = min(diff, res[i]-res[i-1])
            
        return diff
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

#### Red Black Tree

##### **Rules That Every Red-Black Tree Follows:** 

1. Every node has a color either red or black.

2. The root of the tree is always black.

3. There are no two adjacent red nodes (A red node cannot have a red parent or red child).

4. Every path from a node (including root) to any of its descendants NULL nodes has the same number of black nodes.

5. All leaf nodes are black nodes.

   | Sr. No. | Algorithm | Time Complexity |
   | :------ | :-------- | :-------------- |
   | 1.      | Search    | O(log n)        |
   | 2.      | Insert    | O(log n)        |
   | 3.      | Delete    | O(log n)        |

```

```



### Stack

#### Common Edge Case:

- When dealing with String problem involving numbers, rememebr there could be multi digit numbers instead of 0-9, can use stack or add (x*10 + i) to get the number
- Remember to convert str to int if in a string
- not string or len(s) == 0
- isdigit() return false for '-11' because '-' is not digit.
- try to ues //is in "+-*/" to test if it is a digit
- '1111111' or 'sssssssss'



#### Basic

[1130. Minimum Cost Tree From Leaf Values](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/discuss/339959/One-Pass-O(N)-Time-and-Space)
[907. Sum of Subarray Minimums](https://leetcode.com/problems/sum-of-subarray-minimums/discuss/170750/C++JavaPython-Stack-Solution)
[901. Online Stock Span](https://leetcode.com/problems/online-stock-span/discuss/168311/C++JavaPython-O(1))
[856. Score of Parentheses](https://leetcode.com/problems/score-of-parentheses/discuss/141777/C++JavaPython-O(1)-Space)
[503. Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/discuss/98270/JavaC++Python-Loop-Twice)
\496. Next Greater Element I
\84. Largest Rectangle in Histogram
\42. Trapping Rain Water



\1190. Reverse Substrings Between Each Pair of Parentheses

Medium

130434Add to ListShare

You are given a string `s` that consists of lower case English letters and brackets.

Reverse the strings in each pair of matching parentheses, starting from the innermost one.

Your result should **not** contain any brackets.

 

**Example 1:**

```
Input: s = "(abcd)"
Output: "dcba"
```

**Example 2:**

```
Input: s = "(u(love)i)"
Output: "iloveu"
Explanation: The substring "love" is reversed first, then the whole string is reversed.
```

```python
class Solution(object):
    def reverseParentheses(self, s):
        """
        :type s: str
        :rtype: str
        """
        #O(n) time and space
        # stack[0] will hold our result
        # for each ( we will create a space before the letter to hold it,
        # and whenever we see a ) we pop the letter and reverse it and put it back into
        # the previous letter
        
        stack = [""]
        for i in s:
            if i == "(":
                stack.append("")
            elif i == ")":
                add = stack.pop()[::-1]
                stack[-1] += add
            else:
                stack[-1] += i
        return stack.pop()
```

\394. Decode String

Medium

8161349Add to ListShare

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `105`.

 

**Example 1:**

```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"
```

**Example 2:**

```
Input: s = "3[a2[c]]"
Output: "accaccacc"
```

```py
class Solution(object):
    def decodeString(self, s):
        """
        :type s: str
        :rtype: str
        """
        #stack bracket problem
        #create a stack like ['',3,abc] to store number and char, pop when needed 
        res = [""]
        curNum = 0
        for i in s:
            if i.isdigit():
                curNum = curNum*10 + int(i)
            elif i == "[":
                res.append(curNum)
                curNum = 0
                res.append('')
            elif i == "]":
                add = res.pop() * res.pop()
                res[-1] += add
            else:
                res[-1] += i
        return res.pop()
```

\227. Basic Calculator II

Medium

4303569Add to ListShare

Given a string `s` which represents an expression, *evaluate this expression and return its value*. 

The integer division should truncate toward zero.

You may assume that the given expression is always valid. All intermediate results will be in the range of `[-231, 231 - 1]`.

**Note:** You are not allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

 

**Example 1:**

```
Input: s = "3+2*2"
Output: 7
```

```py
if not s:
            return "0"
        stack, num, sign = [], 0, "+"
        for i in xrange(len(s)):
            if s[i].isdigit():
                num = num*10+ord(s[i])-ord("0")
            if (not s[i].isdigit() and not s[i].isspace()) or i == len(s)-1:
                if sign == "-":
                    stack.append(-num)
                elif sign == "+":
                    stack.append(num)
                elif sign == "*":
                    stack.append(stack.pop()*num)
                else:
                    tmp = stack.pop()
                    if tmp//num < 0 and tmp%num != 0:
                        stack.append(tmp//num+1)
                    else:
                        stack.append(tmp//num)
                sign = s[i]
                num = 0
        return sum(stack)
```

\150. Evaluate Reverse Polish Notation

Medium

3074632Add to ListShare

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

 

**Example 1:**

```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

```python
class Solution(object):
    def evalRPN(self, tokens):
        """
        :type tokens: List[str]
        :rtype: int
        """
        #stack bracket
        # '/' case is tricky
        res = []
        for i in tokens:
            if i not in "+-*/":
                res.append(int(i))
            elif i == '+':
                res.append(res.pop() + res.pop())
            elif i == '-':
                sec, fir = res.pop(), res.pop()
                res.append(fir - sec)
            elif i == '*':
                res.append(res.pop() * res.pop())
            else:
                a, b = res.pop(), res.pop()
                add = b // a
                if add < 0 and b%a != 0:
                    res.append(add + 1)
                else:
                    res.append(add)
        return res.pop()
```

\856. Score of Parentheses

Medium

4405143Add to ListShare

Given a balanced parentheses string `s`, return *the **score** of the string*.

The **score** of a balanced parentheses string is based on the following rule:

- `"()"` has score `1`.
- `AB` has score `A + B`, where `A` and `B` are balanced parentheses strings.
- `(A)` has score `2 * A`, where `A` is a balanced parentheses string.

**Example 1:**

```
Input: s = "()"
Output: 1
```

```py
class Solution(object):
    def scoreOfParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        #Using stacks O(n) O(n)
        
#         #Create a stack and sum
#         stack = []
#         curSum = 0
        
#         for i in s:
#             #if i == ( we add sum of last layer into the stack and set sum of this layer = 0
#             if i == '(':
#                 stack.append(curSum)
#                 curSum = 0
#             #if i == ) sum = sum of last layer + 2* this layer 
#             else:
#                 curSum = stack.pop() + max(curSum * 2, 1)
#         return curSum
    
        #Follow up O(1) space: with no stack
        #Using levels
        
        res, level= 0, 0
        for i in range(0, len(s)-1):
            j = i+1
            if s[i] + s[j] == '()':
                res += 2 ** level
            if s[i] == '(':
                level += 1
            else:
                level -= 1
        return res
```

\1249. Minimum Remove to Make Valid Parentheses

Medium

480482Add to ListShare

Given a string s of `'('` , `')'` and lowercase English characters.

Your task is to remove the minimum number of parentheses ( `'('` or `')'`, in any positions ) so that the resulting *parentheses string* is valid and return **any** valid string.

Formally, a *parentheses string* is valid if and only if:

- It is the empty string, contains only lowercase characters, or
- It can be written as `AB` (`A` concatenated with `B`), where `A` and `B` are valid strings, or
- It can be written as `(A)`, where `A` is a valid string.

 

**Example 1:**

```
Input: s = "lee(t(c)o)de)"
Output: "lee(t(c)o)de"
Explanation: "lee(t(co)de)" , "lee(t(c)ode)" would also be accepted.
```

```py
class Solution(object):
    def minRemoveToMakeValid(self, s):
        """
        :type s: str
        :rtype: str
        """
        #stack bucket problem
        s = list(s)
        pointer, checker = 0, []
        for i in range(len(s)):
            #1 s[i] == ( so we save its index if its the first ( then append it to stack
            if s[i] == '(':
                checker.append(i)
            
            #2 s[i] == ) if stack empty then it is the extra one
            elif s[i] == ')':
                if not checker:
                    s[i] = ''
                    continue
                checker.pop()
        
        while checker:
            s[checker.pop()] = ''
        return ''.join(s)

```

\224. Basic Calculator

Hard

3619296Add to ListShare

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return *the result of the evaluation*.

**Note:** You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as `eval()`.

 

**Example 1:**

```
Input: s = "1 + 1"
Output: 2
```

```py
class Solution(object):
    def calculate(self, s):
        """
        :type s: str
        :rtype: int
        """
        #stack to hold bucket operation and sign 
        stack, sign, num, res = [], 1, 0, 0
        #loop thru the Stirng
            #if i is digit, append into num 
            #elif i is + or -, add i*sign into res, sign sign as 1 or -1
            #elif i is (, append res and sign into the stack
            #elif i is ), pop sign and res back
    
        for i in s:
            if i.isdigit():
                num = num * 10 + int(i)
            elif i == '+':
                res += num * sign
                num = 0
                sign = 1
            elif i == '-':
                res += num * sign
                num = 0
                sign = -1
            elif i == '(':
                stack.append(res)
                stack.append(sign)
                res = 0
                sign = 1
            elif i == ')':
                res += num * sign
                res *= stack.pop()
                res += stack.pop()
                num = 0
        if num != 0:
            res += num * sign
        return res
    
```

\503. Next Greater Element II

Medium

4568134Add to ListShare

Given a circular integer array `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`), return *the **next greater number** for every element in* `nums`.

The **next greater number** of a number `x` is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, return `-1` for this number.

 

**Example 1:**

```
Input: nums = [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number. 
The second 1's next greater number needs to search circularly, which is also 2.
```

```python
class Solution(object):
    def nextGreaterElements(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        #circular arary problem, brute force double for loop
        #stack solution uses stack to hold index from back to front
        
        n, stack = len(nums), []
        res = [0]*n
        for j in range(n-1, -1, -1):
            stack.append(j) 
        
        #loop from the last element and compare with each of the element in the front
        #add current number into stack because in next loop if last num smaller than curnum 
        #that will be the answser and if last num larger than curnum will continue to where it were in the last loop. 
        for i in range(n-1, -1, -1):
            #set defult res as -1
            res[i] = -1
            while(stack and nums[stack[-1]] <= nums[i]):
                stack.pop()
            if stack:
                res[i] = nums[stack[-1]]
            stack.append(i)
        return res
```

\71. Simplify Path

Medium

2427486Add to ListShare

Given a string `path`, which is an **absolute path** (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash `'/'`. For this problem, any other format of periods such as `'...'` are treated as file/directory names.

The **canonical path** should have the following format:

- The path starts with a single slash `'/'`.
- Any two directories are separated by a single slash `'/'`.
- The path does not end with a trailing `'/'`.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period `'.'` or double period `'..'`)

Return *the simplified **canonical path***.

 

**Example 1:**

```
Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

```python
class Solution(object):
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        stack = []
        for token in path.split('/'):
            if token == "..":
                if stack:
                    stack.pop()
            elif token != "." and token != '':
                stack.append(token)
        return '/' + '/'.join(stack)
            
```

#### Monotone Stack

\496. Next Greater Element I

Easy

2912190Add to ListShare

The **next greater element** of some element `x` in an array is the **first greater** element that is **to the right** of `x` in the same array.

You are given two **distinct 0-indexed** integer arrays `nums1` and `nums2`, where `nums1` is a subset of `nums2`.

For each `0 <= i < nums1.length`, find the index `j` such that `nums1[i] == nums2[j]` and determine the **next greater element** of `nums2[j]` in `nums2`. If there is no next greater element, then the answer for this query is `-1`.

Return *an array* `ans` *of length* `nums1.length` *such that* `ans[i]` *is the **next greater element** as described above.*

 

**Example 1:**

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
Explanation: The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [1,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,2]. There is no next greater element, so the answer is -1.
```

```py
class Solution(object):
    def nextGreaterElement(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        #monotone stack problem, create a stack that only increases or decreases
        #if find a bigger number, pop stack while that number > stack.peek()
        
        #use dict to hold NGE 
        dic = collections.defaultdict(int)
        stack = []
        
        for i in nums2:
            while stack and i > stack[-1]:
                dic[stack.pop()] = i
            stack.append(i)

        for j in range(len(nums1)):
            nums1[j] = dic.get(nums1[j]) or -1
            
        return nums1
```

\739. Daily Temperatures

Medium

7029158Add to ListShare

Given an array of integers `temperatures` represents the daily temperatures, return *an array* `answer` *such that* `answer[i]` *is the number of days you have to wait after the* `ith` *day to get a warmer temperature*. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

 

**Example 1:**

```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

```py
class Solution(object):
    def dailyTemperatures(self, temperatures):
        """
        :type temperatures: List[int]
        :rtype: List[int]
        """
        #use a stack and counter
        stack, counter = [], 1
        
        #loop thru the array and append index to stack. when see a bigger element, compare the index to find the num of days
        for i in range(len(temperatures)):
            while stack and temperatures[stack[-1]] < temperatures[i]:
                temp = stack.pop()
                temperatures[temp] = i - temp
            stack.append(i)
        for j in stack:
            temperatures[j] = 0
        return temperatures
        
```

\402. Remove K Digits

Medium

6080253Add to ListShare

Given string num representing a non-negative integer `num`, and an integer `k`, return *the smallest possible integer after removing* `k` *digits from* `num`.

 

**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

```py
class Solution(object):
    def removeKdigits(self, num, k):
        """
        :type num: str
        :type k: int
        :rtype: str
        """
        stack = []
        #using stack to hold needed number and when find a smaller number pop the stack[-1]
        for i in num:
            while stack and k > 0 and stack[-1] > i:
                stack.pop()
                k -= 1
            stack.append(i)
        
        #while not done gitting rid of numbers, keep poping because only bigger numbers at the end
        while k > 0:
            stack.pop()
            k -= 1
            
        #while there are 0s at the beginning, pop it
        #you can also not append it to stack when there's nothing in stack
        j = 0
        while j < len(stack)-1 and stack[j] == "0":
            stack[j] = ''
            j += 1
        if not stack:
            return '0'
        return ''.join(stack)
```

\316. Remove Duplicate Letters

Medium

5307346Add to ListShare

Given a string `s`, remove duplicate letters so that every letter appears once and only once. You must make sure your result is **the smallest in lexicographical order** among all possible results.

 

**Example 1:**

```
Input: s = "bcabc"
Output: "abc"
```

```PY
class Solution(object):
    def removeDuplicateLetters(self, s):
        """
        :type s: str
        :rtype: str
        """
        #monotone stack
        #use dict to keep track of appearace of each element
        stack = []
        dic = collections.defaultdict(int)
        for i in s:
            dic[i] += 1

        #keep appending i into stack, if find element smaller than stack[-1] and there are more stack[-1] left, pop
        for i in s:
            if i not in stack:
                while stack and dic.get(stack[-1]) > 0 and i <= stack[-1]:
                    stack.pop()
                stack.append(i)
            dic[i] -= 1
        
        #get rid of the dups in the end
        stack = stack[0:len(dic)]
        return ''.join(stack)
```

\456. 132 Pattern

Medium

4640262Add to ListShare

Given an array of `n` integers `nums`, a **132 pattern** is a subsequence of three integers `nums[i]`, `nums[j]` and `nums[k]` such that `i < j < k` and `nums[i] < nums[k] < nums[j]`.

Return `true` *if there is a **132 pattern** in* `nums`*, otherwise, return* `false`*.*

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: false
Explanation: There is no 132 pattern in the sequence.
```

```

```



### Heap

#### Index

```py
#you want O(1) max() and min()

#Difference between heappush and heapify:
    1. The heappush method will have time complexity O(n * log(n)) where n is ending size of the heap, while the heapify method will have complexity O(n), which is significantly lower. 
    2. heappush assumes that the array (H in your case) is already a heap. heapify does not
    3. doing heapify on a list is almost always a better choice than creating an empty list and adding many items with heappush. If you just add a few items, heappush may be better.

#common functions 
heapq.heapify() #build
heapq.heappop() #pop 
heapq.heappush(,) #push
heapq.heapreplace(,) #pop then push
heapq.heappoppush(,) #push then pop
heapq.nlargest(n, ) #get n th largest element
heapq.nsmallest(n, ) #get n th smallest elemnt 

#max and min heap
in python, the difference between max and min heap is just the way you push elements into the heap heapq.heappush(heap, i) vs heapq.heappush(heap, -i)
# Build heap
	heap = [(-v, k) for k, v in cnt.items()]
	heapq.heapify(heap)
```

\1046. Last Stone Weight

Easy

317964Add to ListShare

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose the **heaviest two stones** and smash them together. Suppose the heaviest two stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return *the smallest possible weight of the left stone*. If there are no stones left, return `0`.

 

**Example 1:**

```
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation: 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of the last stone.
```

```py
class Solution(object):
    def lastStoneWeight(self, stones):
        """
        :type stones: List[int]
        :rtype: int
        """
        #brute force use sort and after every smash resort O(N^2 logn)
        #solution #1 use heap to build heap and pop + every insertion only take O(log n) so total O(N log n)
        #solution #2 use binary search, first sort then use binary search to insert
        
        #heap solution
        #we want the heaveiestg stone so make stones value negative so we will pop largest
        h = [-x for x in stones]
        heapq.heapify(h)
        
        while len(h) > 1:
            heapq.heappush(h, heappop(h) - heappop(h))
        
        return -h[-1]
```

\703. Kth Largest Element in a Stream

Easy

29231739Add to ListShare

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

 

**Example 1:**

```
Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]

Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
```

```py
class KthLargest(object):

    def __init__(self, k, nums):
        """
        :type k: int
        :type nums: List[int]
        """
        self.k = k
        self.nums = nums
        heapq.heapify(self.nums)
        while len(self.nums) > k:
            heapq.heappop(self.nums)
        

    def add(self, val):
        """
        :type val: int
        :rtype: int
        """
        if len(self.nums) < self.k:
            heapq.heappush(self.nums, val)
        elif val > self.nums[0]:
            heapq.heapreplace(self.nums, val)
        return self.nums[0]


# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)
```

\347. Top K Frequent Elements

Medium

9245372Add to ListShare

Given an integer array `nums` and an integer `k`, return *the* `k` *most frequent elements*. You may return the answer in **any order**.

 

**Example 1:**

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

```py
class Solution(object):
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

\451. Sort Characters By Frequency

Medium

4156181Add to ListShare

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
class Solution(object):
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
        print heap
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

\692. Top K Frequent Words

Medium

4500252Add to ListShare

Given an array of strings `words` and an integer `k`, return *the* `k` *most frequent strings*.

Return the answer **sorted** by **the frequency** from highest to lowest. Sort the words with the same frequency by their **lexicographical order**.

 

**Example 1:**

```
Input: words = ["i","love","leetcode","i","love","coding"], k = 2
Output: ["i","love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.
```

```py
class Solution(object):
    def topKFrequent(self, words, k):
        """
        :type words: List[str]
        :type k: int
        :rtype: List[str]
        """
        #Heap problem
        #use int dict to find frequency, -1 for finding item, then push into heap, pop in res
        
        dic = collections.defaultdict(int)
        
        for i in words:
            if i in dic:
                dic[i] += 1
            else:
                dic[i] = 1
        
        #now we have a dict holding item and freq
        heap = []
        for key in dic:
            heapq.heappush(heap, (dic[key], key))
            if len(heap) > k:
                heapq.heappop(heap)
            
        #now ew have a heap with sorted freq, since -1, appeared more will be at the front
        # res = []
        # counter = 0
        # while counter < k:
        #     res.append(heapq.heappop(heap)[-1])
        #     counter +=1 
        # return res
        res = [i[-1] for i in heap]
        return res
```

\378. Kth Smallest Element in a Sorted Matrix

Medium

5906240Add to ListShare

Given an `n x n` `matrix` where each of the rows and columns is sorted in ascending order, return *the* `kth` *smallest element in the matrix*.

Note that it is the `kth` smallest element **in the sorted order**, not the `kth` **distinct** element.

You must find a solution with a memory complexity better than `O(n2)`.

 

**Example 1:**

```
Input: matrix = [[1,5,9],[10,11,13],[12,13,15]], k = 8
Output: 13
Explanation: The elements in the matrix are [1,5,9,10,11,12,13,13,15], and the 8th smallest number is 13
```

```py
class Solution(object):
    def kthSmallest(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        heap = []
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                heapq.heappush(heap, matrix[i][j])
        
        count = 1
        while count < k:
            heapq.heappop(heap)
            count += 1
        return heapq.heappop(heap)
```

#### Cheapest flight problem*

\743. Network Delay Time

Medium

4897305Add to ListShare

You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source node, `vi` is the target node, and `wi` is the time it takes for a signal to travel from source to target.

We will send a signal from a given node `k`. Return *the **minimum** time it takes for all the* `n` *nodes to receive the signal*. If it is impossible for all the `n` nodes to receive the signal, return `-1`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/05/23/931_example_1.png)

```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```

```

```

\787. Cheapest Flights Within K Stops

Medium

4992228Add to ListShare

There are `n` cities connected by some number of flights. You are given an array `flights` where `flights[i] = [fromi, toi, pricei]` indicates that there is a flight from city `fromi` to city `toi` with cost `pricei`.

You are also given three integers `src`, `dst`, and `k`, return ***the cheapest price** from* `src` *to* `dst` *with at most* `k` *stops.* If there is no such route, return `-1`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-3drawio.png)

```
Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
Output: 700
Explanation:
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.
```

```

```

\973. K Closest Points to Origin

Medium

5615207Add to ListShare

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

```

```



### Searching

#### Binary Search

##### Template

```c++

        int n = nums.size();
        int left = 0;
        int right = n; // 我们定义target在左闭右开的区间里，[left, right)  
        while (left < right) { // 因为left == right的时候，在[left, right)是无效的空间
            int middle = left + ((right - left) >> 1);
            if (nums[middle] > target) {
                right = middle; // target 在左区间，因为是左闭右开的区间，nums[middle]一定不是我们的目标值，所以right = middle，在[left, middle)中继续寻找目标值
            } else if (nums[middle] < target) {
                left = middle + 1; // target 在右区间，在 [middle+1, right)中
            } else { // nums[middle] == target
                return middle; // 数组中找到目标值的情况，直接返回下标
            }
        }
        return right;
```

```python
		left, right = 1, n
        while left < right:
            mid = left + (right - left) // 2
            if isBadVersion(mid):
                right = mid
            else:
                left = mid + 1
        return left
```

##### Basic

\300. Longest Increasing Subsequence

Medium

12292237Add to ListShare

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

 

**Example 1:**

```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```

```py
class Solution(object):
    def lengthOfLIS(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        res = []
        for i in nums:
            if not res or i > res[-1]:
                res.append(i)
            else:
                idx = bisect_left(res, i)  # Find the index of the smallest number >= x
                res[idx] = i
        return len(res)
```

\74. Search a 2D Matrix

Medium

7879281Add to ListShare

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

```py
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        for subMatrix in matrix:
            if target <= subMatrix[-1]:
                #do binary search
                left, right, mid = 0, len(subMatrix)-1, 0
                while left < right:
                    mid = (left + right)//2 #python, other use left + (right -left)//2
                    if target < subMatrix[mid]:
                        right = mid
                    elif target > subMatrix[mid]:
                        left = mid+1
                    else:
                        return True
                if subMatrix[left] == target or subMatrix[right] == target:
                    return True 
                else:
                    return False
                
```

\34. Find First and Last Position of Element in Sorted Array

Medium

11133302Add to ListShare

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

 

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

```py
class Solution(object):
    def searchRange(self, nums, target):
        if not nums: 
            return [-1, -1]
        #find 
        def searchLeft(nums, target):
            start, end = 0, len(nums) - 1
            while start + 1 < end:
                mid = (start + end) / 2
                if target > nums[mid]:
                    start = mid 
                else:
                    end = mid
            if nums[start] == target:
                return start
            elif nums[end] == target:
                return end
            else:
                return -1


        def searchRight(nums, target):
            start, end = 0, len(nums) - 1
            while start + 1 < end:
                mid = (start + end) / 2
                if target < nums[mid]:
                    end = mid
                else:
                    start = mid
            if nums[end] == target:
                return end
            elif nums[start] == target:
                return start
            else:
                return -1
        
        left = searchLeft(nums, target)
        right =  searchRight(nums, target)
        return [left, right]   
```

\81. Search in Rotated Sorted Array II

Medium

4564731Add to ListShare

There is an integer array `nums` sorted in non-decreasing order (not necessarily with **distinct** values).

Before being passed to your function, `nums` is **rotated** at an unknown pivot index `k` (`0 <= k < nums.length`) such that the resulting array is `[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]` (**0-indexed**). For example, `[0,1,2,4,4,4,5,6,6,7]` might be rotated at pivot index `5` and become `[4,5,6,6,7,0,1,2,4,4]`.

Given the array `nums` **after** the rotation and an integer `target`, return `true` *if* `target` *is in* `nums`*, or* `false` *if it is not in* `nums`*.*

You must decrease the overall operation steps as much as possible.

 

**Example 1:**

```
Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
```

```py
class Solution(object):
    def search(self, nums, target):
        start, end = 0, len(nums) - 1
        while start + 1 < end:
            mid = (start + end) / 2
            if nums[mid] == target or nums[start] == target or nums[end] == target:
                return True
            if nums[start] < nums[mid]:
                if nums[start] <= target <= nums[mid]:
                    end = mid
                else:
                    start = mid
            elif nums[end] > nums[mid]:
                if nums[mid] <= target <= nums[end]:
                    start = mid
                else:
                    end = mid
            else:
                start += 1
                
        if nums[start] == target or nums[end] == target:
            return True
        else:
            return False
        
```

\287. Find the Duplicate Number

Medium

144261773Add to ListShare

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return *this repeated number*.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

 

**Example 1:**

```
Input: nums = [1,3,4,2,2]
Output: 2
```

```py
class Solution(object):
    def findDuplicate(self, nums):
        slow = fast = finder = 0
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                while finder != slow:
                    finder = nums[finder]
                    slow = nums[slow]
                return finder
```

\162. Find Peak Element

Medium

63173804Add to ListShare

A peak element is an element that is strictly greater than its neighbors.

Given an integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`.

You must write an algorithm that runs in `O(log n)` time.

 

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

```py
class Solution(object):
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #binary search, check middle vs its left and tight
        #logn
        left, right = 0, len(nums) - 1
        while left < right:
            mid1 = (left + right)//2
            mid2 = mid1+1
            if nums[mid1] < nums[mid2]:
                left = mid2
            else:
                right = mid1
        return left
```

#### Two Pointers and Sliding window

##### Template:

```c++
For most substring problem, we are given a string and need to find a substring of it which satisfy some restrictions. A general way is to use a hashmap assisted with two pointers. The template is given below.

int findSubstring(string s){
        vector<int> map(128,0);
        int counter; // check whether the substring is valid
        int begin=0, end=0; //two pointers, one point to tail and one  head
        int d; //the length of substring

        for() { /* initialize the hash map here */ }

        while(end<s.size()){

            if(map[s[end++]]-- ?){  /* modify counter here */ }

            while(/* counter condition */){ 
                 
                 /* update d here if finding minimum*/

                //increase begin to make it invalid/valid again
                
                if(map[s[begin++]]++ ?){ /*modify counter here*/ }
            }  

            /* update d here if finding maximum*/
        }
        return d;
  }
```

\3. Longest Substring Without Repeating Characters

Medium

254911104Add to ListShare

Given a string `s`, find the length of the **longest substring** without repeating characters.

 

**Example 1:**

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

```py
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        #use two pointer, when meet a repeated element, put slow pointer at the next element of repeated
        slow, fast = 0,0
        maxLen = 0
        hashSet = set()
        
        while fast<len(s):
            if s[fast] not in hashSet:
                hashSet.add(s[fast])
                fast += 1
                maxLen = max(maxLen, len(hashSet))
            else:
                hashSet.remove(s[slow])
                slow += 1
        return maxLen
```

\49. Group Anagrams

Medium

9840331Add to ListShare

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

**Example 1:**

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

```py
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        #first create a dict to hold res, then loop each element in the strs
        #if sorted(i) in dict, put into the array, if not, create a new array in dict
        res = {}
        for i in strs:
            j = ''.join(sorted(i))
            if res.has_key(j):
                res[j].append(i)
            else:
                res[j] = [i]
        final = []
        for i in res.values():
            final.append(i)
        return final
    #another way to reduce time is to use [26] to make the key instead of sorting it 
```

\560. Subarray Sum Equals K

Medium

13653437Add to ListShare

Given an array of integers `nums` and an integer `k`, return *the total number of subarrays whose sum equals to* `k`.

A subarray is a contiguous **non-empty** sequence of elements within an array.

 

**Example 1:**

```
Input: nums = [1,1,1], k = 2
Output: 2
```

```py
class Solution(object):
    def subarraySum(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        #use hashmap and prefixsum 
        hashmap = {}
        sumArr, res = 0, 0
        hashmap[0] = 1
        
        #loop thru every element in nums, adding into sum.
        for i in nums:
            sumArr += i
            #if have found subarray(from [0]) that == sumArr - k, add into res based on freq
            if hashmap.has_key(sumArr - k):
                res += hashmap[sumArr-k]
            
            #adding subarrray into hashmap 
            if hashmap.has_key(sumArr):
                hashmap[sumArr] += 1
            else:
                hashmap[sumArr] = 1
                
        return res
```

\11. Container With Most Water

Medium

17753971Add to ListShare

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return *the maximum amount of water a container can store*.

**Notice** that you may not slant the container.

 

**Example 1:**

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```

```py
class Solution(object):
    def maxArea(self, height):
        #two pointer problem, moving towards middle, moving the lower one
        slow, fast, res = 0, len(height) - 1, 0
        for n in range(len(height)):
            res = max(res, min(height[slow], height[fast]) * (fast - slow))
            if height[fast] > height[slow]:
                slow += 1
            else:
                fast -= 1
        return res
```

\16. 3Sum Closest

Medium

6105263Add to ListShare

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.

Return *the sum of the three integers*.

You may assume that each input would have exactly one solution.

 

**Example 1:**

```
Input: nums = [-1,2,1,-4], target = 1
Output: 2
Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

```py
class Solution(object):
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        #two pointer approach, first sort, then move around
        nums = sorted(nums)
        res = 10000000
        for i in range(len(nums)-2):
            left, right = i+1, len(nums) -1
            while left < right:
                sums = nums[i] + nums[left] + nums[right]
                if abs(sums -target) < abs(res-target):
                    res = sums
                if sums < target:
                    left +=1
                elif sums > target:
                    right -= 1
                else:
                    return target
        return res

            
```

\424. Longest Repeating Character Replacement

Medium

4834194Add to ListShare

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return *the length of the longest substring containing the same letter you can get after performing the above operations*.

 

**Example 1:**

```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with two 'B's or vice versa.
```

```py
class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        left, right = 0, -1
        dic = collections.defaultdict(int)
        maxChar, maxLength = 0, 0
        
        #for each element in s, add the count of the element in dict
        for i in s:
            dic[i] += 1
            right += 1
            maxChar = max(maxChar, dic[i])
            #if replacement element more than k, move start to right
            while(right-left+1-maxChar > k):
                dic[s[left]] -= 1
                left += 1
            #reset maxLength
            maxLength = max(maxLength, right-left+1)
        return maxLength
```

\713. Subarray Product Less Than K

Medium

4134138Add to ListShare

Given an array of integers `nums` and an integer `k`, return *the number of contiguous subarrays where the product of all the elements in the subarray is strictly less than* `k`.

 

**Example 1:**

```
Input: nums = [10,5,2,6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are:
[10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```

```py
class Solution(object):
    def numSubarrayProductLessThanK(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        #sliding window, add subarray length
        #[8, 2, 10] has 1 that contains 8, 2 contains 2, 3 contains 10, so total 6
        left, count, multiplier = 0, 0, 1
        for right in range(len(nums)):
            multiplier *= nums[right]
            while multiplier >= k and left <= right:
                multiplier /= nums[left]
                left += 1
            count += (right - left + 1)
        return count
                
```

\567. Permutation in String

Medium

6267189Add to ListShare

Given two strings `s1` and `s2`, return `true` *if* `s2` *contains a permutation of* `s1`*, or* `false` *otherwise*.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

 

**Example 1:**

```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains one permutation of s1 ("ba").
```

```py
class Solution(object):
    def checkInclusion(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        if len(s1) > len(s2):
            return False
        #Sliding window + hashmap
        left, right = 0, 0
        need = collections.Counter(s1)
        hashmap = collections.defaultdict(int)
        counter = 0
        
        
        while right < len(s2):
            #change in window data
            a = s2[right]
            right += 1
            if a in need:
                hashmap[a] += 1
                if hashmap[a] == need[a]:
                    counter += 1
            
            
            while right - left >= len(s1):
                if counter == len(need):
                    return True
                b = s2[left]
                if b in need:
                    if hashmap[b] == need[b]:
                        counter -= 1
                    hashmap[b] -= 1
                left += 1
        return False 
```

\438. Find All Anagrams in a String

Medium

7756259Add to ListShare

Given two strings `s` and `p`, return *an array of all the start indices of* `p`*'s anagrams in* `s`. You may return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

 

**Example 1:**

```
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

```py
class Solution(object):
    def findAnagrams(self, s2, s1):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        if len(s1) > len(s2):
            return []
        #Sliding window + hashmap
        left, right = 0, 0
        need = collections.Counter(s1)
        hashmap = collections.defaultdict(int)
        counter = 0
        res = []
        
        
        while right < len(s2):
            #change in window data
            a = s2[right]
            right += 1
            if a in need:
                hashmap[a] += 1
                if hashmap[a] == need[a]:
                    counter += 1
            
            
            while right - left >= len(s1):
                if counter == len(need):
                    res.append(left)
                b = s2[left]
                if b in need:
                    if hashmap[b] == need[b]:
                        counter -= 1
                    hashmap[b] -= 1
                left += 1
        return res
```

\76. Minimum Window Substring

Hard

10881545Add to ListShare

Given two strings `s` and `t` of lengths `m` and `n` respectively, return *the **minimum window substring** of* `s` *such that every character in* `t` *(**including duplicates**) is included in the window. If there is no such substring**, return the empty string* `""`*.*

The testcases will be generated such that the answer is **unique**.

A **substring** is a contiguous sequence of characters within the string.

 

**Example 1:**

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

```py
class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        #typical sliding window problem, two pointers + hashmap
        #initialize variables
        if len(t) > len(s):
            return ''
        left, right = 0, 0
        need = collections.Counter(t)
        dic = collections.defaultdict(int)
        counter = 0
        resLen = sys.maxsize
        start = 0
        
        while right < len(s):
            #manage in window
            a = s[right]
            right += 1
            if a in need:
                dic[a] += 1
                if dic[a] == need[a]:
                    counter += 1
            #manage out of window
            while counter == len(need):
                if(right - left < resLen):
                    resLen = right - left
                    start = left
                b = s[left]
                left += 1
                if b in need:
                    if need[b] == dic[b]:
                        counter -= 1
                    dic[b] -= 1
        if resLen == sys.maxint:
            return ""
        else:
            return s[start:start + resLen]
```





#### DFS

\341. Flatten Nested List Iterator

Medium

38431340Add to ListShare

You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be integers or other lists. Implement an iterator to flatten it.

Implement the `NestedIterator` class:

- `NestedIterator(List<NestedInteger> nestedList)` Initializes the iterator with the nested list `nestedList`.
- `int next()` Returns the next integer in the nested list.
- `boolean hasNext()` Returns `true` if there are still some integers in the nested list and `false` otherwise.

Your code will be tested with the following pseudocode:

```
initialize iterator with nestedList
res = []
while iterator.hasNext()
    append iterator.next() to the end of res
return res
```

```py
class NestedIterator(object):

    def __init__(self, nestedList):
        """
        Initialize your data structure here.
        :type nestedList: List[NestedInteger]
        """
        self.position = 0
        self.lists = []
        def dfs(nested):
            for i in nested:
                #if integer, append
                if i.isInteger():
                    self.lists.append(i.getInteger())
                #if nestedList, dfs the list
                else:
                    dfs(i.getList())
        
        dfs(nestedList)
        
    
    def next(self):
        """
        :rtype: int
        """
        res = self.lists[self.position]
        self.position += 1
        return res
        

    def hasNext(self):
        """
        :rtype: bool
        """
        if self.position == len(self.lists):
            return False
        return True
        
```

\545. Boundary of Binary Tree

Medium

11361824Add to ListShare

The **boundary** of a binary tree is the concatenation of the **root**, the **left boundary**, the **leaves** ordered from left-to-right, and the **reverse order** of the **right boundary**.

The **left boundary** is the set of nodes defined by the following:

- The root node's left child is in the left boundary. If the root does not have a left child, then the left boundary is **empty**.
- If a node in the left boundary and has a left child, then the left child is in the left boundary.
- If a node is in the left boundary, has **no** left child, but has a right child, then the right child is in the left boundary.
- The leftmost leaf is **not** in the left boundary.

The **right boundary** is similar to the **left boundary**, except it is the right side of the root's right subtree. Again, the leaf is **not** part of the **right boundary**, and the **right boundary** is empty if the root does not have a right child.

The **leaves** are nodes that do not have any children. For this problem, the root is **not** a leaf.

Given the `root` of a binary tree, return *the values of its **boundary***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/11/boundary1.jpg)

```
Input: root = [1,null,2,3,4]
Output: [1,3,4,2]
Explanation:
- The left boundary is empty because the root does not have a left child.
- The right boundary follows the path starting from the root's right child 2 -> 4.
  4 is a leaf, so the right boundary is [2].
- The leaves from left to right are [3,4].
Concatenating everything results in [1] + [] + [3,4] + [2] = [1,3,4,2].
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def boundaryOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        def dfs(root, way):
            res = []
            if not root:
                return []
            #left
            if way == 0:
                if not root.left and not root.right:
                    return res
                elif root.left:
                    res.append(root.val)
                    return res + dfs(root.left, 0)
                elif root.right:
                    res.append(root.val)
                    return res + dfs(root.right, 0)
            #right
            elif way == 1:
                if not root.left and not root.right:
                    return res
                elif root.right:
                    res.append(root.val)
                    return res + dfs(root.right, 1)
                elif root.left:
                    res.append(root.val)
                    return res + dfs(root.left, 1)
            else:
                if not root.left and not root.right:
                    res.append(root.val)
                    return res
                if root.left and root.right:
                    return dfs(root.left, 2) + dfs(root.right, 2)
                elif root.left:
                    return dfs(root.left, 2)
                elif root.right:
                    return dfs(root.right, 2)
                

                
        if not root.left and not root.right:
            return [root.val]
        #left boundary
        left = dfs(root.left, 0)
        #leaf
        leaf = dfs(root, 2)
        #right boundary
        right = dfs(root.right, 1)
        
        return [root.val]+left+leaf+right[::-1]
```

\99. Recover Binary Search Tree

Medium

5779190Add to ListShare

You are given the `root` of a binary search tree (BST), where the values of **exactly** two nodes of the tree were swapped by mistake. *Recover the tree without changing its structure*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg)

```
Input: root = [1,3,null,null,2]
Output: [3,1,null,null,2]
Explanation: 3 cannot be a left child of 1 because 3 > 1. Swapping 1 and 3 makes the BST valid.
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: None Do not return anything, modify root in-place instead.
        """
        """
        use inorder traversal, arr will be accending 
        , find two mistakes
        """
        ### can be solved with morris, costant space
        ###                     Recursive: easiest
        # arr = []
        # def inorder(root):
        #     if root:
        #         inorder(root.left)
        #         arr.append(root)
        #         inorder(root.right)
        # inorder(root)
        # mis1 = arr[0]
        # mis2 = arr[-1]
        # for i in range(1,len(arr)):
        #     if arr[i].val < arr[i-1].val:
        #         mis1 = arr[i-1]
        #         break
        # for j in range(len(arr)-2, -1,-1):
        #     if arr[j].val > arr[j+1].val:
        #         mis2 = arr[j+1]
        #         break
        # mis1.val, mis2.val = mis2.val, mis1.val
        
        
        ###Inorder Traversal: Iterative: Best Time Performance
        stack = []
        x = y = pred = None
        
        while stack or root:
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            if pred and root.val < pred.val:
                y = root
                if x is None:
                    x = pred 
                else:
                    break
            pred = root
            root = root.right

        x.val, y.val = y.val, x.val
        
```



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

\721. Accounts Merge

Medium

4411799Add to ListShare

Given a list of `accounts` where each element `accounts[i]` is a list of strings, where the first element `accounts[i][0]` is a name, and the rest of the elements are **emails** representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails **in sorted order**. The accounts themselves can be returned in **any order**.

 

**Example 1:**

```
Input: accounts = [["John","johnsmith@mail.com","john_newyork@mail.com"],["John","johnsmith@mail.com","john00@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Output: [["John","john00@mail.com","john_newyork@mail.com","johnsmith@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Explanation:
The first and second John's are the same person as they have the common email "johnsmith@mail.com".
The third John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

```py
class Solution(object):
    def accountsMerge(self, accounts):
        """
        :type accounts: List[List[str]]
        :rtype: List[List[str]]
        """
        #set up
        res = []
        graph = collections.defaultdict(list)
        visited = [False] * len(accounts)
        
        #build graph
        for i, account in enumerate(accounts):
            for j in range(1, len(account)):
                graph[account[j]].append(i)
        
        #dfs
        def dfs(i, emails):
            if visited[i]:
                return
            visited[i] = True
            for j in range(1, len(accounts[i])):
                email = accounts[i][j]
                emails.add(email)
                for neibor in graph[email]:
                    dfs(neibor, emails)
                
        #walk thru and append to res
        for i, account in enumerate(accounts):
            if visited[i]:
                continue
            name, emails = account[0], set()
            dfs(i, emails)
            res.append([name] + sorted(emails))
        return res
```

\547. Number of Provinces

Medium

5434245Add to ListShare

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return *the total number of **provinces***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

```
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2
```

```py
class Solution(object):
    def findCircleNum(self, isConnected):
        """
        :type isConnected: List[List[int]]
        :rtype: int
        """
                #dfs and a visited list
        #ineach loop
        
        count = 0
        visited = [0] * len(isConnected)
        
        #dfs
        def dfs(i):
            for j in range(len(isConnected)):
                if isConnected[i][j] == 1 and visited[j] == 0:
                    visited[j] = 1
                    dfs(j)     
        
        
        #walk thru the list and return graph len
        for i in range(len(visited)):
            if visited[i] == 0:
                dfs(i)
                count += 1
        return count
```

\339. Nested List Weight Sum

Medium

1369312Add to ListShare

You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be integers or other lists.

The **depth** of an integer is the number of lists that it is inside of. For example, the nested list `[1,[2,2],[[3],2],1]` has each integer's value set to its **depth**.

Return *the sum of each integer in* `nestedList` *multiplied by its **depth***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/14/nestedlistweightsumex1.png)

```
Input: nestedList = [[1,1],2,[1,1]]
Output: 10
Explanation: Four 1's at depth 2, one 2 at depth 1. 1*2 + 1*2 + 2*1 + 1*2 + 1*2 = 10.
```

```py
class Solution(object):
    def depthSum(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        #kinda like a dfs, for each element, call helper function
        return self.helper(nestedList, 1)
    
    def helper(self, i, depth):
        total = 0
        for lists in i:
            if lists.isInteger():
                total += lists.getInteger() * depth
            else:
                total += self.helper(lists.getList(), depth+1)
        return total
```

\364. Nested List Weight Sum II

Medium

1011303Add to ListShare

You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be integers or other lists.

The **depth** of an integer is the number of lists that it is inside of. For example, the nested list `[1,[2,2],[[3],2],1]` has each integer's value set to its **depth**. Let `maxDepth` be the **maximum depth** of any integer.

The **weight** of an integer is `maxDepth - (the depth of the integer) + 1`.

Return *the sum of each integer in* `nestedList` *multiplied by its **weight***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/27/nestedlistweightsumiiex1.png)

```
Input: nestedList = [[1,1],2,[1,1]]
Output: 8
Explanation: Four 1's with a weight of 1, one 2 with a weight of 2.
1*1 + 1*1 + 2*2 + 1*1 + 1*1 = 8
```

```py
class Solution:
    def depthSumInverse(self, nestedList: List[NestedInteger]) -> int:
                #similar to part 1, adding a loop at the beginning to find the max depth
        #then use dfs to loop and find the total
        maxDepth = self.maxDepth(nestedList)
        return self.dfs(maxDepth, nestedList, 1)
    
    
    
    #find the total
    def dfs(self, maxDepth, lists, depth):
        total = 0
        for i in lists:
            if i.isInteger():
                total += i.getInteger() * (maxDepth - depth + 1)
            else:
                total += self.dfs(maxDepth, i.getList(), depth+1)
        return total
        
        
        
    # find maxDepth using DFS 
    def maxDepth(self, lists):
        maxDepth = 1
        for i in lists:
            if i.isInteger():
                continue
            else:
                maxDepth = max(self.maxDepth(i.getList())+1, maxDepth)
        return maxDepth
```

```py
class Solution(object):
    def depthSumInverse(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        #similar to part 1, adding a loop at the beginning to find the max depth
        #then use dfs to loop and find the total
        self.maxDepth = 0
        res = []
        
        def dfs(lists, depth):
            self.maxDepth = max(depth, self.maxDepth)
            for i in lists:
                if i.isInteger():
                    res.append((depth, i.getInteger()))
                else:
                    dfs(i.getList(), depth+1)
            
        dfs(nestedList, 0)
        total = 0
        for depth, val in res:
            total += (self.maxDepth-depth+1)*val
        return total
```

\426. Convert Binary Search Tree to Sorted Doubly Linked List

Medium

2259179Add to ListShare

Convert a **Binary Search Tree** to a sorted **Circular Doubly-Linked List** in place.

You can think of the left and right pointers as synonymous to the predecessor and successor pointers in a doubly-linked list. For a circular doubly linked list, the predecessor of the first element is the last element, and the successor of the last element is the first element.

We want to do the transformation **in place**. After the transformation, the left pointer of the tree node should point to its predecessor, and the right pointer should point to its successor. You should return the pointer to the smallest element of the linked list.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/12/bstdlloriginalbst.png)

```
Input: root = [4,2,5,1,3]
```

```py
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
"""

class Solution(object):
    def treeToDoublyList(self, root):
        """
        :type root: Node
        :rtype: Node
        """
        #using dfs because going down
        if not root:
            return
        head, tail = self.dfs(root)
        head.left = tail
        tail.right = head
        return head

    
    def dfs(self, root):
        if not root:
            return None, None
        leftHead, leftTail = self.dfs(root.left)
        rightHead, rightTail = self.dfs(root.right)
        if leftTail:
            leftTail.right = root
            root.left = leftTail
        if rightHead:
            root.right = rightHead
            rightHead.left = root
        if leftHead:
            head = leftHead
        else:
            head = root
        if rightTail:
            tail = rightTail
        else:
            tail = root
        return head, tail
```

\2096. Step-By-Step Directions From a Binary Tree Node to Another

Medium

115275Add to ListShare

You are given the `root` of a **binary tree** with `n` nodes. Each node is uniquely assigned a value from `1` to `n`. You are also given an integer `startValue` representing the value of the start node `s`, and a different integer `destValue` representing the value of the destination node `t`.

Find the **shortest path** starting from node `s` and ending at node `t`. Generate step-by-step directions of such path as a string consisting of only the **uppercase** letters `'L'`, `'R'`, and `'U'`. Each letter indicates a specific direction:

- `'L'` means to go from a node to its **left child** node.
- `'R'` means to go from a node to its **right child** node.
- `'U'` means to go from a node to its **parent** node.

Return *the step-by-step directions of the **shortest path** from node* `s` *to node* `t`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/11/15/eg1.png)

```
Input: root = [5,1,2,3,null,6,4], startValue = 3, destValue = 6
Output: "UURL"
Explanation: The shortest path is: 3 → 1 → 5 → 2 → 6.
```

```

```

\430. Flatten a Multilevel Doubly Linked List

Medium

3911273Add to ListShare

You are given a doubly linked list, which contains nodes that have a next pointer, a previous pointer, and an additional **child pointer**. This child pointer may or may not point to a separate doubly linked list, also containing these special nodes. These child lists may have one or more children of their own, and so on, to produce a **multilevel data structure** as shown in the example below.

Given the `head` of the first level of the list, **flatten** the list so that all the nodes appear in a single-level, doubly linked list. Let `curr` be a node with a child list. The nodes in the child list should appear **after** `curr` and **before** `curr.next` in the flattened list.

Return *the* `head` *of the flattened list. The nodes in the list must have **all** of their child pointers set to* `null`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/11/09/flatten11.jpg)

```
Input: head = [1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
Output: [1,2,3,7,8,11,12,9,10,4,5,6]
```

```py
class Solution(object):
    def flatten(self, head):
        """
        :type head: Node
        :rtype: Node
        """
        
        def dfs(head):
            while head:
                if head.child:
                    if head.next:
                        tail = dfs(head.child)
                        temp = head.next
                        temp.prev = tail
                        tail.next = temp
                        head.next = head.child
                        head.child.prev = head
                        head.child = None
                        head = tail
                    else:
                        head.next = head.child
                        head.child.prev = head
                        head.child = None
                if head.next:
                    head = head.next
                else:
                    break
            return head
        if not head:
            return 
        dfs(head)
        return head
        
```

\98. Validate Binary Search Tree

Medium

11023945Add to ListShare

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
#Brute Force
class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        """
        Inorder traversal, BST can be converted into a sorted array
        """
        def inorder(root):
            if not root:
                return []
            return inorder(root.left)+[root.val]+inorder(root.right)
        
        arr = inorder(root)
        for i in range(1, len(arr)):
            if arr[i] <= arr[i-1]:
                return False
        return True
    	
        """
        DFS inplace
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

\419. Battleships in a Board

Medium

1655794Add to ListShare

Given an `m x n` matrix `board` where each cell is a battleship `'X'` or empty `'.'`, return *the number of the **battleships** on* `board`.

**Battleships** can only be placed horizontally or vertically on `board`. In other words, they can only be made of the shape `1 x k` (`1` row, `k` columns) or `k x 1` (`k` rows, `1` column), where `k` can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/04/10/battelship-grid.jpg)

```
Input: board = [["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]
Output: 2
```

```py
class Solution(object):
    def countBattleships(self, board):
        """
        :type board: List[List[str]]
        :rtype: int
        """
        """
        DFS + VISITED
        """
        row, col = len(board), len(board[0])
        res = 0
        
        def dfs(board, i, j):
            board[i][j] = "."
            directions = [(1,0),(0,1),(-1,0),(0,-1)]
            for a,b in directions:
                if 0<=i+a<row and 0<=j+b<col and board[i+a][j+b] == "X":
                    dfs(board, i+a, j+b)
                
        for i in range(row):
            for j in range(col):
                if board[i][j] == "X":
                    res += 1
                    dfs(board, i, j)
        return res
```





#### BFS

##### basics

```py
#First create queue / and visited set
que = collections.deque()
visited = set()
//directions = [(0,1),(1,0), (-1,0), (0,-1)]
#append first case into que
que.append((x))
#BFS, while que, search the first poped ited in que, if found item, push into que
while que:
    cur = que.popleft()
    #if cur == what we want to find
    if res?:
        return 
    #if valid neibor found, push into que
    if ////:
        que.append(next)
#res not found, return -1
return baseCase
```

\100. Same Tree

Easy

6455147Add to ListShare

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

```
Input: p = [1,2,3], q = [1,2,3]
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
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if not p and not q:
            return True
        que = collections.deque()
        que.append((p,q))
        while que:
            temp1, temp2 = que.popleft()
            if temp1 == None and temp2 == None:
                continue
            elif temp1 == None or temp2 == None:
                return False
            else:
                if temp1.val != temp2.val:
                    return False
                que.append((temp1.left, temp2.left))
                que.append((temp1.right, temp2.right))
        return True
```

\101. Symmetric Tree

Easy

10255243Add to ListShare

Given the `root` of a binary tree, *check whether it is a mirror of itself* (i.e., symmetric around its center).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

```
Input: root = [1,2,2,3,4,4,3]
Output: true
```

```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        """
        BFS
        """
        if not root:
            return True
        que = collections.deque()
        que.append((root.left, root.right))
        while que:
            left, right = que.popleft()
            if left == None and right == None:
                continue
            elif left == None or right == None:
                return False
            elif left.val != right.val:
                return False
            que.append((left.left, right.right))
            que.append((left.right,right.left))
        return True
```

\117. Populating Next Right Pointers in Each Node II

Medium

4634267Add to ListShare

Given a binary tree

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/02/15/117_sample.png)

```
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

```py
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val=0, left=None, right=None, next=None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
"""

class Solution(object):
    def connect(self, root):
        """
        :type root: Node
        :rtype: Node
        BFS, but in each level we need to use DFS way
        """
        if not root:
            return
        que = collections.deque()
        que.append(root)
        while que:
            prev = None
            for i in range(len(que)):
                cur = que.popleft()
                if cur.left:
                    que.append(cur.left)
                if cur.right:
                    que.append(cur.right)
                if prev != None:
                    prev.next = cur
                prev = cur
            prev.next = None
        return root
```

\339. Nested List Weight Sum

Medium

1398316Add to ListShare

You are given a nested list of integers `nestedList`. Each element is either an integer or a list whose elements may also be integers or other lists.

The **depth** of an integer is the number of lists that it is inside of. For example, the nested list `[1,[2,2],[[3],2],1]` has each integer's value set to its **depth**.

Return *the sum of each integer in* `nestedList` *multiplied by its **depth***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/14/nestedlistweightsumex1.png)

```
Input: nestedList = [[1,1],2,[1,1]]
Output: 10
Explanation: Four 1's at depth 2, one 2 at depth 1. 1*2 + 1*2 + 2*1 + 1*2 + 1*2 = 10.
```

```py
class Solution(object):
    def depthSum(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        #BFS solution
         # initialize the queue
        queue = deque([[1, item] for item in nestedList])
        total = 0
        # bfs search and update total
        while queue:
            # pop left
            level, item = queue.popleft()
            # evaluate
            if item.isInteger():
                total += level * item.getInteger()
            else:
                # append the children
                for element in item.getList():
                    queue.append([level+1, element])
        return total
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
from collections import deque
class Solution(object):
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
```

\1091. Shortest Path in Binary Matrix

Medium

3712164Add to ListShare

Given an `n x n` binary matrix `grid`, return *the length of the shortest **clear path** in the matrix*. If there is no clear path, return `-1`.

A **clear path** in a binary matrix is a path from the **top-left** cell (i.e., `(0, 0)`) to the **bottom-right** cell (i.e., `(n - 1, n - 1)`) such that:

- All the visited cells of the path are `0`.
- All the adjacent cells of the path are **8-directionally** connected (i.e., they are different and they share an edge or a corner).

The **length of a clear path** is the number of visited cells of this path.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/18/example1_1.png)

```
Input: grid = [[0,1],[1,0]]
Output: 2
```

```py
class Solution(object):
    def shortestPathBinaryMatrix(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        BFS
        """
        
        #store que
        #store visited
        #initialize with top left
        que = collections.deque()
        que.append((0,0,1))
        row, col = len(grid), len(grid[0])
        
        while que:
            i,j,length = que.popleft()
            #if bottom right
            if i == row-1 and j == col-1 and grid[i][j] == 0:
                #return length
                return length
            #if valid and not visited and ==0:
            if 0<=i<row and 0<=j<col and grid[i][j] == 0:
                grid[i][j] = 1
                #add path into que and length+1
                que.append((i+1,j-1,length+1))
                que.append((i+1,j,length+1))
                que.append((i+1,j+1,length+1))
                que.append((i,j-1,length+1))
                que.append((i,j+1,length+1))
                que.append((i-1,j-1,length+1))
                que.append((i-1,j,length+1))
                que.append((i-1,j+1,length+1))
        return -1
```

\695. Max Area of Island

Medium

7440168Add to ListShare

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

```py
class Solution(object):
    def maxAreaOfIsland(self, grid):
        """
        BFS
        """
        #que to store bfs 
        #res to store 
        que = collections.deque()
        res = 0
        row,col = len(grid), len(grid[0])
        area = 0
        #BFS
        for i in range(row):
            for j in range(col):
                #if find an island 
                if grid[i][j] == 1:
                    que.append((i,j))
                    while que:
                        x,y = que.popleft()
                        if 0<=x<row and 0<=y<col and grid[x][y] == 1:
                            area += 1
                            grid[x][y] = 0
                            que.append((x+1,y))
                            que.append((x,y+1))
                            que.append((x-1,y))
                            que.append((x,y-1))
                    res = max(res,area)
                    area = 0
        return res
        
```

\1197. Minimum Knight Moves

Medium

1250358Add to ListShare

In an **infinite** chess board with coordinates from `-infinity` to `+infinity`, you have a **knight** at square `[0, 0]`.

A knight has 8 possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.

![img](https://assets.leetcode.com/uploads/2018/10/12/knight.png)

Return *the minimum number of steps needed to move the knight to the square* `[x, y]`. It is guaranteed the answer exists.

 

**Example 1:**

```
Input: x = 2, y = 1
Output: 1
Explanation: [0, 0] → [2, 1]
```

```py
class Solution(object):
    def minKnightMoves(self, x, y):
        """
        :type x: int
        :type y: int
        :rtype: int
        """
        """
        暴力BFS
        """
        que = collections.deque()
        que.append((0,0,0))
        moves = [(1,2),(2,1),(-1,-2),(-2,-1),(-1,2),(-2,1),(2,-1),(1,-2)]
        visited = set((0,0))
        x,y = abs(x),abs(y)
        while que:
            i,j,steps = que.popleft()
            if i == x and j == y:
                return steps
            for a,b in moves:
                if (i+a,j+b) not in visited and -1<=i+a<=x+2 and -1<=j+b<=y+2:
                    visited.add((i+a,j+b))
                    que.append((i+a,j+b,steps+1))
        return -1
```

\994. Rotting Oranges

Medium

7517288Add to ListShare

You are given an `m x n` `grid` where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return *the minimum number of minutes that must elapse until no cell has a fresh orange*. If *this is impossible, return* `-1`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

```py
class Solution(object):
    def orangesRotting(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        BFS
        """
        if not grid:
            return 0
        res = 0
        que = collections.deque()
        directions = [(0,1),(1,0),(0,-1),(-1,0)]
        visited = set()
        count = 0
        row, col = len(grid), len(grid[0])
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 2:
                    que.append((i,j,0))
                elif grid[i][j] == 1:
                    count += 1
 
        while que:
            x,y,time = que.popleft()
            grid[x][y] = 2
            for a,b in directions:
                if 0<=x+a<row and 0<=y+b<col and (x+a, y+b) not in visited and grid[x+a][y+b] == 1:
                    que.append((x+a,y+b,time+1))
                    visited.add((x+a, y+b))
            res = max(res,time)
        if len(visited) != count:
            return -1
        return res
```

\529. Minesweeper

Medium

1492898Add to ListShare

Let's play the minesweeper game ([Wikipedia](https://en.wikipedia.org/wiki/Minesweeper_(video_game)), [online game](http://minesweeperonline.com/))!

You are given an `m x n` char matrix `board` representing the game board where:

- `'M'` represents an unrevealed mine,
- `'E'` represents an unrevealed empty square,
- `'B'` represents a revealed blank square that has no adjacent mines (i.e., above, below, left, right, and all 4 diagonals),
- digit (`'1'` to `'8'`) represents how many mines are adjacent to this revealed square, and
- `'X'` represents a revealed mine.

You are also given an integer array `click` where `click = [clickr, clickc]` represents the next click position among all the unrevealed squares (`'M'` or `'E'`).

Return *the board after revealing this position according to the following rules*:

1. If a mine `'M'` is revealed, then the game is over. You should change it to `'X'`.
2. If an empty square `'E'` with no adjacent mines is revealed, then change it to a revealed blank `'B'` and all of its adjacent unrevealed squares should be revealed recursively.
3. If an empty square `'E'` with at least one adjacent mine is revealed, then change it to a digit (`'1'` to `'8'`) representing the number of adjacent mines.
4. Return the board when no more squares will be revealed.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/12/minesweeper_example_1.png)

```
Input: board = [["E","E","E","E","E"],["E","E","M","E","E"],["E","E","E","E","E"],["E","E","E","E","E"]], click = [3,0]
Output: [["B","1","E","1","B"],["B","1","M","1","B"],["B","1","1","1","B"],["B","B","B","B","B"]]
```

```py
class Solution(object):
    def updateBoard(self, board, click):
        """
        :type board: List[List[str]]
        :type click: List[int]
        :rtype: List[List[str]]
        """
        """
        BFS, start with click
        """
        #que to store next step
        que = collections.deque()
        que.append((click[0],click[1]))
        directions = [(1,0),(0,1),(1,1),(1,-1),(-1,1),(-1,-1),(-1,0),(0,-1)]
        row, col = len(board),len(board[0])
        
        while que:
            i, j = que.popleft()
            mineCount = 0
            #return if mine
            if board[i][j] == "M":
                board[i][j] = "X"
                return board
            #check digit and change value
            for a, b in directions:
                if 0<=i+a<row and 0<=j+b<col and board[i+a][j+b] == "M":
                    mineCount+=1 
            #if blank, reveal surrounding        
            if mineCount != 0:
                board[i][j] = str(mineCount)
            else:
                board[i][j] = "B"
                for a, b in directions:
                    if 0<=i+a<row and 0<=j+b<col and board[i+a][j+b] == "E":
                        que.append((i+a,j+b))
                        board[i+a][j+b] = "B"
                
        
        return board
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

\863. All Nodes Distance K in Binary Tree

Medium

6826132Add to ListShare

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
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
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

\286. Walls and Gates

Medium

251342Add to ListShare

You are given an `m x n` grid `rooms` initialized with these three possible values.

- `-1` A wall or an obstacle.
- `0` A gate.
- `INF` Infinity means an empty room. We use the value `231 - 1 = 2147483647` to represent `INF` as you may assume that the distance to a gate is less than `2147483647`.

Fill each empty room with the distance to *its nearest gate*. If it is impossible to reach a gate, it should be filled with `INF`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/03/grid.jpg)

```
Input: rooms = [[2147483647,-1,0,2147483647],[2147483647,2147483647,2147483647,-1],[2147483647,-1,2147483647,-1],[0,-1,2147483647,2147483647]]
Output: [[3,-1,0,1],[2,2,1,-1],[1,-1,2,-1],[0,-1,3,4]]
```

```py
class Solution(object):
    def wallsAndGates(self, rooms):
        """
        BFS
        """
        que = collections.deque()
        row, col = len(rooms), len(rooms[0])
        directions = [(0,1),(1,0),(0,-1),(-1,0)]
        #First put all gate into queue with distance 0
        for i in range(row):
            for j in range(col):
                if rooms[i][j] == 0:
                    que.append((i,j,0))
        
        #use BFS to mark each empty room with steps
        while que:
            #get current step
            x,y, steps = que.popleft()
            #do bfs on neibors
            for a,b in directions:
                if 0<=x+a<row and 0<=y+b<col and rooms[x+a][y+b] == 2147483647:
                    #mark steps on neibor
                    rooms[x+a][y+b] = steps+1
                    que.append((x+a,y+b,steps+1))
        return rooms
            
```

\934. Shortest Bridge

Medium

2933136Add to ListShare

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An **island** is a 4-directionally connected group of `1`'s not connected to any other `1`'s. There are **exactly two islands** in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form **one island**.

Return *the smallest number of* `0`*'s you must flip to connect the two islands*.

 

**Example 1:**

```
Input: grid = [[0,1],[1,0]]
Output: 1
```

```py
class Solution(object):
    def shortestBridge(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        """
        BFS
        """
        #first identify one islands using bfs
            #use visited set to record visited node 
        row,col = len(grid), len(grid[0])
        visited = set()
        que = collections.deque()
        directions = [(0,1),(1,0),(0,-1),(-1,0)]
        #for later BFS
        que2 = collections.deque()
        #first island found
        stop = False
        for i in range(row):
            if stop:
                break
            for j in range(col):
                if grid[i][j] == 1:
                    que.append((i,j))
                    visited.add((i,j))
                    stop = True
                    break
                    
            
        #find all first island
        while que:
            x,y = que.popleft()
            que2.append((x,y,0))
            for a,b in directions:
                if 0<=x+a<row and 0<=y+b<col and grid[x+a][y+b] == 1 and (x+a,y+b) not in visited:
                    que.append((x+a,y+b))
                    visited.add((x+a,y+b))
        
        #Do BFS on each island node, when find a node belongs to other island, return steps
        while que2:
            i,j,steps = que2.popleft()
            for a,b in directions:
                if 0<=i+a<row and 0<=j+b<col and (i+a,j+b) not in visited:
                    if grid[i+a][j+b] == 1:
                        return steps
                    que2.append((i+a,j+b,steps+1))
                    visited.add((i+a,j+b))
        
        return -1
```

\694. Number of Distinct Islands

Medium

1867110Add to ListShare

You are given an `m x n` binary matrix `grid`. An island is a group of `1`'s (representing land) connected **4-directionally** (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.

Return *the number of **distinct** islands*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/05/01/distinctisland1-1-grid.jpg)

```
Input: grid = [[1,1,0,0,0],[1,1,0,0,0],[0,0,0,1,1],[0,0,0,1,1]]
Output: 1
```

```py
class Solution(object):
    def numDistinctIslands(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        """
        BFS OR DFS
        """
        #BFS solutions:
        que = collections.deque()
        row, col = len(grid), len(grid[0])
        directions = [(0,1,"R"),(1,0,"U"),(-1,0,"D"),(0,-1,"L")]
        visited = set()
        islands = set()
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 1:
                    que.append((i,j))
                    visited.add((i,j))
                    finalRes = ""
                    while que:
                        x,y = que.popleft()
                        grid[x][y] = 0
                        for a,b,dire in directions:
                            if 0<=x+a<row and 0<=y+b<col and (x+a,y+b) not in visited and grid[x+a][y+b] == 1:
                                finalRes += dire
                                que.append((x+a,y+b))
                                visited.add((x+a,y+b))
                        ###
                        #Important part
                        ####
                        finalRes += "0"
                        ###
                        
                        ###
            
                    islands.add(finalRes)
                finalRes = ""
        return len(islands)
```

\787. Cheapest Flights Within K Stops

Medium

5462250Add to ListShare

There are `n` cities connected by some number of flights. You are given an array `flights` where `flights[i] = [fromi, toi, pricei]` indicates that there is a flight from city `fromi` to city `toi` with cost `pricei`.

You are also given three integers `src`, `dst`, and `k`, return ***the cheapest price** from* `src` *to* `dst` *with at most* `k` *stops.* If there is no such route, return `-1`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-3drawio.png)

```
Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
Output: 700
Explanation:
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.
```

```py
class Solution(object):
    def findCheapestPrice(self, n, flights, src, dst, k):
        """
        :type n: int
        :type flights: List[List[int]]
        :type src: int
        :type dst: int
        :type k: int
        :rtype: int
        """
        """
        BFS
        """
#         if not flights:
#             return -1
#         #create a map mapping each city to its dest
#         mapping = collections.defaultdict(list)
#         for i,j,money in flights:
#             mapping[i].append((j,money))
        
#         #from src do bfs, put in steps and money in tuple 
#             #if reach des and steps < k add into res 
#         que = collections.deque()
#         res = sys.maxint
#         que.append((src,0,0))
#         while que:
#             start, steps, cost = que.popleft()
#             if cost <= res and steps <= k and start != dst:
#                 for neibor, money in mapping[start]:
#                     que.append((neibor,steps+1,cost+money))
#             if start == dst:
#                 res = min(res,cost)
#         if res != sys.maxint:
#             return res
#         return -1
        # Build the adjacency matrix
        adj_matrix = [[0 for _ in range(n)] for _ in range(n)]
        for s, d, w in flights:
            adj_matrix[s][d] = w
            
        # Shortest distances dictionary
        distances = {}
        distances[(src, 0)] = 0
        
        # BFS Queue
        bfsQ = deque([src])
        
        # Number of stops remaining
        stops = 0
        ans = float("inf")
        
        # Iterate until we exhaust K+1 levels or the queue gets empty
        while bfsQ and stops < k + 1:
            
            # Iterate on current level
            length = len(bfsQ)
            for _ in range(length):
                node = bfsQ.popleft()
                
                # Loop over neighbors of popped node
                for nei in range(n):
                    if adj_matrix[node][nei] > 0:
                        dU = distances.get((node, stops), float("inf"))
                        dV = distances.get((nei, stops + 1), float("inf"))
                        wUV = adj_matrix[node][nei]
                        
                        # No need to update the minimum cost if we have already exhausted our K stops. 
                        if stops == k and nei != dst:
                            continue
                        
                        if dU + wUV < dV:
                            distances[nei, stops + 1] = dU + wUV
                            bfsQ.append(nei)
                            
                            # Shortest distance of the destination from the source
                            if nei == dst:
                                ans = min(ans, dU + wUV)
            stops += 1   
        
        return -1 if ans == float("inf") else ans
```

\785. Is Graph Bipartite?

Medium

5223284Add to ListShare

There is an **undirected** graph with `n` nodes, where each node is numbered between `0` and `n - 1`. You are given a 2D array `graph`, where `graph[u]` is an array of nodes that node `u` is adjacent to. More formally, for each `v` in `graph[u]`, there is an undirected edge between node `u` and node `v`. The graph has the following properties:

- There are no self-edges (`graph[u]` does not contain `u`).
- There are no parallel edges (`graph[u]` does not contain duplicate values).
- If `v` is in `graph[u]`, then `u` is in `graph[v]` (the graph is undirected).
- The graph may not be connected, meaning there may be two nodes `u` and `v` such that there is no path between them.

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every** edge in the graph connects a node in set `A` and a node in set `B`.

Return `true` *if and only if it is **bipartite***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/21/bi2.jpg)

```
Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
Output: false
Explanation: There is no way to partition the nodes into two independent sets such that every edge connects a node in one and a node in the other.
```

```py
class Solution(object):
    def isBipartite(self, graph):
        """
        :type graph: List[List[int]]
        :rtype: bool
        """
        """
        BFS each node, setting color of each node's neibors opposite of each node
        if see node with 
        """
        #colored to store color of node 
        colored = {}
        for i in range(len(graph)):
            
            #if not visited, mark color == 1 and put in BFS
            if i not in colored and graph[i]:
                colored[i] = 1
                que = collections.deque([i])
                
                #for each BFS check each neibor color and color in opposite color
                while que:
                    cur = que.popleft()
                    for j in graph[cur]:
                        if j not in colored:
                            colored[j] = -colored[cur]
                            que.append(j)
                        else:
                            #if same color for neibor, return false
                            if colored[cur] == colored[j]:
                                return False
        return True
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

\37. Sudoku Solver

Hard

5676163Add to ListShare

Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy **all of the following rules**:

1. Each of the digits `1-9` must occur exactly once in each row.
2. Each of the digits `1-9` must occur exactly once in each column.
3. Each of the digits `1-9` must occur exactly once in each of the 9 `3x3` sub-boxes of the grid.

The `'.'` character indicates empty cells.

 

**Example 1:**

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

```
Input: board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
Output: [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
```

```py
class Solution(object):
    def solveSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: None Do not return anything, modify board in-place instead.
        """

        self.backtracking(board, 0class Solution(object):
    def solveSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: None Do not return anything, modify board in-place instead.
        """
        #in place change
        self.backtracking(board, 0, 0)
        return
            
    def backtracking(self, board, i, j):
        #move to next valid one
        while board[i][j] != ".":
            j += 1
            if j == 9:
                i += 1
                j = 0
            #passes last row, all good
            if i == 9:
                return True
        
        #backtracking, try 1-9 on each slot, if valid, put it in and call backtracking on it
        for char in range(1, 10):
            if self.isValid(board, i, j, str(char)):
                board[i][j] = str(char)
                if self.backtracking(board, i, j):
                    return True
        board[i][j] = "."
        return False
       
    #test if num is valid in a slot of board  
    def isValid(self, board, i, j, num):
        for n in range(9):
            if board[n][j] == num:
                return False
            if board[i][n] == num:
                return False
            if board[(i/3)*3 + n/3][(j/3)*3 + n%3] == num:
                return False
        return True, 0)
        return
        
        
    def backtracking(self, board, i, j):
        while board[i][j] != ".":
            j += 1
            if j == 9:
                i += 1
                j = 0
            if i == 9:
                return True
        for char in range(1, 10):
            if self.isValid(board, i, j, str(char)):
                board[i][j] = str(char)
                if self.backtracking(board, i, j):
                    return True
        board[i][j] = "."
        return False
        
        
        
    def isValid(self, board, i, j, num):
        for n in range(9):
            if board[n][j] == num:
                return False
            if board[i][n] == num:
                return False
            if board[(i/3)*3 + n/3][(j/3)*3 + n%3] == num:
                return False
        return True
      
```

\22. Generate Parentheses

Medium

13737520Add to ListShare

Given `n` pairs of parentheses, write a function to *generate all combinations of well-formed parentheses*.

 

**Example 1:**

```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

```py
class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
#         res = []
#         paren = ""
#         self.backtrack(n, paren, res)
#         return res
        
#     def backtrack(self, n, paren, res):
#         a = b = 0
#         for i in paren:
#             if i == "(":
#                 a += 1
#             else:
#                 b += 1
#         if b > len(paren)/2 or a > n or b > n:
#             return
#         if len(paren) == n*2:
#             res.append(paren)
#             return
#         for i in ["(", ")"]:
#             self.backtrack(n, paren + i, res)
        def paren(left, right, curr, res):
			# 'evaluate current string
			# if we are out of brackets to add, we must be at a valid string
			if left == 0 and right == 0:
				res.append(curr)
				return

			# recursive call: add either open or close
			# if adding open bracket is valid
			if left > 0:
				# add open bracket, decr count
				paren(left-1, right, curr + "(", res)

			# if adding close bracket is valid
			if right > left:
				# add close bracket, decr count
				paren(left, right-1, curr + ")", res)

			return res
		# end paren()

        res = paren(n, n, '', [])

        return res
```



































### Greedy

<img src="https://camo.githubusercontent.com/daa3b49a8d3a274c8e595c01920394f9150f9aca9e96ca312d81b72cac98f0fa/68747470733a2f2f636f64652d7468696e6b696e672d313235333835353039332e66696c652e6d7971636c6f75642e636f6d2f706963732f32303231303931373130343331352e706e67" alt="贪心算法大纲" style="zoom:55%;" />

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

#### Knapsack problem

#### 序列问题

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
        # 贪心思想1 优先满足需求因子较小的孩子。因为如果较小需求的孩子无法被满足，则之后的较大的需求		更不可能能被满足了。
		#贪心思想2 尽量用较小的糖果去优先满足孩子。
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

\1005. Maximize Sum Of Array After K Negations

Easy

104982Add to ListShare

Given an integer array `nums` and an integer `k`, modify the array in the following way:

- choose an index `i` and replace `nums[i]` with `-nums[i]`.

You should apply this process exactly `k` times. You may choose the same index `i` multiple times.

Return *the largest possible sum of the array after modifying it in this way*.

 

**Example 1:**

```
Input: nums = [4,2,3], k = 1
Output: 5
Explanation: Choose index 1 and nums becomes [4,-2,3].
```

```py
class Solution(object):
    def largestSumAfterKNegations(self, nums, k):
        """
        greedy, changing from lowerst: if less than 0 change it,
        else: if k even return, if odd change then return
        """
        nums = sorted(nums)
        i = 0
        while(k > 0 and i<len(nums) and nums[i] < 0):
            nums[i] = -nums[i]
            i+=1
            k-=1
        if k%2 != 0:
            return sum(nums) - min(nums)*2
        return sum(nums)
        
```

\860. Lemonade Change

Easy

1320126Add to ListShare

At a lemonade stand, each lemonade costs `$5`. Customers are standing in a queue to buy from you and order one at a time (in the order specified by bills). Each customer will only buy one lemonade and pay with either a `$5`, `$10`, or `$20` bill. You must provide the correct change to each customer so that the net transaction is that the customer pays `$5`.

Note that you do not have any change in hand at first.

Given an integer array `bills` where `bills[i]` is the bill the `ith` customer pays, return `true` *if you can provide every customer with the correct change, or* `false` *otherwise*.

 

**Example 1:**

```
Input: bills = [5,5,5,10,20]
Output: true
Explanation: 
From the first 3 customers, we collect three $5 bills in order.
From the fourth customer, we collect a $10 bill and give back a $5.
From the fifth customer, we give a $10 bill and a $5 bill.
Since all customers got correct change, we output true.
```

```py
class Solution(object):
    def lemonadeChange(self, bills):
        """
        :type bills: List[int]
        :rtype: bool
        """
        five = ten = 0
        for num in bills:
            if num == 5:
                five += 1
            elif num == 10 and five:
                ten += 1
                five -= 1
            elif num == 20 and five and ten:
                five -= 1
                ten -= 1
            elif num == 20 and five >= 3:
                five -= 3
            else:
                return False
        return True
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

\738. Monotone Increasing Digits

Medium

96887Add to ListShare

An integer has **monotone increasing digits** if and only if each pair of adjacent digits `x` and `y` satisfy `x <= y`.

Given an integer `n`, return *the largest number that is less than or equal to* `n` *with **monotone increasing digits***.

 

**Example 1:**

```
Input: n = 10
Output: 9
```

```py
class Solution(object):
    def monotoneIncreasingDigits(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        Greedy, from first to last, if mono increase, copy number, if not
        down last by one and change cur to 9
        """
        n_str = str(n)
        len_n = len(n_str)
        for i in range(len_n-1, 0, -1):
            if int(n_str[i]) < int(n_str[i - 1]):
                n_str = str(int(n_str) - (int(n_str[i:]) + 1))
        return int(n_str)
```

#### 股票问题



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

\714. Best Time to Buy and Sell Stock with Transaction Fee

Medium

4266109Add to ListShare

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day, and an integer `fee` representing a transaction fee.

Find the maximum profit you can achieve. You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

 

**Example 1:**

```
Input: prices = [1,3,2,8,4,9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
- Buying at prices[0] = 1
- Selling at prices[3] = 8
- Buying at prices[4] = 4
- Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

```py
class Solution(object):
    def maxProfit(self, prices, fee):
        """
        :type prices: List[int]
        :type fee: int
        :rtype: int
        """
        """
        Greedy, if find a lower low, change low, if can make a profitable trade, then 
        sell and change low to tradevalue-fee because for [1,4, 10,14], 14-4-2is what we will miss
        """
        n = len(prices)
        if n < 2:
             return 0
        ans = 0
        minimum = prices[0]
        for i in range(1, n):
            if prices[i] < minimum:
                minimum = prices[i]
            elif prices[i] > minimum + fee:
                ans += prices[i] - fee - minimum
                minimum = prices[i] - fee
        return ans
        
```

#### 2D

\135. Candy

Hard

4452309Add to ListShare

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

Return *the minimum number of candies you need to have to distribute the candies to the children*.

 

**Example 1:**

```
Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
```

```py
class Solution(object):
    def candy(self, ratings):
        """
        :type ratings: List[int]
        :rtype: int
        """
        [1,2,3,1,3,2,1]
        #brute force: if larger add, if lower and less than 0 change all prev
        #O(2n): two array, one round from left and one round from right, take max
        #O(n): one round from left and one round from right, change in same array
        n = len(ratings)        
        res = [1]*n
        for i in range(1, n):
            #if larger:
            if ratings[i] > ratings[i-1]:
                res[i] = res[i-1]+1
        for i in range(n-2, -1, -1):
            if ratings[i] > ratings[i+1]:
                res[i] = max(res[i+1]+1, res[i])
        return sum(res)
```

\406. Queue Reconstruction by Height

Medium

6251637Add to ListShare

You are given an array of people, `people`, which are the attributes of some people in a queue (not necessarily in order). Each `people[i] = [hi, ki]` represents the `ith` person of height `hi` with **exactly** `ki` other people in front who have a height greater than or equal to `hi`.

Reconstruct and return *the queue that is represented by the input array* `people`. The returned queue should be formatted as an array `queue`, where `queue[j] = [hj, kj]` is the attributes of the `jth` person in the queue (`queue[0]` is the person at the front of the queue).

 

**Example 1:**

```
Input: people = [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
Output: [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]]
Explanation:
Person 0 has height 5 with no other people taller or the same height in front.
Person 1 has height 7 with no other people taller or the same height in front.
Person 2 has height 5 with two persons taller or the same height in front, which is person 0 and 1.
Person 3 has height 6 with one person taller or the same height in front, which is person 1.
Person 4 has height 4 with four people taller or the same height in front, which are people 0, 1, 2, and 3.
Person 5 has height 7 with one person taller or the same height in front, which is person 1.
Hence [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]] is the reconstructed queue.
```

```py
class Solution(object):
    def reconstructQueue(self, people):
        """
        :type people: List[List[int]]
        :rtype: List[List[int]]
        """
        """
        Greedy, first sort people in h and then in k, insert higher first and then
        insert lower accourding to their k and res[k] will be their position
        """
        people.sort(key = lambda x: (-x[0], x[1]))
        output = []
        for p in people:
            output.insert(p[1], p)
        return output
```

#### 区间问题

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
    
    	######
        
        if len(nums) == 1:
            return True
        step = 0
        maxStep = 0
        while step<len(nums) and maxStep >= step:
            
            maxStep = max(maxStep, step + nums[step])
            step += 1
        if step-1 >= len(nums)-1:
            return True
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

\452. Minimum Number of Arrows to Burst Balloons

Medium

3595105Add to ListShare

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose **horizontal diameter** stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up **directly vertically** (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is **burst** by an arrow shot at `x` if `xstart <= x <= xend`. There is **no limit** to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return *the **minimum** number of arrows that must be shot to burst all balloons*.

 

**Example 1:**

```
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].
```

```py
class Solution(object):
    def findMinArrowShots(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        """
        Greedy: sort list using first index, then check arr1[1] with arr2[0],
        if larger, then is contained in the same arrow, if smaller, update to the smallest width
        """
        n = len(points)
        arrow = 1
        points = sorted(points)
        i = 0
        for i in range(1,n):
            if points[i][0] > points[i-1][1]:
                arrow += 1
            else:
                points[i][1] = min(points[i - 1][1], points[i][1])
        return arrow
```

\435. Non-overlapping Intervals

Medium

4363130Add to ListShare

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return *the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping*.

 

**Example 1:**

```
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of the intervals are non-overlapping.
```

```py
class Solution(object):
    def eraseOverlapIntervals(self, intervals):
        """
        :type intervals: List[List[int]]
        :rtype: int
        """
        """
        难点一：一看题就有感觉需要排序，但究竟怎么排序，按左边界排还是右边界排。
        难点二：排完序之后如何遍历，如果没有分析好遍历顺序，那么排序就没有意义了。
        难点三：直接求重复的区间是复杂的，转而求最大非重复区间个数。
        难点四：求最大非重复区间个数时，需要一个分割点来做标记
        右边界排序之后，局部最优：优先选右边界小的区间，所以从左向右遍历，留给下一个区间的空          间大一些，从而尽量避免交叉。全局最优：选取最多的非交叉区间。
        """
        intervals = sorted(intervals, key = lambda x: x[1])
        count = 1
        end = intervals[0][1]
        for i in range(1, len(intervals)):
            if intervals[i][0] >= end:
                count += 1
                end = intervals[i][1]
        return len(intervals) - count 
```

\763. Partition Labels

Medium

8036305Add to ListShare

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be `s`.

Return *a list of integers representing the size of these parts*.

 

**Example 1:**

```
Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits s into less parts.
```

```py
class Solution(object):
    def partitionLabels(self, s):
        """
        :type s: str
        :rtype: List[int]
        """
        #first construct hashmap so we know the last of each number 
        hashmap = [0] * 26
        res = []
        for i in range(len(s)):
            hashmap[ord(s[i])-ord("a")] = i

        #loop and update the end index, if index == end, append index
        end = start = 0
        for i in range(len(s)):
            end = max(end, hashmap[ord(s[i])-ord("a")])
            if end == i:
                res.append(end-start+1)
                start = end+1
        
        return res

```

\56. Merge Intervals

Medium

14847548Add to ListShare

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return *an array of the non-overlapping intervals that cover all the intervals in the input*.

 

**Example 1:**

```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

```py
class Solution(object):
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

#### Hard

\134. Gas Station

Medium

6365634Add to ListShare

There are `n` gas stations along a circular route, where the amount of gas at the `ith` station is `gas[i]`.

You have a car with an unlimited gas tank and it costs `cost[i]` of gas to travel from the `ith` station to its next `(i + 1)th` station. You begin the journey with an empty tank at one of the gas stations.

Given two integer arrays `gas` and `cost`, return *the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return* `-1`. If there exists a solution, it is **guaranteed** to be **unique**

 

**Example 1:**

```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
Explanation:
Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4
Travel to station 4. Your tank = 4 - 1 + 5 = 8
Travel to station 0. Your tank = 8 - 2 + 1 = 7
Travel to station 1. Your tank = 7 - 3 + 2 = 6
Travel to station 2. Your tank = 6 - 4 + 3 = 5
Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3.
Therefore, return 3 as the starting index.
```

```py
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        """
        首先如果总油量减去总消耗大于等于零那么一定可以跑完一圈，说明 各个站点的加油站 剩油量rest[i]相加一定是大于等于零的。

每个加油站的剩余量rest[i]为gas[i] - cost[i]。

i从0开始累加rest[i]，和记为curSum，一旦curSum小于零，说明[0, i]区间都不能作为起始位置，起始位置从i+1算起，再从0计算curSum。
        """
        curSum = totalSum = start = 0
        for i in range(len(gas)):
            curSum += gas[i] - cost[i]
            totalSum += gas[i] - cost[i]
            if curSum < 0:
                curSum = 0
                start = i+1
        if totalSum < 0:
            return -1
        return start
```











### Union Find

#### Idea:

```java
class UF {
	// 记录连通分量个数
    private int count;
    // 存储若⼲棵树
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
    /* 将 p 和 q 连通 */
    public void union(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        if (rootP == rootQ):
        	return;
        // ⼩树接到⼤树下⾯，较平衡
        if (size[rootP] > size[rootQ]) {
            parent[rootQ] = rootP;
            size[rootP] += size[rootQ];
        } else {
            parent[rootP] = rootQ;
            size[rootQ] += size[rootP];
        }
        count--;
    }
    /* 判断 p 和 q 是否互相连通 */
    public boolean connected(int p, int q) {
        int rootP = find(p);
        int rootQ = find(q);
        // 处于同⼀棵树上的节点，相互连通
        return rootP == rootQ;
    }
    /* 返回节点 x 的根节点 */
    private int find(int x) {
        while (parent[x] != x) {
            // 进⾏路径压缩
            parent[x] = parent[parent[x]];
            x = parent[x];
        }
        return x;
    }
    public int count() {
    	return count;
    }
}
算法的关键点有 3 个：
1、⽤ parent 数组记录每个节点的⽗节点，相当于指向⽗节点的指针，所
以 parent 数组内实际存储着⼀个森林（若⼲棵多叉树）。
2、⽤ size 数组记录着每棵树的重量，⽬的是让 union 后树依然拥有平
衡性，⽽不会退化成链表，影响操作效率。
3、在 find 函数中进⾏路径压缩，保证任意树的⾼度保持在常数，使得
union 和 connected API 时间复杂度为 O(1)。

```

<img src="C:\Users\Simon\AppData\Roaming\Typora\typora-user-images\image-20220707234921099.png" alt="image-20220707234921099" style="zoom:33%;" />

\200. Number of Islands

Medium

14664344Add to ListShare

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
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        #union find 
        #first create count and parent[]
        row = len(grid)
        col = len(grid[0])
        
        self.count = sum(grid[i][j] == "1" for i in range(row) for j in range(col))
        parent = [i for i in range(row*col)]
        rank = [0] * row*col

        #define find and union
        def find(x):
            if parent[x] != x:
                parent[x] = find(parent[x])
            return parent[x]

        def union(i, j):
            rooti, rootj = find(i), find(j)
            if rooti == rootj:
                return
            if rank[i] > rank[j]:
                parent[rootj] = rooti
                rank[rooti] = max(rank[rooti], rank[rootj]+1)
            else:
                parent[rooti] = rootj
                rank[rootj] = max(rank[rootj], rank[rooti]+1)
            self.count -= 1
            return

        for i in range(row):
            for j in range(col):
                if grid[i][j] == "0":
                    continue
                grid[i][j] = "0"
                index = i*col + j
                if j < col-1 and grid[i][j+1] == "1":
                    union(index, index+1)
                if i < row-1 and grid[i+1][j] == "1":
                    union(index, index+col)
        return self.count
```

\547. Number of Provinces

Medium

5493245Add to ListShare

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return *the total number of **provinces***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

```
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2
```

```py
class Solution(object):
    def findCircleNum(self, isConnected):
        """
        :type isConnected: List[List[int]]
        :rtype: int
        """
        #union find
        #initialize count, parent
        row = len(isConnected)
        col = len(isConnected[0])
        self.count = row
        parent = [i for i in range(row)]
        
        
        #define find
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]
    
        #define union 
        def union(i, j):
            rooti, rootj = find(i), find(j)
            if rooti == rootj:
                return
            parent[rootj] = rooti
            self.count -= 1
            return
        
        for i in range(row):
            for j in range(col):
                print(self.count)
                if isConnected[i][j] == 1 and i != j:
                    union(i, j)
                    
        return self.count
        
```

\1319. Number of Operations to Make Network Connected

Medium

234434Add to ListShare

There are `n` computers numbered from `0` to `n - 1` connected by ethernet cables `connections` forming a network where `connections[i] = [ai, bi]` represents a connection between computers `ai` and `bi`. Any computer can reach any other computer directly or indirectly through the network.

You are given an initial computer network `connections`. You can extract certain cables between two directly connected computers, and place them between any pair of disconnected computers to make them directly connected.

Return *the minimum number of times you need to do this in order to make all the computers connected*. If it is not possible, return `-1`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/01/02/sample_1_1677.png)

```
Input: n = 4, connections = [[0,1],[0,2],[1,2]]
Output: 1
Explanation: Remove cable between computer 1 and 2 and place between computers 1 and 3.
```

```py
class Solution(object):
    def makeConnected(self, n, connections):
        """
        :type n: int
        :type connections: List[List[int]]
        :rtype: int
        """
        #union find:
        #since we only need n-1 cable to connect n comps, we can use union to connect
        #each computer, if we see the root of two comps are same, we have an extra cable
        #return -1 if extra < non-connected
        #return non-connected
        
        #initialize extra, parent, (rank)
        if len(connections) < n-1:
            return -1
        count = n
        parent = [i for i in range(n)]
        rank = [0] * n
        
        #find
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]
        
        #union    
        for i, j in connections:
            rooti, rootj = find(i), find(j)
            if rooti != rootj:
                if rank[rooti] > rank[rootj]:
                    rooti, rootj = rootj, rooti
                parent[rooti] = rootj 
                rank[rootj] = rank[rootj] + rank[rooti]
                count -= 1
        return count - 1
            
```

\990. Satisfiability of Equality Equations

Medium

167821Add to ListShare

You are given an array of strings `equations` that represent relationships between variables where each string `equations[i]` is of length `4` and takes one of two different forms: `"xi==yi"` or `"xi!=yi"`.Here, `xi` and `yi` are lowercase letters (not necessarily different) that represent one-letter variable names.

Return `true` *if it is possible to assign integers to variable names so as to satisfy all the given equations, or* `false` *otherwise*.

 

**Example 1:**

```
Input: equations = ["a==b","b!=a"]
Output: false
Explanation: If we assign say, a = 1 and b = 1, then the first equation is satisfied, but not the second.
There is no way to assign the variables to satisfy both equations.
```

```py
class Solution(object):
    def equationsPossible(self, equations):
        """
        :type equations: List[str]
        :rtype: bool
        """
        #union find
        parent = [i for i in range(26)]
        rank = [1] * 26
        hashset= set()
        
        #def find:
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]
        
        #first loop connext all =='s
        for i in equations:
            if i[1] == "=":
                rooti, rootj = find(ord(i[0]) - ord('a')), find(ord(i[3]) - ord('a'))
                if rooti != rootj:
                    if rank[rooti] > rank[rootj]:
                        rooti, rootj = rootj, rooti
                    parent[rooti] = rootj
                    rank[rootj] = rank[rooti] + rank[rootj]
                hashset.add(i[0])
                hashset.add(i[3])
        
        
        #second loop check all the != 
        for i in equations:
            if i[1] == "!":
                if i[0] == i[3]:
                    return False
                if i[0] not in hashset or i[3] not in hashset:
                    continue
                rooti, rootj = find(ord(i[0]) - ord('a')), find(ord(i[3]) - ord('a'))
                if rooti == rootj:
                    return False
        return True
```

\684. Redundant Connection

Medium

4004303Add to ListShare

In this problem, a tree is an **undirected graph** that is connected and has no cycles.

You are given a graph that started as a tree with `n` nodes labeled from `1` to `n`, with one additional edge added. The added edge has two **different** vertices chosen from `1` to `n`, and was not an edge that already existed. The graph is represented as an array `edges` of length `n` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the graph.

Return *an edge that can be removed so that the resulting graph is a tree of* `n` *nodes*. If there are multiple answers, return the answer that occurs last in the input.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/05/02/reduntant1-1-graph.jpg)

```
Input: edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```

```py
class Solution(object):
    def findRedundantConnection(self, edges):
        """
        :type edges: List[List[int]]
        :rtype: List[int]
        """
        #union find, if rooti == rootj, res打擂台
        parent = [i for i in range(len(edges)+1)]
        rank = [1] * (len(edges)+1)
        self.res = [0,0]
        
        #find
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]
        
        #union
        def union(i,j):
            rooti, rootj = find(i), find(j)
            if rooti == rootj:
                self.res[0] = i
                self.res[1] = j
            if rank[rooti] > rank[rootj]:
                rooti, rootj = rootj, rooti
            parent[rooti] = rootj
            rank[rootj] = rank[rooti] + rank[rootj]
            return
        
        for i,j in edges:
            union(i, j)
        return self.res
```

\128. Longest Consecutive Sequence

Medium

11801503Add to ListShare

Given an unsorted array of integers `nums`, return *the length of the longest consecutive elements sequence.*

You must write an algorithm that runs in `O(n)` time.

 

**Example 1:**

```
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

```py
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #union find but instead of parent[] use hashmap
        if len(nums) == 0:
            return 0
        self.res = 1
        parent = {}
        rank = {}
        for i in nums:
            parent[i] = i
            rank[i] = 1
        hashset = set()
        
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]
        
        #when updating rank, update res
        def union(i, j):
            rooti, rootj = find(i), find(j)
            if rank[rooti] > rank[rootj]:
                rooti, rootj = rootj, rooti
            parent[rooti] = rootj
            rank[rootj] = rank[rooti] + rank[rootj]
            self.res = max(self.res, rank[rootj])
            return
            
        for i in nums:
            if i not in hashset:
                hashset.add(i)
                if i-1 in hashset:
                    union(i, i-1)
                if i+1 in hashset:
                    union(i, i+1)
                    
        return self.res
```

\952. Largest Component Size by Common Factor

Hard

131186Add to ListShare

You are given an integer array of unique positive integers `nums`. Consider the following graph:

- There are `nums.length` nodes, labeled `nums[0]` to `nums[nums.length - 1]`,
- There is an undirected edge between `nums[i]` and `nums[j]` if `nums[i]` and `nums[j]` share a common factor greater than `1`.

Return *the size of the largest connected component in the graph*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/01/ex1.png)

```
Input: nums = [4,6,15,35]
Output: 4
```

```py
class Solution(object):
    def largestComponentSize(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        #union find:
        self.res = 1
        rank = {}
        hashmap = collections.defaultdict(list)
        parent = {}
        
        
        def find(x):
            if parent[x] != x:
                return find(parent[x])
            return parent[x]
        
        def union(i, j):
            rooti, rootj = find(i), find(j)
            if rooti == rootj:
                return
            if rank[rooti] > rank[rootj]:
                rooti, rootj = rootj, rooti
            parent[rooti] = rootj
            rank[rootj] = rank[rooti] + rank[rootj]
            self.res = max(self.res, rank[rootj]) 
             
            
        def find_set(x):
            for i in range(2, int(math.sqrt(x)) + 1):
                if x % i == 0:
                    return find_set(x//i) | set([i])
            return set([x])
            
            
        #first put all elements in nums in map associated with prime factor as key
        for i in nums:
            rank[i] = 1
            parent[i] = i
            set_prime = find_set(i)
            for j in set_prime:
                hashmap[j].append(i)
        
        #second connect all the elements in each key, while updating rank
        temp = -1
        for _, num in hashmap.items():
            for i in num:
                if temp == -1:
                    temp = i
                union(temp, i)
                temp = i
            temp = -1
        
        #return highest rank 
        return self.res
```



### Matrix

\54. Spiral Matrix

Medium

7631853Add to ListShare

Given an `m x n` `matrix`, return *all elements of the* `matrix` *in spiral order*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

```py
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        res = []
        if not matrix:
            return res
        rowStart, rowEnd = 0, len(matrix)-1
        colStart, colEnd = 0, len(matrix[0])-1
        while(rowStart<= rowEnd and colStart <= colEnd):
            for i in range(colStart, colEnd+1):
                res.append(matrix[rowStart][i])
            rowStart += 1
            for j in range(rowStart, rowEnd+1):
                res.append(matrix[j][colEnd])
            colEnd -= 1
            if colStart > colEnd or rowStart > rowEnd:
                break
            for i in range(colEnd, colStart-1, -1):
                res.append(matrix[rowEnd][i])
            rowEnd -= 1
            for j in range(rowEnd, rowStart-1, -1):
                res.append(matrix[j][colStart])
            colStart += 1
        return res
```

\59. Spiral Matrix II

Medium

3781184Add to ListShare

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```

```py
class Solution(object):
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        colStart, rowStart = 0, 0
        colEnd, rowEnd = n-1, n-1
        counter = 1
        res = [[0] * n for _ in range(n)]
        while colStart <= colEnd and rowStart <= rowEnd:
            for i in range(colStart, colEnd+1):
                res[rowStart][i] = counter
                counter += 1
            rowStart += 1
            for j in range(rowStart, rowEnd+1):
                res[j][colEnd] = counter
                counter += 1
            colEnd -= 1
            for i in range(colEnd, colStart-1, -1):
                res[rowEnd][i] = counter
                counter += 1
            rowEnd -= 1
            for j in range(rowEnd, rowStart-1, -1):
                res[j][colStart] = counter
                counter += 1
            colStart += 1
        return res
```

\73. Set Matrix Zeroes

Medium

7770509Add to ListShare

Given an `m x n` integer matrix `matrix`, if an element is `0`, set its entire row and column to `0`'s.

You must do it [in place](https://en.wikipedia.org/wiki/In-place_algorithm).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        
        int m = matrix.length;
        int n = matrix[0].length;
        Set<Integer> hash_seti = new HashSet<>();
        Set<Integer> hash_setj = new HashSet<>();
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(matrix[i][j] == 0){
                    hash_seti.add(i);
                    hash_setj.add(j);
                }
            }
        }
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(hash_seti.contains(i) || hash_setj.contains(j)){
                    matrix[i][j] = 0;
                }
            }
        }
    }
}
```





\

### Bitwise Operation

#### Background:

- 从现代计算机中所有的数据二进制的形式存储在设备中。即 0、1 两种状态，计算机对二进制数据进行的运算(+、-、*、/)都是叫位运算，即将符号位共同参与运算的运算。

- 所以，相比在代码中直接使用(+、-、*、/)运算符，合理的运用位运算更能显著提高代码在机器上的执行效率。

#### **位操作符**

- & 与运算 两个位都是 1 时，结果才为 1，否则为 0，如
    1 0 0 1 1 
  &  1 1 0 0 1 
  `------------------------------` 
    1 0 0 0 1 



- | 或运算 两个位都是 0 时，结果才为 0，否则为 1，如
    1 0 0 1 1 
  |   1 1 0 0 1 
  `------------------------------` 
    1 1 0 1 1 



- ^ 异或运算，两个位相同则为 0，不同则为 1，如
    1 0 0 1 1 
  ^  1 1 0 0 1 
  `-----------------------------` 
    0 1 0 1 0 



- ~ 取反运算，0 则变为 1，1 则变为 0，如
  ~   1 0 0 1 1 
  `-----------------------------` 
     0 1 1 0 0 



- << 左移运算，向左进行移位操作，高位丢弃，低位补 0，如

```text
int a = 8;
a << 3;
移位前：0000 0000 0000 0000 0000 0000 0000 1000
移位后：0000 0000 0000 0000 0000 0000 0100 0000
```

\>> 右移运算，向右进行移位操作，对无符号数，高位补 0，对于有符号数，高位补符号位，如

```text
unsigned int a = 8;
a >> 3;
移位前：0000 0000 0000 0000 0000 0000 0000 1000
移位后：0000 0000 0000 0000 0000 0000 0000 0001

int a = -8;
a >> 3;
移位前：1111 1111 1111 1111 1111 1111 1111 1000
移位前：1111 1111 1111 1111 1111 1111 1111 1111
```

#### **常见位运算问题**

##### 1. 位操作实现[乘除法](https://www.zhihu.com/search?q=乘除法&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A736472332})

- 数 a 向右移一位，相当于将 a 除以 2；数 a 向左移一位，相当于将 a 乘以 2

```text
int a = 2;
a >> 1; ---> 1
a << 1; ---> 4
```

##### 2. 位操作交货两数

- 位操作交换两数可以不需要第三个临时变量，虽然普通操作也可以做到，但是没有其效率高

```text
//普通操作
void swap(int &a, int &b) {
  a = a + b;
  b = a - b;
  a = a - b;
}

//位与操作
void swap(int &a, int &b) {
  a ^= b;
  b ^= a;
  a ^= b;
}
```

位与操作解释：第一步：a ^= b ---> a = (a^b); 

第二步：b ^= a ---> b = b^(a^b) ---> b = (b^b)^a = a

第三步：a ^= b ---> a = (a^b)^a = (a^a)^b = b

##### 3. 位操作判断[奇偶数](https://www.zhihu.com/search?q=奇偶数&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A736472332})

- 只要根据数的最后一位是 0 还是 1 来决定即可，为 0 就是偶数，为 1 就是奇数。

```text
if(0 == (a & 1)) {
 //偶数
}
```

##### 4. 位操作交换符号

- 交换符号将正数变成负数，负数变成正数

```text
int reversal(int a) {
  return ~a + 1;
}
```

整数取反加1，正好变成其对应的负数(补码表示)；负数取反加一，则变为其原码，即正数

##### 5. 位操作求绝对值

- 整数的绝对值是其本身，负数的绝对值正好可以对其进行取反加一求得，即我们首先判断其符号位（整数右移 31 位得到 0，负数右移 31 位得到 -1,即 [0xffffffff](https://www.zhihu.com/search?q=0xffffffff&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A736472332})），然后根据符号进行相应的操作

```text
int abs(int a) {
  int i = a >> 31;
  return i == 0 ? a : (~a + 1);
}
```

上面的操作可以进行优化，可以将 i == 0 的条件判断语句去掉。我们都知道符号位 i 只有两种情况，即 i = 0 为正，i = -1 为负。对于任何数与 0 异或都会保持不变，与 -1 即 0xffffffff 进行异或就相当于对此数进行取反,因此可以将上面三目元算符转换为((a^i)-i)，即整数时 a 与 0 异或得到本身，再减去 0，负数时与 0xffffffff 异或将 a 进行取反，然后在加上 1，即减去 i(i =-1)

```text
int abs2(int a) {
  int i = a >> 31;
  return ((a^i) - i);
}
```

##### 6. 位操作进行高低位交换

- 给定一个 16 位的无符号整数，将其高 8 位与低 8 位进行交换，求出交换后的值，如：

```text
34520的二进制表示：
10000110 11011000

将其高8位与低8位进行交换，得到一个新的二进制数：
11011000 10000110
其十进制为55430
```

从上面移位操作我们可以知道，只要将无符号数 a>>8 即可得到其高 8 位移到低 8 位，高位补 0；将 a<<8 即可将 低 8 位移到高 8 位，低 8 位补 0，然后将 a>>8 和 a<<8 进行或操作既可求得交换后的结果。

```text
unsigned short a = 34520;
a = (a >> 8) | (a << 8);
```

##### 7. 位操作进行二进制逆序

将无符号数的二进制表示进行逆序，求取逆序后的结果，如

```text
数34520的二进制表示：
10000110 11011000

逆序后则为：
00011011 01100001
它的十进制为7009
```

在字符串逆序过程中，可以从字符串的首尾开始，依次交换两端的数据。在二进制中使用位的高低位交换会更方便进行处理，这里我们分组进行多步处理。

- 第一步:以每 2 位为一组，组内进行高低位交换

```text
交换前： 10 00 01 10 11 01 10 00
交换后： 01 00 10 01 11 10 01 00
```

- 第二步：在上面的基础上，以每 4 位为 1 组，组内高低位进行交换

```text
交换前： 0100 1001 1110 0100
交换后： 0001 0110 1011 0001
```

- 第三步：以每 8 位为一组，组内高低位进行交换

```text
交换前： 00010110 10110001
交换后： 01100001 00011011
```

- 第四步：以每16位为一组，组内高低位进行交换

```text
交换前： 0110000100011011
交换后： 0001101101100001
```

对于上面的第一步，依次以 2 位作为一组，再进行组内高低位交换，这样处理起来比较繁琐，下面介绍另外一种方法进行处理。先分别取原数 10000110 11011000 的奇数位和偶数位，将空余位用 0 填充：

```text
原数：  10000110 11011000
奇数位： 10000010 10001000
偶数位： 00000100 01010000
```

再将奇数位右移一位，偶数位左移一位，此时将两个数据相或即可以达到奇偶位上数据交换的效果：

```text
原数：  10000110 11011000
奇数位右移一位： 0 10000010 1000100
偶数位左移一位：0000100 01010000 0
两数相或得到： 01001001 11100100
```

上面的方法用位操作可以表示为：

- 取a的奇数位并用 0 进行填充可以表示为：a & 0xAAAA
- 取a的偶数为并用 0 进行填充可以表示为：a & 0x5555 因此，上面的第一步可以表示为：
  a = ((a & 0xAAAA) >> 1) | ((a & 0x5555) << 1)
  同理，可以得到其第二、三和四步为：
  a = ((a & 0xCCCC) >> 2) | ((a & 0x3333) << 2)
  a = ((a & 0xF0F0) >> 4) | ((a & 0x0F0F) << 4)
  a = ((a & 0xFF00) >> 8) | ((a & 0x00FF) << 8)
  因此整个操作为：

```text
unsigned short a = 34520;

a = ((a & 0xAAAA) >> 1) | ((a & 0x5555) << 1);
a = ((a & 0xCCCC) >> 2) | ((a & 0x3333) << 2);
a = ((a & 0xF0F0) >> 4) | ((a & 0x0F0F) << 4);
a = ((a & 0xFF00) >> 8) | ((a & 0x00FF) << 8);
```

##### 8. 位操作统计二进制中 1 的个数

统计二进制1的个数可以分别获取每个二进制位数，然后再统计其1的个数，此方法效率比较低。这里介绍另外一种高效的方法，同样以 34520 为例，我们计算其 a &= (a-1)的结果：

- 第一次：计算前：1000 0110 1101 1000 计算后：1000 0110 1101 0000
- 第二次：计算前：1000 0110 1101 0000 计算后：1000 0110 1100 0000
- 第二次：计算前：1000 0110 1100 0000 计算后：1000 0110 1000 0000 我们发现，没计算一次二进制中就少了一个 1，则我们可以通过下面方法去统计：

```text
count = 0  
while(a){  
  a = a & (a - 1);  
  count++;  
} 
```

#### Problems

\191. Number of 1 Bits

Easy

3676856Add to ListShare

Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

**Note:**

- Note that in some languages, such as Java, there is no unsigned integer type. In this case, the input will be given as a signed integer type. It should not affect your implementation, as the integer's internal binary representation is the same, whether it is signed or unsigned.
- In Java, the compiler represents the signed integers using [2's complement notation](https://en.wikipedia.org/wiki/Two's_complement). Therefore, in **Example 3**, the input represents the signed integer. `-3`.

 

**Example 1:**

```
Input: n = 00000000000000000000000000001011
Output: 3
Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.
```

```py
class Solution(object):
    def hammingWeight(self, n):
        """
        :type n: int
        :rtype: int
        """
        count = 0  
        while n:
            n &= (n-1)
            count += 1
        return count
        
```

### LRU:

#### intro

![image-20220714183257068](C:\Users\zx616\AppData\Roaming\Typora\typora-user-images\image-20220714183257068.png)



![image-20220714183307436](C:\Users\zx616\AppData\Roaming\Typora\typora-user-images\image-20220714183307436.png)

### DP

#### DP解题过程

**对于动态规划问题，我将拆解为如下五步曲，这五步都搞清楚了，才能说把动态规划真的掌握了！**

1. 确定dp数组（dp table）以及下标的含义
2. 确定递推公式
3. dp数组如何初始化
4. 确定遍历顺序
5. 举例推导dp数组

**因为一些情况是递推公式决定了dp数组要如何初始化！**

后面的讲解中我都是围绕着这五点来进行讲解。

可能刷过动态规划题目的同学可能都知道递推公式的重要性，感觉确定了递推公式这道题目就解出来了。

其实 确定递推公式 仅仅是解题里的一步而已！

一些同学知道递推公式，但搞不清楚dp数组应该如何初始化，或者正确的遍历顺序，以至于记下来公式，但写的程序怎么改都通过不了。

#### Easy

\70. Climbing Stairs

Easy

13089391Add to ListShare

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

 

**Example 1:**

```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

```py
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        """
        Dp推导公式 dp[i] = dp[i-1] + dp[i-2]
        """
        if n <= 2:
            return n
        dp = [0]*(n+1)
        dp[1] = 1
        dp[2] = 2
        for i in range(3, n+1):
            dp[i] = dp[i-2] + dp[i-1]
        return dp[n]
```

\746. Min Cost Climbing Stairs

Easy

72331175Add to ListShare

You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return *the minimum cost to reach the top of the floor*.

 

**Example 1:**

```
Input: cost = [10,15,20]
Output: 15
Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.
```

```py
class Solution(object):
    def minCostClimbingStairs(self, cost):
        """
        :type cost: List[int]
        :rtype: int
        """
        """
        就是要不是第一步不花费，要不是最后一步不花费
        """
        n = len(cost)
        dp = [0]*(n+1)
        for i in range(2,n+1):
            dp[i] = min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2])
        return dp[n]
```

\62. Unique Paths

Medium

9906314Add to ListShare

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return *the number of possible unique paths that the robot can take to reach the bottom-right corner*.

The test cases are generated so that the answer will be less than or equal to `2 * 109`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
Input: m = 3, n = 7
Output: 28
```

```py
class Solution(object):
    def uniquePaths(self, m, n):
        """
        2d DP 
        """
        dp = [[0]*n]*m
        for i in range(m):
            for j in range(n):
                if i == 0:
                    dp[0][j] = 1
                elif j == 0:
                    dp[i][0] = 1
                else:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[m-1][n-1]
```

\63. Unique Paths II

Medium

5550398Add to ListShare

You are given an `m x n` integer array `grid`. There is a robot initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m-1][n-1]`). The robot can only move either down or right at any point in time.

An obstacle and space are marked as `1` or `0` respectively in `grid`. A path that the robot takes cannot include **any** square that is an obstacle.

Return *the number of possible unique paths that the robot can take to reach the bottom-right corner*.

The testcases are generated so that the answer will be less than or equal to `2 * 109`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)

```
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

```py
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        
        2D DP: if obstacke, change to -1
        while dp: if find -1, dont include 
        
        """
        row,col = len(obstacleGrid), len(obstacleGrid[0])
        dp = [[0 for _ in range(col)] for _ in range(row)]
        #initialize dp, first row+col
        for i in range(len(obstacleGrid)):
            if obstacleGrid[i][0] == 1:
                break
            else:
                dp[i][0] = 1
        for j in range(len(obstacleGrid[0])):
            if obstacleGrid[0][j] == 1:
                break
            else:
                dp[0][j] = 1
        #DP      
        for i in range(1,row):
            for j in range(1,col):
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0
                    continue
                else:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[row-1][col-1]
                    
```

\343. Integer Break

Medium

2971339Add to ListShare

Given an integer `n`, break it into the sum of `k` **positive integers**, where `k >= 2`, and maximize the product of those integers.

Return *the maximum product you can get*.

 

**Example 1:**

```
Input: n = 2
Output: 1
Explanation: 2 = 1 + 1, 1 × 1 = 1.
```

```py
class Solution(object):
    def integerBreak(self, n):
        """
        :type n: int
        :rtype: int
        dp, for each find the max of each combo or past combo
        
        """
        dp = [0 for _ in range(n+1)]
        dp[2] = 1
        for i in range(3, n+1):
            for j in range(1, i-1):
                dp[i] = max(dp[i], max(j*(i-j), j*(dp[i-j])))
        return dp[n]
        
```

#### 01背包问题

##### intro

![416.分割等和子集1](https://camo.githubusercontent.com/5c5af3f54a3503cdb989ab1c28e2933202a33259608c70af0e72db5a858f14e6/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303131373137313330373430372e706e67)

问能否能装满背包（或者最多装多少）：dp[j] = max(dp[j], dp[j - nums[i]] + nums[i]); ，对应题目如下：

- [动态规划：416.分割等和子集](https://programmercarl.com/0416.分割等和子集.html)
- [动态规划：1049.最后一块石头的重量 II](https://programmercarl.com/1049.最后一块石头的重量II.html)

问装满背包有几种方法：dp[j] += dp[j - nums[i]] ，对应题目如下：

- [动态规划：494.目标和](https://programmercarl.com/0494.目标和.html)
- [动态规划：518. 零钱兑换 II](https://programmercarl.com/0518.零钱兑换II.html)
- [动态规划：377.组合总和Ⅳ](https://programmercarl.com/0377.组合总和Ⅳ.html)
- [动态规划：70. 爬楼梯进阶版（完全背包）](https://programmercarl.com/0070.爬楼梯完全背包版本.html)

问背包装满最大价值：dp[j] = max(dp[j], dp[j - weight[i]] + value[i]); ，对应题目如下：

- [动态规划：474.一和零](https://programmercarl.com/0474.一和零.html)

问装满背包所有物品的最小个数：dp[j] = min(dp[j - coins[i]] + 1, dp[j]); ，对应题目如下：

- [动态规划：322.零钱兑换](https://programmercarl.com/0322.零钱兑换.html)
- [动态规划：279.完全平方数](https://programmercarl.com/0279.完全平方数.html)

![img](https://camo.githubusercontent.com/0f1e8c608f9f618ed4df4571907bcf5df1058e0a5b532bef8ed8f34425cee2d6/68747470733a2f2f636f64652d7468696e6b696e672d313235333835353039332e66696c652e6d7971636c6f75642e636f6d2f706963732f254538253833253843254535253843253835254539253937254145254539254132253938312e6a706567)

##### 二维dp数组01背包

<img src="https://camo.githubusercontent.com/76247d4a17bf2cb456d9e4ecce19800bd6524cd23d56ba42ad41841f878da6fc/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303131303130333030333336312e706e67" alt="动态规划-背包问题1" style="zoom:50%;" />

1. 确定递推公式

再回顾一下dp[i][j]的含义：从下标为[0-i]的物品里任意取，放进容量为j的背包，价值总和最大是多少。

那么可以有两个方向推出来dp[i][j]，

- **不放物品i**：由dp[i - 1][j]推出，即背包容量为j，里面不放物品i的最大价值，此时dp[i][j]就是dp[i - 1][j]。(其实就是当物品i的重量大于背包j的重量时，物品i无法放进背包中，所以被背包内的价值依然和前面相同。)
- **放物品i**：由dp[i - 1][j - weight[i]]推出，dp[i - 1][j - weight[i]] 为背包容量为j - weight[i]的时候不放物品i的最大价值，那么dp[i - 1][j - weight[i]] + value[i] （物品i的价值），就是背包放物品i得到的最大价值

所以递归公式：

```py
 dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);
```

2. dp数组如何初始化

**关于初始化，一定要和dp数组的定义吻合，否则到递推公式的时候就会越来越乱**。

首先从dp[i][j]的定义出发，如果背包容量j为0的话，即dp[i][0]，无论是选取哪些物品，背包价值总和一定为0。如图：

在看其他![动态规划-背包问题10](https://camo.githubusercontent.com/c3fce313bc37ddf8c0c3883d8eb9496fdaf32ea1970e36703f97bfa65be4bf4b/68747470733a2f2f636f64652d7468696e6b696e672e63646e2e626365626f732e636f6d2f706963732f2545352538412541382545362538302538312545382541372538342545352538382539322d25453825383325384325453525384325383525453925393725414525453925413225393831302e6a7067)情况。

状态转移方程 dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]); 可以看出i 是由 i-1 推导出来，那么i为0的时候就一定要初始化。

dp[0][j]，即：i为0，存放编号0的物品的时候，各个容量的背包所能存放的最大价值。

那么很明显当 j < weight[0]的时候，dp[0][j] 应该是 0，因为背包容量比编号0的物品重量还小。

当j >= weight[0]时，dp[0][j] 应该是value[0]，因为背包容量放足够放编号0物品。

代码初始化如下：

```
for (int j = 0 ; j < weight[0]; j++) {  // 当然这一步，如果把dp数组预先初始化为0了，这一步就可以省略，但很多同学应该没有想清楚这一点。
    dp[0][j] = 0;
}
// 正序遍历
for (int j = weight[0]; j <= bagweight; j++) {
    dp[0][j] = value[0];
}
```

那么问题来了，**先遍历 物品还是先遍历背包重量呢？**

**其实都可以！！ 但是先遍历物品更好理解**。

那么我先给出先遍历物品，然后遍历背包重量的代码。

```
// weight数组的大小 就是物品个数
for(int i = 1; i < weight.size(); i++) { // 遍历物品
    for(int j = 0; j <= bagweight; j++) { // 遍历背包容量
        if (j < weight[i]) dp[i][j] = dp[i - 1][j]; 
        else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);

    }
}
```

**先遍历背包，再遍历物品，也是可以的！（注意我这里使用的二维dp数组）**

例如这样：

```
// weight数组的大小 就是物品个数
for(int j = 0; j <= bagweight; j++) { // 遍历背包容量
    for(int i = 1; i < weight.size(); i++) { // 遍历物品
        if (j < weight[i]) dp[i][j] = dp[i - 1][j];
        else dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);
    }
}
```

**如果求组合数就是外层for循环遍历物品，内层for遍历背包**。

**如果求排列数就是外层for遍历背包，内层for循环遍历物品**。



##### 一维dp数组（滚动数组）

对于背包问题其实状态都是可以压缩的。

在使用二维数组的时候，递推公式：dp[i][j] = max(dp[i - 1][j], dp[i - 1][j - weight[i]] + value[i]);

**其实可以发现如果把dp[i - 1]那一层拷贝到dp[i]上，表达式完全可以是：dp[i][j] = max(dp[i][j], dp[i][j - weight[i]] + value[i]);**

**与其把dp[i - 1]这一层拷贝到dp[i]上，不如只用一个一维数组了**，只用dp[j]（一维数组，也可以理解是一个滚动数组）。

1. 确定dp数组的定义

在一维dp数组中，dp[j]表示：容量为j的背包，所背的物品价值可以最大为dp[j]。

1. 一维dp数组的递推公式

dp[j]为 容量为j的背包所背的最大价值，那么如何推导dp[j]呢？

dp[j]可以通过dp[j - weight[i]]推导出来，dp[j - weight[i]]表示容量为j - weight[i]的背包所背的最大价值。

dp[j - weight[i]] + value[i] 表示 容量为 j - 物品i重量 的背包 加上 物品i的价值。（也就是容量为j的背包，放入物品i了之后的价值即：dp[j]）

此时dp[j]有两个选择，一个是取自己dp[j] 相当于 二维dp数组中的dp[i-1][j]，即不放物品i，一个是取dp[j - weight[i]] + value[i]，即放物品i，指定是取最大的，毕竟是求最大价值，

所以递归公式为：

```
dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);
```

可以看出相对于二维dp数组的写法，就是把dp[i][j]中i的维度去掉了。

1. 一维dp数组如何初始化

**关于初始化，一定要和dp数组的定义吻合，否则到递推公式的时候就会越来越乱**。

dp[j]表示：容量为j的背包，所背的物品价值可以最大为dp[j]，那么dp[0]就应该是0，因为背包容量为0所背的物品的最大价值就是0。

那么dp数组除了下标0的位置，初始为0，其他下标应该初始化多少呢？

看一下递归公式：dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);

dp数组在推导的时候一定是取价值最大的数，如果题目给的价值都是正整数那么非0下标都初始化为0就可以了。

**这样才能让dp数组在递归公式的过程中取的最大的价值，而不是被初始值覆盖了**。

那么我假设物品价值都是大于0的，所以dp数组初始化的时候，都初始为0就可以了。

1. 一维dp数组遍历顺序

代码如下：

```
for(int i = 0; i < weight.size(); i++) { // 遍历物品
    for(int j = bagWeight; j >= weight[i]; j--) { // 遍历背包容量
        dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);

    }
}
```

**这里大家发现和二维dp的写法中，遍历背包的顺序是不一样的！**

二维dp遍历的时候，背包容量是从小到大，而一维dp遍历的时候，背包是从大到小。

为什么呢？

**倒序遍历是为了保证物品i只被放入一次！**。但如果一旦正序遍历了，那么物品0就会被重复加入多次！

\416. Partition Equal Subset Sum

Medium

8184128Add to ListShare

Given a **non-empty** array `nums` containing **only positive integers**, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

 

**Example 1:**

```
Input: nums = [1,5,11,5]
Output: true
Explanation: The array can be partitioned as [1, 5, 5] and [11].
```

```py
class Solution(object):
    def canPartition(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        DP 01backpack  problem: we want to find if any combination can have sum of sum(nums)/2 because that can create two subsets
        """
        if sum(nums)%2 == 1:
            return False
        target = sum(nums)/2
        dp = [0]*(target+1)
        for i in range(len(nums)):
            for j in range(target, nums[i]-1, -1):
                dp[j] = max(dp[j], dp[j-nums[i]] + nums[i])
        return dp[target] == target
```

\1049. Last Stone Weight II

Medium

230177Add to ListShare

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

We are playing a game with the stones. On each turn, we choose any two stones and smash them together. Suppose the stones have weights `x` and `y` with `x <= y`. The result of this smash is:

- If `x == y`, both stones are destroyed, and
- If `x != y`, the stone of weight `x` is destroyed, and the stone of weight `y` has new weight `y - x`.

At the end of the game, there is **at most one** stone left.

Return *the smallest possible weight of the left stone*. If there are no stones left, return `0`.

 

**Example 1:**

```
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
We can combine 2 and 4 to get 2, so the array converts to [2,7,1,8,1] then,
we can combine 7 and 8 to get 1, so the array converts to [2,1,1,1] then,
we can combine 2 and 1 to get 1, so the array converts to [1,1,1] then,
we can combine 1 and 1 to get 0, so the array converts to [1], then that's the optimal value.
```

```py
class Solution(object):
    def lastStoneWeightII(self, stones):
        """
        :type stones: List[int]
        :rtype: int
        First understand the question, we want to find the last stone weight so that
        involves hitting two stones. A piles of stones can be understood as two simmilar weight stones like 417, so just Use DP 01 backpack to find the left weight
        
        """
        n = sum(stones)
        target = n/2
        dp = [0] * (target+1)
        for i in range(len(stones)):
            for j in range(target, stones[i]-1, -1):
                dp[j] = max(dp[j], dp[j-stones[i]]+stones[i])
        return n - 2*dp[target]
        
```



求组合类问题的公式，都是类似这种：

```
dp[j] += dp[j - nums[i]]
```

\494. Target Sum

Medium

7483274Add to ListShare

You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

 

**Example 1:**

```
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

```py
class Solution(object):
    def findTargetSumWays(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        每个物品只能用一次！！！！！
        组合类背包问题 since add to a target, there will be a left and right part wehre:
        left - right = target, since right = sum - left:
        left = (target+sum)/2
        backpack weight = target
        each item weight = value = nums[i]
        
        """
        sums = sum(nums)
        n = (sums+target)/2
        if abs(target) > sums or (sums+target)%2 == 1:
            return 0
        dp = [0] * (n+1)
        dp[0] = 1
        for i in range(len(nums)):
            for j in range(n, nums[i]-1, -1):
                dp[j] += dp[j-nums[i]]
        return dp[n]
```

\474. Ones and Zeroes

Medium

4144396Add to ListShare

You are given an array of binary strings `strs` and two integers `m` and `n`.

Return *the size of the largest subset of `strs` such that there are **at most*** `m` `0`*'s and* `n` `1`*'s in the subset*.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

 

**Example 1:**

```
Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
Output: 4
Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.
```

```py
class Solution(object):
    def findMaxForm(self, strs, m, n):
        """
        :type strs: List[str]
        :type m: int
        :type n: int
        :rtype: int
        
        看见数组每个element只能用一次加上背包重量直接想到dp01背包问题
        二位数组用mn做ij
        dp[i][j] = max(dp[i][j], dp[i-zero][j-one]+1)
        """
        dp = [[0]*(m+1) for _ in range(n+1)]
        for x in strs:
            zeroCount = x.count("0")
            oneCount = x.count("1")
            for i in range(n, oneCount-1, -1):
                for j in range(m, zeroCount-1, -1):
                    dp[i][j] = max(dp[i][j], dp[i-oneCount][j-zeroCount]+1)
        return dp[n][m] 

        
```

##### 完全背包

我们知道01背包内嵌的循环是从大到小遍历，为了保证每个物品仅被添加一次。

而完全背包的物品是可以添加多次的，所以要从小到大去遍历，即：

```
// 先遍历物品，再遍历背包
for(int i = 0; i < weight.size(); i++) { // 遍历物品
    for(int j = weight[i]; j <= bagWeight ; j++) { // 遍历背包容量
        dp[j] = max(dp[j], dp[j - weight[i]] + value[i]);

    }
}
```

\518. Coin Change 2

Medium

5644111Add to ListShare

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the number of combinations that make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `0`.

You may assume that you have an infinite number of each kind of coin.

The answer is **guaranteed** to fit into a signed **32-bit** integer.

 

**Example 1:**

```
Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: there are four ways to make up the amount:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```

```py
class Solution(object):
    def change(self, amount, coins):
        """
        :type amount: int
        :type coins: List[int]
        :rtype: int
        
        一个array有重量、价值，一个背包，马上想到DP
        因为每个element可以用无数次，是完全背包问题
        """
        dp = [0] * (amount+1)
        dp[0] = 1
        for i in range(len(coins)):
            for j in range(coins[i], amount+1):
                dp[j] += dp[j-coins[i]]
        return dp[amount]
```

\377. Combination Sum IV

Medium

3740423Add to ListShare

Given an array of **distinct** integers `nums` and a target integer `target`, return *the number of possible combinations that add up to* `target`.

The test cases are generated so that the answer can fit in a **32-bit** integer.

 

**Example 1:**

```
Input: nums = [1,2,3], target = 4
Output: 7
Explanation:
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
```

```py
class Solution(object):
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        如果求组合数就是外层for循环遍历物品，内层for遍历背包。
        如果求排列数就是外层for遍历背包，内层for循环遍历物品。
        target is backpack， n items to put in
        """
        dp = [0] * (target + 1)
        dp[0] = 1
        for i in range(1, target+1):
            for j in nums:
                if i >= j:
                    dp[i] += dp[i-j]
        return dp[target]
```

\322. Coin Change

Medium

12890289Add to ListShare

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return *the fewest number of coins that you need to make up that amount*. If that amount of money cannot be made up by any combination of the coins, return `-1`.

You may assume that you have an infinite number of each kind of coin.

 

**Example 1:**

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

```py
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        each can use infinite time, 完全背包
        排列问题
        dp[i] = fewest length to fill i
        dp[i] = min(dp[i], dp[i-j]+1)
        [0,1,2,3,4,5]
        for backpack:
            for item
        
        """
        dp = [sys.maxint] * (amount+1)
        dp[0] = 0
        for i in range(1,amount+1):
            for j in coins:
                if i>=j:
                    dp[i] = min(dp[i], dp[i-j]+1)
        if dp[amount] == sys.maxint:
            return -1
        return dp[amount]
```

\279. Perfect Squares

Medium

7124310Add to ListShare

Given an integer `n`, return *the least number of perfect square numbers that sum to* `n`.

A **perfect square** is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and `16` are perfect squares while `3` and `11` are not.

 

**Example 1:**

```
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```

```py
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        DP完全背包
        dp[i] = i最小能有几个ps
        dp[i] = min(dp[i], dp[i-j]+1)\
        [0,!,!,!,!]
        doesnt matter what order
        """
        dp = [sys.maxint] * (n+1)
        dp[0] = 0
        for i in range(1,n+1):
            for j in range(1,int(math.sqrt(n))+1):
                if i>=j*j:
                    dp[i] = min(dp[i], dp[i-j*j]+1)
        return dp[n]
        
```

#### House Robbing

\198. House Robber

Medium

13501280Add to ListShare

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

 

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

```py
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        Robbing, DP
        dp[i] = max for house i
        dp[1:2] = nums[1:2]
        dp[i] = max(dp[i-3]+nums[i], dp[i-2]+nums[i])
        left to right
        for i in dp[]
            for j in nums
        [2,7,9,3,1]
        [0,2,7,11,10,12]
        return max(dp[-1],dp[-2])
        """
        if len(nums) == 1:
            return nums[0]
        dp = [0] * (len(nums)+1)
        dp[1] = nums[0]
        dp[2] = nums[1]
        for i in range(3, len(nums)+1):
            dp[i] = max(dp[i-3]+nums[i-1], dp[i-2]+nums[i-1])
        return max(dp[-1],dp[-2])
```

\213. House Robber II

Medium

624797Add to ListShare

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return *the maximum amount of money you can rob tonight **without alerting the police***.

 

**Example 1:**

```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
```

```py
class Solution(object):
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        two cases, either rob first, or rob last
        dp[i] = max for house i
        dp[1:2] = nums[1:2]
        dp[i] = max(dp[i-1], dp[i-2]+nums[i])
        left to right
        for i in dp[]
            for j in nums
        return max(dp[-1],dp[-2])
        """
        if len(nums) == 1:
            return nums[0]
        if len(nums) == 2:
            return max(nums[0], nums[1])
        res1 = self.helper(nums, 0, len(nums)-2)
        res2 = self.helper(nums, 1, len(nums)-1)
        return max(res1, res2)
    
    def helper(self,nums,start,end):
        dp = [0] * len(nums)
        dp[start] = nums[start]
        dp[start+1] = max(nums[start], nums[start + 1])
        for i in range(start+1, end+1):
            dp[i] = max(dp[i-1], dp[i-2]+nums[i])
        return max(dp[-1], dp[-2])
```

\337. House Robber III

Medium

656597Add to ListShare

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called `root`.

Besides the `root`, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if **two directly-linked houses were broken into on the same night**.

Given the `root` of the binary tree, return *the maximum amount of money the thief can rob **without alerting the police***.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/10/rob1-tree.jpg)

```
Input: root = [3,2,3,null,3,null,1]
Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

```py
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        树状DP， 因为要从地下往上算最多偷多少，DFS后序
        DP[0] = 不偷最多多少
        Dp[1] = 偷最多多少
        """
        res = self.helper(root)
        return max(res[0], res[1])
    
    def helper(self, root):
        if not root:
            return [0,0]
        left = self.helper(root.left)
        right = self.helper(root.right)
        #不偷此节点，可偷可不偷子节点
        leftMax = max(left[1], left[0]) + max(right[1], right[0])
        #偷此节点，加上子节点的子节点
        rightMax = root.val + left[0] + right[0]
        return [leftMax, rightMax]
```

#### 股票(暂时没懂，三维？)

\121. Best Time to Buy and Sell Stock

Easy

18159583Add to ListShare

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

 

**Example 1:**

```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

```py
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        If have to solve with dp way
        dp[i][0] = money have if we hold stock
        dp[i][1] = money have if we dont hold stock
        dp[i][0] = max(dp[i-1][0], -prices[i])
        dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i]) 
        """
        n = len(prices)
        if n == 1:
            return 0
        dp = [[0,0],[0,0]]
        dp[0][0] = -prices[0]
        for i in range(1, n):
            #如果第i天持有股票即dp[i][0]， 那么可以由两个状态推出来
                #第i-1天就持有股票，那么就保持现状，所得现金就是昨天持有股票的所得现金 即：dp[i - 1][0]
                #第i天买入股票，所得现金就是买入今天的股票后所得现金即：-prices[i]
            #dp[i][0] = max(dp[i-1][0], -prices[i])
            dp[i % 2][0] = max(dp[(i - 1) % 2][0], -prices[i])
            
            #如果第i天不持有股票即dp[i][1]， 也可以由两个状态推出来
                #第i-1天就不持有股票，那么就保持现状，所得现金就是昨天不持有股票的所得现金 即：dp[i - 1][1]
                #第i天卖出股票，所得现金就是按照今天股票佳价格卖出后所得现金即：prices[i] + dp[i - 1][0]
            #dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i]) 
            dp[i % 2][1] = max(dp[(i - 1) % 2][1], prices[i] + dp[(i - 1) % 2][0])
        
        return dp[(n - 1) % 2][1]
```

\122. Best Time to Buy and Sell Stock II

Medium

83512412Add to ListShare

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

```py
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        """
        Greedy, form start, if less than prev, record res, else continue
        res, low = 0, 0
        for i in range(len(prices)-1):
            temp = prices[i+1] - prices[i]
            if temp > 0:
                res += temp
        
        return res
        """

        
        """
        2D DP
        DP[i][0] = if we hold stock, how much cash we have
        DP[i][1] = if we sell stock, how much cash we have
        Dp[i][0] = max(dp[i-1][0], dp[i-1][1]-prices[i])
        dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i])
        dp[0][0] = -prices[0]
        """
        n = len(prices)
        dp = [[0,0] for _ in range(n)]
        dp[0][0] = -prices[0]
        for i in range(1, n):
            #is it more to hold or sell and add the profit 
            dp[i][0] = max(dp[i-1][0], dp[i-1][1]-prices[i])
            #should we not sell or sell at current value 
            dp[i][1] = max(dp[i-1][1], dp[i-1][0] + prices[i])
        return dp[n-1][1]
```

#### 子序列

##### 不连续

##### 连续

##### 编辑距离

##### 回文





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
