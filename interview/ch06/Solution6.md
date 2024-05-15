https://leetcode.com/problems/longest-palindromic-substring

- 투포인터 + 슬라이딩 윈도우

- 짝수(2칸), 홀수(3칸)으로 이루어진 포인터가 슬라이딩 윈도우처럼 우측으로 이동 -> 윈도우에 들어온 문자열이 팰린드롬인 경우 양측으로 확장하면서 가장 긴 값을 찾는다

```java
class Solution {
    int start = 0;
    int max = 0;

    public String longestPalindrome(String s) {
        if (s.length() < 2) {
            return s;
        }
        
        for (int i = 0; i < s.length() - 1; i++) {
            extendPalindrome(s, i, i + 1); // 짝수 윈도우
            extendPalindrome(s, i, i + 2); // 홀수 윈도우
        }
        return s.substring(start, start + max);
    }

    private void extendPalindrome(String str, int left, int right) {
        // 범위 내에 있고, 양끝 문자가 같으면 확장
        while (left >=0 && right < str.length() && str.charAt(left) == str.charAt(right)) {
            left--;
            right++;
        }
        // 최대 길이보다 긴 경우
        if (max < right - left - 1) {
            max = right - left - 1;
            start = left + 1;
        }
    }
}
```
