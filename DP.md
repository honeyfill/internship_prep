+ [Climbing Stairs](#climbing-stairs)
+ [Coin Change](#coin-change)
+ [Longest Increasing Subsequence](#longest-increasing-subsequence)
+ [Longest Common Subsequence](#longest-common-subsequence)
+ [Word Break](#word-break)
+ [Combination Sum IV](#combination-sum-iv)
+ [House Robber](#house-robber)
+ [House Robber II](#house-robber-ii)
+ [Unique Paths](#unique-paths)
+ [Jump Game](#jump-game)
<!---->
## Climbing Stairs
https://leetcode.com/problems/climbing-stairs/
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        stairs = [0]*n
        stairs[0], stairs[1] = 1, 2
        for i in range(2, n):
            stairs[i] = stairs[i-1] + stairs[i-2]
        return stairs[n-1]
```
## Coin Change
https://leetcode.com/problems/coin-change/
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        comb = [2**31]*(amount+1)
        comb[0] = 0
        for i in range(1, amount+1):
            for coin in coins:
                if i < coin:
                    continue
                comb[i] = min(comb[i], 1 + comb[i - coin])
        return comb[amount] if comb[amount] != 2**31 else -1
```
## Longest Increasing Subsequence
https://leetcode.com/problems/longest-increasing-subsequence/
```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        size = len(nums)
        lenght = 0
        dp = [10**4 + 1]*(size+1)
        dp[0] = -10**4 - 1
        for num in nums:
            left = -1
            right = size
            while left < right - 1:
                mid = (left + right)//2
                if num > dp[mid]:
                    left = mid
                else:
                    right = mid
            dp[right] = num
            lenght = max(lenght, right)
        return lenght```
## Longest Common Subsequence
https://leetcode.com/problems/longest-common-subsequence/
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0]*(len(text2)+1) for _ in range(len(text1)+1)]
        for i, sym1 in enumerate(text1):
            for j, sym2 in enumerate(text2):
                dp[i+1][j+1] = dp[i][j] + 1 if sym1 == sym2 else max(dp[i][j+1], dp[i+1][j])
        return dp[-1][-1]
```
## Word Break
https://leetcode.com/problems/word-break/
```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False]*(len(s)+1)
        dp[0] = True
        for i in range(len(s)):
            if dp[i]:
                for j in range(i, len(s)):
                    if s[i:j+1] in wordDict:
                        dp[j+1] = True
        return dp[-1]
```
## Combination Sum IV
https://leetcode.com/problems/combination-sum-iv/
```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        comb = [0]*(target + 1)
        comb[0] = 1
        for i in range(1, len(comb)):
            for j in range(len(nums)):
                if i - nums[j] >= 0:
                    comb[i] += comb[i - nums[j]]
        return comb[target]
```
## House Robber
https://leetcode.com/problems/house-robber/
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        max_prev = max_last = 0
        for num in nums:
            max_prev, max_last = max_last, max(max_prev + num, max_last)
        return max_last
```
## House Robber II
https://leetcode.com/problems/house-robber-ii/
```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        rob_prev = rob_cur = ans = 0
        if len(nums) == 1:
            return nums[0]
        for i in range(len(nums)-1):
            rob_prev, rob_cur = rob_cur, max(rob_prev + nums[i], rob_cur)
            ans = max(ans, rob_cur)
        rob_prev = rob_cur = 0
        for i in range(1, len(nums)):
            rob_prev, rob_cur = rob_cur, max(rob_prev + nums[i], rob_cur)
            ans = max(ans, rob_cur)
        return ans
```
## Unique Paths
https://leetcode.com/problems/unique-paths/
```python
import math
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        return math.comb(m + n - 2, m - 1)
```
## Jump Game
https://leetcode.com/problems/jump-game/
```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        can_reach = 0
        for i, num in enumerate(nums):
            if i > can_reach:
                return False
            can_reach = max(can_reach, i + num)
        return True
```
