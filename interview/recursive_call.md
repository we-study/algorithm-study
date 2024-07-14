## 재귀함수 작성하기

예시

https://leetcode.com/problems/swap-nodes-in-pairs

``` java
public static ListNode swapPairsWithRecursion(ListNode head) {
    if (head != null && head.next != null) {
        ListNode next = head.next; // 2번 노드
        head.next = swapPairsWithRecursion(head.next.next); // 1번 노드의 next를 재귀 호출 결과로 설정
        next.next = head; // 2번 노드의 next를 1번 노드로 설정
        return next; // 2번 노드를 반환
    }
    return head;
}
```

### 1. Base Case(기본 조건 설정)
- 종료 조건 설정하기
-> head == null or head.next == null 일때 재귀가 종료된다 

### 2. Divide the Problem
- 문제를 더 작은 문제로 분할해야한다
-> 두 노드를 스왑하는 작업을 더 작은 문제로 나눔

### 3. Recursive call
- 문제를 분할 하고, 재귀호출을 사용해서 작은 문제를 해결
-> swapPairsWithRecursion(head.next.next)를 호출하여 나머지 리스트를 처리 

### 4. Combine the results(결과 결합)
- 재귀호출이 반환한 결과를 사용해서 전체 문제의 해결책을 결합
-> 스왑된 나머지 리스트를 현재노드와 결합 

### 5. Return the Result
- 스왑된 페어의 첫 번째 노드 반환

