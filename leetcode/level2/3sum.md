https://leetcode.com/problems/3sum/


1. 투포인터로 시도 -> 정확성 실패
``` java

class Solution {
    public static List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        int left = 0;
        int right = nums.length - 1;
        Set<List<Integer>> listSet = new HashSet<>();
        while (left < right && right - left + 1 > 2) {
            int sum = nums[left] + nums[right];
            if (sum < 0) {
                if (sum + nums[right-1] == 0) {
                    listSet.add(List.of(nums[left], nums[right-1], nums[right]));
                    left++;
                    right--;
                } else {
                    left++;
                }
            } else if (sum > 0) {
                if (sum + nums[left+1] == 0) {
                    listSet.add(List.of(nums[left], nums[left+1], nums[right]));
                    left++;
                    right--;
                } else {
                    right--;
                }
            } else {
                if (sum + nums[left + 1] == 0) {
                    listSet.add(List.of(nums[left], nums[left+1], nums[right]));
                } else if (sum + nums[right-1] == 0) {
                    listSet.add(List.of(nums[left], nums[right-1], nums[right]));
                }
                left++;
                right--;
            }

        }
        return new ArrayList<>(listSet);
    }
}

```

2. n + 투포인터 -> O(n^2)
``` java

    public static List<List<Integer>> threeSumAnswer(int[] nums) {
        Arrays.sort(nums);
        int left, right, sum = 0;
        List<List<Integer>> answer = new ArrayList<>();
        // i : 0 -> n-2 으로 이동
        for (int i = 0; i < nums.length - 2; i++) {
            // 중복 Pass
            if (i > 0 && nums[i] == nums[i-1]) {
                continue;
            }

            // 투포인터로 간격 좁히면서 합계산
            left = i+1;
            right = nums.length - 1;
            while(left < right) {
                sum = nums[i] + nums[left] + nums[right];
                if (sum < 0) {
                    left++;
                } else if (sum > 0) {
                    right--;
                } else {
                    answer.add(List.of(nums[i], nums[left], nums[right]));
                    // 중복 제거
                    while (left < right && nums[left] == nums[left+1]) {
                        left++;
                    }
                    while(left < right && nums[right] == nums[right-1]) {
                        right--;
                    }
                    left++;
                    right--;
                }
            }
        }
        return answer;
    }
```

3. Set으로 중복 제거
``` java
    public static List<List<Integer>> threeSumWithSet(int[] nums) {
            Arrays.sort(nums);
            int left, right, sum = 0;
            Set<List<Integer>> answer = new HashSet<>();
            // i : 0 -> n-2 으로 이동
            for (int i = 0; i < nums.length - 2; i++) {
                // 투포인터로 간격 좁히면서 합계산
                left = i+1;
                right = nums.length - 1;
                while(left < right) {
                    sum = nums[i] + nums[left] + nums[right];
                    if (sum < 0) {
                        left++;
                    } else if (sum > 0) {
                        right--;
                    } else {
                        answer.add(List.of(nums[i], nums[left], nums[right]));
                        // 중복 제거
                        left++;
                        right--;
                    }
                }
            }
            return new ArrayList<>(answer);
        }
```
