# Array Tasks
+ [Two Sum](#two-sum)
+ [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)
+ [Contains Duplicate](#contains-duplicate)
+ [Product of Array Except Self](#product-of-array-except-self)
+ [Maximum Subarray](#maximum-subarray)
+ [Maximum Product Subarray](#maximum-product-subarray)
+ [Find Minimum in Rotated Sorted Array](#find-minimum-in-rotated-sorted-array)
+ [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)
+ [Container With Most Water](#container-with-most-water)
<!---->
## Two Sum
https://leetcode.com/problems/two-sum/
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        candidates = {}
        for i, num in enumerate(nums):
            if num in candidates:
                return [i, candidates[num]]
            candidates[target - num] = i
```
## Best Time to Buy and Sell Stock
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        minprof = 10**5
        maxprof = 0
        for price in prices:
            if price < minprof:
                minprof = price
            else:
                maxprof = max(maxprof, price - minprof)
        return maxprof
```
## Contains Duplicate
https://leetcode.com/problems/contains-duplicate/
```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        return False if len(set(nums)) == len(nums) else True
```
## Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self/
```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        left = right = 1
        answer = [1 for _ in range(len(nums))]
        for i in range(len(nums)):
            answer[i] *= left
            left *= nums[i]
            answer[len(nums) - 1 - i] *= right
            right *= nums[len(nums) - 1 - i]
        return answer
```
## Maximum Subarray
https://leetcode.com/problems/maximum-subarray/
```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        ans = -10**5
        cur = 0
        for num in nums:
            cur += num
            ans, cur = max(cur, ans), max(cur, 0)
        return ans
```
## Maximum Product Subarray
https://leetcode.com/problems/maximum-product-subarray/submissions/
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        prev_max = nums[0]
        prev_min = nums[0]
        ans = nums[0]
        for i, num in enumerate(nums):
            if i == 0:
                continue
            prev_max, prev_min = max(num, max(prev_max*num, prev_min*num)), min(num, min(prev_max*num, prev_min*num))
            ans = max(ans, prev_max)
        return ans
```
## Find Minimum in Rotated Sorted Array
https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        if nums[0] < nums[-1]:
            return nums[0]
        left = -1
        right = len(nums)-1
        while right - 1 > left:
            mid = (right + left)//2
            if nums[left] > nums[mid]:
                right = mid
            else:
                left = mid
        return nums[right]
```
## Search in Rotated Sorted Array
https://leetcode.com/problems/search-in-rotated-sorted-array/
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1

        while left < right:
            mid = (left + right) // 2
            if (nums[0] > target) ^ (nums[0] > nums[mid]) ^ (target > nums[mid]):
                left = mid + 1
            else:
                right = mid
        return left if nums[left] == target else -1
```
## Container With Most Water
https://leetcode.com/problems/container-with-most-water/
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1

        water = 0

        while left < right:
            water = max(water, (right-left)*min(height[left], height[right]))
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1

        return water
```
