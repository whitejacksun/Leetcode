链表的本质就是一组节点，每个节点包含两个部分：数据域（value）和指针域(pointer). 对链表的大部分操作都是对指针的操作。

一个节点的next是指它的指针域，是存储着链表中下一个节点的地址的部分。

***206. Reverse Linked List***

Given the ```head``` of a singly linked list, reverse the list, and return the reversed list.

**递归解法：**
```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null)return head;
        ListNode res = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return res;
    }
}
```
主要思路如下：

检查链表头是否为空或只有一个节点，如果是，则直接返回头节点。

如果链表有两个或更多节点，递归调用reverseList函数，将头节点的下一个节点作为参数传递给它。

进行迭代，当符合停止条件时，即```（head.next) == null ||（head.next).next == null```此时head位于倒数第二个节点

将head的下一个节点的next指针指向头节点head。

将head的next指针设置为空，断开原来的链接。

一步步归来，res从倒数第二个逐渐回到原始的头节点。

通过递归调用实现链表翻转的主要思路是不断将链表分成前半段和后半段，对后半段进行翻转，然后再将前半段与翻转后的后半段连接起来。这种递归思想在链表操作中很常见，也是链表操作中比较优秀的解法之一。

**迭代解法：**
```java
class Solution {
    public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    ListNode next = null;
    while(curr != null){
        next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
    }
}
```

**头插法(Head Insertion)** python
```python
class ListNode(object):
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        newhead = ListNode(-1)
        while head:
            next = head.next
            head.next = newhead.next
            newhead.next = head
            head = next
        return newhead.next
```

***21. Merge Two Sorted Lists***

You are given the ```heads``` of two **sorted** linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

**迭代：**
```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode res = new ListNode();
        ListNode curr = res;
        while(list1 != null && list2 != null){
            if(list1.val < list2.val){
                curr.next = list1;
                list1 = list1.next;
            }
            else{
                curr.next = list2;
                list2 = list2.next;
            }
            curr = curr.next;
        }
        curr.next =  list1 == null?list2:list1;
        return res.next;
    }
}
```

***83. Remove Duplicates from Sorted List***

Given the ```head``` of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list **sorted** as well.

**递归：**
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode curr = head;
        while(curr.next != null){
            if(curr.val == curr.next.val){
                curr.next = curr.next.next;
            }
            else{
                curr = curr.next;
            }
        }
        return head;
    }
}
```
递归解法比较通俗易懂。

***19. Remove Nth Node From End of List***

Given the ```head``` of a linked list, remove the ```nth``` node from the end of the list and return its head.

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode slow = head;
        ListNode fast = head;
        for(int i=0;i<n;i++){
            fast = fast.next;
        }
        if(fast == null)return slow.next;
        while(fast.next != null){
            slow = slow.next;
            fast = fast.next;
        }
        slow.next = slow.next.next;
        return head;
    }
}
```

***445. Add Two Numbers II***

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

难点是需要进位，并且是给自己的prev节点进位。因此选择将两个链表倒置方便求和。记得最后return的时候要倒置回去。

```java
class Solution {
    public ListNode reverse(ListNode head){
        if(head == null || head.next == null)return head;
        ListNode newhead = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return newhead;
    }
    
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode curr1 = reverse(l1);
        ListNode curr2 = reverse(l2);
        ListNode res = new ListNode(0);
        ListNode dummy = res; 
        boolean flag = false;
        while(curr1 != null || curr2 != null){
            int sum = (curr1 != null ? curr1.val : 0) + (curr2 != null ? curr2.val : 0) + (flag ? 1 : 0);
            res.next = new ListNode(sum % 10);
            flag = sum >= 10;
            res = res.next;
            curr1 = curr1 != null ? curr1.next : null;
            curr2 = curr2 != null ? curr2.next : null;
        }
        if (flag) res.next = new ListNode(1); 
        return reverse(dummy.next);
    }
}
```

***24. Swap Nodes in Pairs***

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

因为是两两成对进行swap，因此swap之后，pair中靠后的那个节点的next也需要改变（因为下一个pair也变了），因此使用dummy node方便改变。需要注意的是swap之后两个节点的顺序已经变了，因此是curr = slow，因为slow是改变后靠后的那个节点。

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode pummy = new ListNode(-1);
        pummy.next = head;
        ListNode curr = pummy;
        while(curr.next != null && curr.next.next != null){
            ListNode slow = curr.next;
            ListNode fast = curr.next.next;
            slow.next = fast.next;
            fast.next = slow;
            curr.next = fast;

            curr = slow;
        }
        return pummy.next;
    }
}
```

***234. Palindrome Linked List***

Given the ```head``` of a singly linked list, return ```true``` if it is a palindrome or ```false``` otherwise.

暴力&蠢 解法: 时间和空间都在out的边缘。先复制一份链表，然后将原链表倒置与复制的比较。（因为倒置过程中会把原列表改变，[1,2,3,2,1]会变成[1,null]）

```java
class Solution {
    public ListNode reverse(ListNode head){
        if(head == null || head.next == null)return head;
        ListNode res = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return res;
    }

    
    public ListNode copy(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode copyHead = new ListNode(head.val);
        ListNode copyNode = copyHead;
        ListNode originalNode = head.next;
        while (originalNode != null) {
            ListNode newNode = new ListNode(originalNode.val);
            copyNode.next = newNode;
            copyNode = copyNode.next;
            originalNode = originalNode.next;
        }
        return copyHead;
    }


    public boolean isPalindrome(ListNode head) {
        ListNode copy = copy(head);       
        ListNode re = reverse(head);
        while (copy != null && copy.next != null){
            if(copy.val != re.val) {return false;}
            else{
                re = re.next;
                copy = copy.next;
            }
        }
        return true;
    }
}
```
