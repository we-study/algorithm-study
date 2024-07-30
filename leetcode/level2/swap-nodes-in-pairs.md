https://leetcode.com/problems/swap-nodes-in-pairs


``` java
// ex) 1 -> 2 -> 3 -> 4
public static ListNode swapPairsWithRecursion(ListNode head) {
        if (head != null && head.next != null) {
            ListNode next = head.next; // 2
            head.next = swapPairsWithRecursion(head.next.next); // 4 -> 3을 반환 => 1 -> 4 -> 3
            next.next = head; 2 -> 1 -> 4 -> 3
            return next; // swap 했으니 next를 리턴
        }
        return head; 
    }
```
ex) 1 -> 2 -> null

0. 2 tmp에 저장
1. 1의 next로 null 연결 (하기전 2 주소 저장)
2. 2의 next로 1 연결

=> 코드로 옮기면

ListNode tmp = head.next
head.next = tmp.next // head.next.next
tmp.next = head






