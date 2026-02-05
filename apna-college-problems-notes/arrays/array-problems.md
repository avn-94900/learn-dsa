### max-sub array sum - kadane's algorithem

### brute force approach
```java
    public static Result bruteForce(int[] a) {
        int n = a.length;
        int maxSum = Integer.MIN_VALUE;
        int bestL = 0, bestR = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int sum = 0;
                // compute sum of a[i..j]
                for (int k = i; k <= j; k++) {
                    sum += a[k];
                }
                if (sum > maxSum) {
                    maxSum = sum;
                    bestL = i;
                    bestR = j;
                }
            }
        }
        return new Result(maxSum, bestL, bestR);
    }
```
#### optimized 

```java
public class KadaneAlgo {
    public static int maxSubArraySum(int[] nums) {
        int maxSoFar = nums[0];
        int currentMax = nums[0];

        for (int i = 1; i < nums.length; i++) {
            // extend or start new subarray
            currentMax = Math.max(nums[i], currentMax + nums[i]);
            // update best answer
            maxSoFar = Math.max(maxSoFar, currentMax);
        }
        return maxSoFar;
    }

    public static void main(String[] args) {
        int[] arr = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum Subarray Sum = " + maxSubArraySum(arr));
    }
}
```

---
