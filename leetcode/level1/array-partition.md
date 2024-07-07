https://leetcode.com/problems/array-partition/

1. [n, n+i, (n+i)+j, (n+i+j)+k] 라고 하면 -> n+(n+i+j) 이 항상 가장 큼 

``` java
class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int result = 0;
        for (int i=0; i<nums.length; i+=2) {
            result += nums[i]; // 0~nums.length까지 순차적으로 돌고 if(i%2==0) 짝수번 인덱스일 때만 더하게 할 수 도 있다.
        }
        return result;
    }
}
```

2. Collections.min(list); 함수 사용하기
``` java

int sum = 0;
        List<Integer> pair = new ArrayList<>();
        Arrays.sort(nums);
        for (int n : nums) {
            pair.add(n);
            if (pair.size()==2) {
                sum += Collections.min(pair);
                pair.clear();
            }
        }
        return sum;
```

