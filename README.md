# DSA TWO

## Best Time to Buy and Sell Stock

Given an array prices[] of length N, representing the prices of the stocks on different days.
The task is to find the maximum profit possible by buying and selling the stocks on different
days when at most one transaction is allowed.

Note: Stock must be bought before being sold

```text
   Input: prices[] = {7, 1, 5, 3, 6, 4}
   Output: 5
   Explanation:
   The lowest price of the stock is on the 2nd day, i.e. price = 1. Starting from the 2nd day, 
   the highest price of the stock is witnessed on the 5th day, i.e. price = 6. 
   Therefore, maximum possible profit = 6 – 1 = 5. 

   Input: prices[] = {7, 6, 4, 3, 1} 
   Output: 0
   Explanation: Since the array is in decreasing order, no possible way exists to solve the problem.
```
## Implementing solution using Greedy Approach

```txt
    To maximize profit it is important that the cost is lowered down, so minimize cost price and then maximize selling price.

    At every step, we will keep track of the minimum buying price of stock encountered so far. Then if the current price of 
    the stock is less than the previous buying price, we will update the buy price, else if the current price of stock is
    greater than the previous buying price, we can sell at this price ot get some profit.

    After iterating over the entire array, return the maximum profit.
```
### Steps to solve the problem

- Declare a buy variable to store the minimum stock price encountered so far and max_profit to store the maximum profit.
- Initialize the buy variable to the first element of the prices array.
- Iterate over the prices array and check if the current price is less than the buy price or not.
  - If the current price is smaller than buy price, then buy on this ith day.
  - If the current price is greater than buy price, then make profit from it and maximize the max_profit
- Finally, return the max_profit.

```js
    /**
     * Calculates the maximum profit that can be obtained by buying and selling stocks.
     * @param {number[]} prices - Array representing the prices of stocks on different days.
     * @returns {number} - Maximum profit achievable.
     */
    
    function maxProfit(prices) {
        if (prices.length < 2) {
            return 0; // Edge Case: Cannot make a profit with less than two prices.
        }
   
        // Initialize variables
        let buy = prices[0]; // The initial buying price
        let max_profit = 0; // The maximum profit obtained
   
        // Iterate through the prices array starting from the second element
        for (let i = 1; i < prices.length; i++) {
            // Update buying price if the current price is lower
            if (buy > prices[i]) {
                buy = prices[i];
            }
            // Update maximum profit if selling at the current price results in a higher profit
            else if (prices[i] - buy > max_profit) {
                max_profit = prices[i] - buy;
            }
        }
   
        return max_profit
    }
```

- Time Complexity: O(2^n), where n is the size of input array prices[]
- Auxiliary Space: O(N)

### Implementation using Dynamic Programming

```txt
    The recursive approach can be optimized by storing the states in a 2D dp array of size NX2.
    Here, dp[idx][0] will store the answer of maxProfit[idx, false] and dp[idx][1] will store the
    the answer of maxProfit[idx, true].
```

```js
    /**
     * Calculates the maximum profit that can be obtained by buying and selling stocks using dynamic programming.
     * @param {number[]} prices - Array representing the prices of stocks on different days.
     * @returns {number} - Maximum profit achievable.
     */

    function maxProfitDP(prices) {
        //Edge case: Cannot make a profit with less than two prices
        if (prices.length < 2) {
            return 0;
        }

        const n = prices.length;
        // 2D DP array to store max profit with 0 and 1 stocks
        const dp = new Array(n).fill(null).map(() => [0, 0]);

        // Initialize variables
        let buy = -prices[0];
        let sell = 0;

        // Loop through prices to calculate max profit at each day
        for (let i = 1; i < n; i++) {
            // Update but to be the maximum between the previous buy and the profit from buying at prices[i]
            buy = Math.max(buy, -prices[i]);
            
            // Update sell to be the maximum between the previous sell and the profit form selling at prices[i]
            sell = Math.max(sell, buy + prices[i]);
        }

        // Return the maximum profit calculated from the last day
        return Math.max(buy, sell);
    }

    // Given Prices
    const prices = [7, 1, 5, 3, 6, 4];
    
    // Function Call
    const ans = max.ProfitDP(prices);

    // Print answer
    console.log(ans);
```

- Time Complexity: O(N), where N is the length of the given array.
- Auxiliary Space: O(N)

