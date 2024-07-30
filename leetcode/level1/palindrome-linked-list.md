

https://leetcode.com/problems/palindrome-linked-list

1. list 사용
``` java
/**
     * Definition for singly-linked list.
     * public class ListNode {
     * int val;
     * ListNode next;
     * ListNode() {}
     * ListNode(int val) { this.val = val; }
     * ListNode(int val, ListNode next) { this.val = val; this.next = next; }
     * }
     */
    public boolean isPalindromeWithList(ListNode head) {
        List<Integer> list = new ArrayList<>();
        ListNode node = head;
        while (node != null) {
            list.add(node.val);
            node = node.next;
        }

        int right = list.size() - 1;
        for (int left = 0; left < list.size() / 2; left++) {
            if (list.get(left) != list.get(right-left)) {
                return false;
            }
        }
        return true;
    }
```

2. stack 사용
``` java
public boolean isPalindromeWithStack(ListNode head) {
        Stack<Integer> stack = new Stack<>();
        ListNode node = head;
        while (node != null) {
            stack.add(node.val);
            node = node.next;
        }

        while (head != null) {
            if (head.val != stack.pop()) {
                return false;
            }
            head = head.next;
        }

        return true;
    }


```


3. deque사용

``` java
    Deque<Integer> deque = new LinkedList<>();
        ListNode node = head;
        while (node != null) {
            deque.push(node.val);
            node = node.next;
        }

        while (!deque.isEmpty() && deque.size() > 1) {
            if (deque.pollFirst() != deque.pollLast()) {
                return false;
            }
        }
        return true;

```
