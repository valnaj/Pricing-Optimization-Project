# Pricing Optimization Project

This repository contains the implementation of a pricing optimization strategy for a retailer game, aiming to maximize revenue over a 15-week sales period.

## Game Context

In the Retailer Game, you are in charge of selling 2,000 items of brand new fashion apparel. Your goal is to select the optimal pricing strategy to maximize revenues. The list price of the item is $60, and it must be sold at the list price for at least one week. After this, the item may be discounted to $54 (a 10% discount), to $48 (a 20% discount), or to $36 (a 40% discount). Once lowered, the price may not be increased. The sales season is 15 weeks long. Production lead times are long enough that additional items cannot be procured during the sales season. All items remaining at the end of the sales horizon will be discarded at $0 value. Historical demand data can be considered to make pricing decisions.

## Objectives

The primary objective of this project was to develop a markdown pricing strategy for a retailer to maximize the total revenue from selling inventory over a 15-week period. Historical sales data and statistical analyses were used to inform the strategy.

## Methodology

### Data Collection

To gather enough samples to accurately estimate how price changes from markdowns affect demand, a scraper using Selenium WebDriver was employed to play the game 2,500 times, randomly choosing between maintaining the price, applying a 20% markdown, and applying a 40% markdown. Instances with zero inventory before the 15th week were excluded, as they do not contribute to the analysis and effectively end the game with no items left to sell.

### Data Analysis

- **Average Weekly Sales:** Calculated for each price point ($60, $54, $48, $36).
- **Demand Jumps:** Computed the percentage change in average weekly sales from the baseline price of $60 to the discounted prices.
  - At $54 (10% discount): 27.63% increase
  - At $48 (20% discount): 74.36% increase
  - At $36 (40% discount): 148.16% increase

### Optimization Strategy

A dynamic linear programming (LP) method was used to determine the optimal markdown strategy. The LP model aimed to maximize total revenue by selecting the best weeks to apply markdowns, considering constraints such as the total weeks available and inventory limits. Decision variables included the number of weeks to sell at each price point.

#### Linear Programming (LP) Method

The LP model considered the following key aspects:
- **Demand Calculation:** Estimated demand at each price point based on historical data.
- **Units Available:** Calculated the remaining units available for sale each week.
- **Decision Variables:** Determined the number of weeks to sell at each price point ($60, $54, $48, $36).
- **Constraints:**
  - **Total Weeks Constraint:** The sum of weeks selling at each price point must equal the total weeks remaining.
  - **Inventory Constraint:** The total units sold across all price points must not exceed the available inventory.
- **Objective Function:** Maximized the total revenue by optimizing the allocation of weeks to each price point.

### Implementation

The implementation and simulation were carried out using a combination of Python and Selenium to automate the retailer game. Each week, the LP strategy guided whether to maintain the current price or apply a markdown. Sales data was continuously collected after each action to inform subsequent decisions.

## Results

The results of running 500 simulations with the LP strategy demonstrated significant improvements in revenue optimization. The analysis of the revenue differences between achieved and perfect revenue yielded the following statistics:
- Mean difference: 2.36%
- Minimum difference: 0%
- Maximum difference: 15.76%
- Standard deviation: 2.38%
- Mean confidence interval: (2.15%, 2.57%)
