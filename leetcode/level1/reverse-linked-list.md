https://leetcode.com/problems/reverse-linked-list


재귀 + linkedList
``` java

/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        return recursiveCall(head, null);
    }

    public static ListNode recursiveCall(ListNode node, ListNode prev) {
        if (node == null) {
            return prev;
        }
        // null -> 1 -> 2
        // next = node.next
        // node.next = node.prev
        ListNode next = node.next;
        node.next = prev;
        // prev = node, node = next
        return recursiveCall(next, node);
    }
    
}

```
