# Three Sum
## https://leetcode.com/problems/3sum

## Implementation :

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

