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
   The lowest price of the stock is on the 2nd day, i.e. price = 1. Starting from the 2nd day, the highest price of the stock is witnessed on the 5th day, i.e. price = 6. 
   Therefore, maximum possible profit = 6 – 1 = 5. 

   Input: prices[] = {7, 6, 4, 3, 1} 
   Output: 0
   Explanation: Since the array is in decreasing order, no possible way exists to solve the problem.
```
## Implementing solution using Greedy Approach

```txt
    To maximize profit it is important that the cost is lowered down, so minimize cost price and then maximize selling price.
    At every step, we will keep track of the minimum buying price of stock encountered so far. Then if the current price of 
    the stock is less than the previous buying price, we will update the buy price, else if the current price of stock is greater
    than the previous buying price, we can sell at this price ot get some profit.
    After iterating over the entire array, return the maximum profit.
```
### Steps to solve the problem

- Declare a buy variable to store the minimum stock price encountered so far and max_profit to store the maximum profit.
- Initialize the buy variable to the first element of the prices array.
- Iterate over the prices array and check if the current price is less than the buy price or not.
  - If the current price is smaller than buy price, then buy on this ith day.
  - If the current price is greater than buy price, then make profit from it and maximize the max_profit
- Finally, return the max_profit.
