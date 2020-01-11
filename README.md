# Three Sum
## https://leetcode.com/problems/3sum

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

**Note: The solution set must not contain duplicate triplets.**

```
Example:

Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Implementation 1 : O(n^3) Time Limit Exceeded 😰

```java
public static List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
    	if(nums == null || nums.length < 3)
        	return result;
    	
    	int n = nums.length; 
    	for(int i = 0; i < n - 2; i++) {
    	    for(int j = i + 1; j < n - 1; j++) {
    		for(int k = j + 1; k < n; k++) {
    		     if((nums[i] + nums[j] + nums[k]) == 0 ) {
    			  addResult(result, new Integer[] {nums[i], nums[j], nums[k]});
    			  break;
    		      }
    		}
    	    }
    	}
    	
    	return result;
}

private static void addResult(List<List<Integer>> result, Integer[] triplet) {
	Set<Integer> threeSum = new HashSet<Integer>(Arrays.asList(triplet));
	boolean alredayExists = false;
	for(List<Integer> list: result) {
	     Set<Integer> res = new HashSet<Integer>(list);
	     if(res.equals(threeSum)) {
		 alredayExists = true;
		 break;
	     }
	}
	
	if(!alredayExists) {
	   result.add(Arrays.asList(triplet));
	}	
}
```

Above implementation have Runtime complexity of O(n^3) and space complexity of O(1)
```
Runtime Complexity = O(n^3)
Space Complexity   = O(1)
```

## Implementation 2 : O(n^2) Time Limit Exceeded 😰

```java
public static List<Integer[]> threeSum(int[] nums) {
        List<Integer[]> result = new ArrayList<Integer[]>();
    	if(nums == null || nums.length < 3)
        	return result;
    	
    	int n = nums.length; 
    	Arrays.sort(nums);
    	for(int i = 0; i < n - 2; i++) {
    		int left = i + 1;
    		int right = n - 1;
    		while(left < right) {
    			if( (nums[i] + nums[left] + nums[right]) > 0) {
    				right --;
    			} else if( (nums[i] + nums[left] + nums[right]) < 0) {
    				left++;
    			} else {
    				addResult(result, new Integer[] {nums[i], nums[left], nums[right]});
    				left++;
    				right--;
    			}
    		}
    	}
    	
    	return result;
    }

	private static void addResult(List<Integer[]> result, Integer[] triplet) {
		Set<Integer> threeSum = new HashSet<Integer>(Arrays.asList(triplet));
		boolean alredayExists = false;
		for(Integer[] list: result) {
			Set<Integer> res = new HashSet<Integer>(Arrays.asList(list));
			if(res.equals(threeSum)) {
				alredayExists = true;
				break;
			}
		}
		if(!alredayExists) {
			result.add(triplet);
		}
		
	}
```
Above implementation have Runtime complexity of O(n^2) and space complexity of O(1)
```
Runtime Complexity = O(n^2)
Space Complexity   = O(1)
```

## Implementation 3 : O(n^2) Optimization - Making LeetCode Happy 😊

```java
public static List<List<Integer>> threeSum(int[] nums) {
       List<List<Integer>> result = new ArrayList<List<Integer>>();
    	if(nums == null || nums.length < 3)
        	return result;
    	
    	Arrays.sort(nums);
    	for (int i = 0; i < nums.length - 2; i++) {
    	    if (i == 0 || (i > 0 && nums[i] != nums[i-1])) {
    	        int low = i+1, high = nums.length - 1;
    	        int sum = 0 - nums[i];
    	        while (low < high) {
    	           if (nums[low] + nums[high] == sum) {
    	              result.add(Arrays.asList(nums[i], nums[low], nums[high]));
    	              while (low < high && nums[low] == nums[low+1]) low++;
    	              while (low < high && nums[high] == nums[high-1]) high--;
    	              low++; 
		      high--;
    	           } else if (nums[low] + nums[high] < sum) {
    	              low++;
    	           } else {
    	              high--;
    	           }
    	        }
    	    }
    	}
    	
       return result;
}
```
Above implementation have Runtime complexity of O(n^2) and space complexity of O(1)
```
Runtime Complexity = O(n^2)
Space Complexity   = O(1)
```
**Note that in above implementation, we are not using `addResult()` method to handle duplicate triplets, rather we are handling duplicate scenarios, when we are adding a triplet to the final result. This optimizes the runtime of the algorithms and makes it fast.

## References :
1. https://massivealgorithms.blogspot.com/2014/06/leetcode-3sum.html
2. https://www.youtube.com/watch?v=qJSPYnS35SE
