# Problem Solved: Uncover the Most Efficient Java Algorithm!

# Problem

[Problem_Link](https://practice.geeksforgeeks.org/problems/d894706c496da5c5a4f45b0360c7f4164c516f83/1)

## **Problem Solving Approach**

1. Traverse through all the numbers in the intervals and store their frequencies in a HashMap.
2. Sort the hashmap based on the keys.→in worst case, O(n log n)
3. Find the maximum powerful integer by iterating through the sorted hashmap, which occurs at least k times.

## **Time Complexity: O(n log n), Space Complexity: O(n)**

```java
import java.util.*;
class Solution {

    /**
     * This method takes in the number of intervals n, the 2D integer array of intervals interval, 
     * and the minimum number of occurrences k for a number to be considered powerful.
     * It returns the powerful integer which occurs at least k times. If multiple integers have 
     * at least k occurrences, the maximum integer out of all those elements is returned.
     * If no integer occurs at least k times, -1 is returned.
     *
     * @param n         the number of intervals
     * @param interval  the 2D integer array of intervals where interval[i] = [start, end]
     * @param k         the minimum number of occurrences for a number to be considered powerful
     * @return the powerful integer which occurs at least k times, or -1 if no integer occurs at least k times
     */
    public static int powerfullInteger(int n, int[][] interval, int k) {
        // A hashmap to store the frequency of each number
        Map<Integer, Integer> map = new HashMap<>();
        // The maximum powerful integer that occurs at least k times, if there is no, return -1
        int maxPowerful = -1;

        // Loop through each interval and update the frequency of each number in the hashmap
        for (int i = 0; i < n; i++) {
            for (int j = interval[i][0]; j <= interval[i][1]; j++) {
                map.put(j, map.getOrDefault(j, 0) + 1);
            }
        }

        // Sort the hashmap by key
        List<Map.Entry<Integer, Integer>> list = new ArrayList<>(map.entrySet());
        list.sort(Map.Entry.comparingByKey());

        // find the maximum powerful integer
        for (Map.Entry<Integer, Integer> val : list) {
            if (val.getValue() >= k) {
                maxPowerful = val.getKey();
            }
        }

        return maxPowerful;
    }
}
```