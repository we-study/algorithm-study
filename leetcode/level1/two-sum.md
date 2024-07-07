https://leetcode.com/problems/two-sum

1. brute-force -> O(n^2)
``` java
public int[] twoSum(int[] nums, int target) {
        int [] result = new int[2];
        for (int i = 0; i < nums.length; i++) {
            for (int j=i+1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    result[0] = i;
                    result[1] = j;
                    break;
                }
            }
        }
        return result;
    }
```

1. x + y = target -> y = target - x -> O(n)
2. HashMap 조회 -> O(1)
``` java
    public int[] twoSumByMap(int[] nums, int target) {
        Map<Integer, Integer> numbersMap = new HashMap<>();
        for (int i=0; i<nums.length; i++) {
            numbersMap.put(nums[i], i);
        }

        for (int i=0; i<nums.length; i++) {
            int y = target - nums[i];
            if (numbersMap.containsKey(y) && numbersMap.get(y) != i) {
                return new int[]{i, numbersMap.get(y)};
            }
        }

        // for 문 하나로 합치기
        Map<Integer, Integer> anotherMap = new HashMap<>();
        for (int i=0; i<nums.length; i++) {
            int y = target - nums[i];
            if (anotherMap.containsKey(y) && anotherMap.get(y) != i) {
                return new int[] {y, i};
            }
            anotherMap.put(nums[i], i);
        }

        return null;
    }
```
