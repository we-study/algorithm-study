https://leetcode.com/problems/product-of-array-except-self

``` java

public class Solution11 {

    public static void main(String[] args) {
        productExceptSelf(new int [] {1,2,3,4});
    }

    /**
     * a    b   c   d
     * -> nums[i]의 left 값들의 곱
     * 1    a   ab  abc
     *              <- nums[i]의 right 값들의 곱
     * bcd  cd   d   1
     *
     * bcd  acd  abc abc
     */
    public static int[] productExceptSelf(int[] nums) {
        int p = 1;
        int [] result = new int [nums.length];
        for (int i=0; i<nums.length; i++) {
            result[i] = p;
            p *= nums[i];
        }
        p = 1;
        for (int i=nums.length-1; i >=0; i--) {
            result[i] *= p;
            p *= nums[i];
        }
        return result;
    }
}


```
