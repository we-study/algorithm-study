https://leetcode.com/problems/odd-even-linked-list

``` java

    public static ListNode oddEvenList(ListNode head) {
        ListNode odd = new ListNode(0);
        ListNode even = new ListNode(0);
        ListNode oddRoot = odd;
        ListNode evenRoot = even;
        int idx = 1;
        while (head != null) {
            ListNode next = head.next;
            if (idx % 2 == 0) {
                even.next = head;
                even.next.next = null;
                even = even.next;
            } else {
                odd.next = head;
                odd.next.next = null; // 루프가 생겨서 끊어 줘야 함
                odd = odd.next;
            }
            idx++;
            head = next;
        }

        // 홀수의 마지막 노드의 next에 짝수의 첫번째 노드 연결
        odd.next = evenRoot.next;

        return oddRoot.next;
    }

    public ListNode oddEvenList2(ListNode head) {
        // 방어코드
        if (head == null) {
            return head;
        }
        // 홀수
        ListNode odd = head;
        // 짝수
        ListNode even = head.next;
        ListNode evenHead = even; // 짝수노드 첫번째 (홀수노드의 가장 마지막 노드와 연결해야하므로)
        while (even != null && even.next != null) {
            // 두칸씩 이동
            odd.next = odd.next.next;
            even.next = even.next.next;

            odd = odd.next;
            even = even.next;
        }
        // 홀수노드의 마지막 노드를 짝수노드의 첫번째와 연결
        odd.next = evenHead;
        // 첫번째 노드
        return head;
    }

```
