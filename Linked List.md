链表的本质就是一组节点，每个节点包含两个部分：数据域（value）和指针域(pointer). 对链表的大部分操作都是对指针的操作。

一个节点的next是指它的指针域，是存储着链表中下一个节点的地址的部分。

**206. Reverse Linked List**
Given the head of a singly linked list, reverse the list, and return the reversed list.
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
递归解法，主要思路如下：

判断头节点是否为空或链表是否只有一个节点，如果是，则直接返回原链表头节点。

递归调用reverseList方法，传入头节点的下一个节点，即head.next作为新的头节点。

```next.next = head```将当前头节点head的下一个节点的next指针指向当前头节点head，实现翻转。

将当前头节点head的next指针置为空，因为当前头节点成为了翻转后的尾节点。

返回新的头节点newHead，即原链表的尾节点，即为翻转后的头节点。

通过递归调用实现链表翻转的主要思路是不断将链表分成前半段和后半段，对后半段进行翻转，然后再将前半段与翻转后的后半段连接起来。这种递归思想在链表操作中很常见，也是链表操作中比较优秀的解法之一。

