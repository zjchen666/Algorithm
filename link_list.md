Sort a linked list in O(n log n) time using constant space complexity.

Example
Given 1->3->2->null, sort it to 1->2->3->null.
### 思路 ###
    + 要求 O(nlgn)的时间复杂度，使用mergeSort，快慢指针找到终点。
    + 每次二分完成要断成两个链表
```python
"""
Definition of ListNode
class ListNode(object):

    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""
class Solution:
    """
    @param: head: The head of linked list.
    @return: You should return the head of the sorted linked list, using constant space complexity.
    """
    def sortList(self, head):
        # write your code here
        if not head:
            return None
        return self.mergeSort(head)

    def mergeSort(self, head):
        if head == None or head.next == None:
            return head

        fast = head
        slow = head
        while fast.next != None and fast.next.next != None:
            fast = fast.next.next
            slow = slow.next
        mid = slow.next
        slow.next = None

        list1 = self.mergeSort(head)
        list2 = self.mergeSort(mid)
        return self.mergeList(list1, list2)
        
    def mergeList(self, list1, list2):
        if list1 == None:
            return list2
        if list2 == None:
            return list1

        dummy = ListNode(0)
        head = dummy

        while list1 != None and list2 != None:
            if list1.val < list2.val:
                head.next = list1
                list1 = list1.next
            else:
                head.next = list2
                list2 = list2.next
            head = head.next

        if list1 != None:
            head.next = list1
        if list2 != None:
            head.next = list2
        return dummy.next
```
### QuickSort 解法 ###
    + 不用midList行么？
```python
    def quickSort(self, head):
        if head == None or head.next == None:
            return head

        fast = head
        slow = head
        while fast.next != None and fast.next.next != None:
            fast = fast.next.next
            slow = slow.next
        mid = slow.next

        dummy = ListNode(0)
        midDummy = ListNode(0)
        leftDummy = ListNode(0)
        rightDummy = ListNode(0)
        left = leftDummy
        right = rightDummy
        midList = midDummy
        while head != None:
            if head.val > mid.val:
                right.next = head
                right = right.next
            elif head.val < mid.val:
                left.next = head
                left = left.next
            else:
                midList.next = head
                midList = midList.next
            head = head.next
        midList.next = None
        left.next = None
        right.next = None

        llist = self.quickSort(leftDummy.next)
        rlist = self.quickSort(rightDummy.next)

        l = dummy
        l.next = llist
        while l.next != None:
            l = l.next
        l.next = midDummy.next
        while l.next != None:
            l = l.next
        l.next = rlist
        
        return dummy.next
```
## 反转单向链表 ## 
   ### 方法1 ### 
   创建新链表， 遍历旧链表，不断向新链表头插入。1->2->3->4, 2->1->3->4, 3->2->1->4, 4->3->2->1
   ### 方法2 ### 
   遍历旧链表，不断向链表头插入当前节点的下一个节点。1->2->3->4, 2->1->3->4, 3->2->1->4, 4->3->2->1