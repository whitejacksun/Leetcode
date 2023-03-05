链表的本质就是一组节点，每个节点包含两个部分：数据域（value）和指针域(pointer). 对链表的大部分操作都是对指针的操作。

一个节点的next是指它的指针域，是存储着链表中下一个节点的地址的部分。

***206. Reverse Linked List***

Given the head of a singly linked list, reverse the list, and return the reversed list.

**迭代解法：**
```java
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) {
        return head;
    }
    ListNode next = head.next;
    ListNode newHead = reverseList(next);
    next.next = head;
    head.next = null;
    return newHead;
}
```
主要思路如下：

检查链表头是否为空或只有一个节点，如果是，则直接返回头节点。

如果链表有两个或更多节点，递归调用reverseList函数，将头节点的下一个节点作为参数传递给它。此时，newHead变量将保存原链表的尾部节点，即反转后链表的头部节点。

将头节点的下一个节点next的next指针指向头节点head，这将把头节点和下一个节点反转过来。

将头节点head的next指针设置为空，断开原来的链接。

返回新的头节点newHead

通过递归调用实现链表翻转的主要思路是不断将链表分成前半段和后半段，对后半段进行翻转，然后再将前半段与翻转后的后半段连接起来。这种递归思想在链表操作中很常见，也是链表操作中比较优秀的解法之一。

**递归解法：**
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

