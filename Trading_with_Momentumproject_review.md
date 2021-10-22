# Trading with Momentum

This is the project review I got for the project "Trading with Momentum" in the "AI for trading" nanodegree


## Meets Specifications

*I also am a fan of just returning values in the return statement. So I did a calculation before and assigned it a variable, to return the variable(s) then._*

That's a good practise for debugging in a small codebase. I'd suggest using debuggers in pycharm or any other IDE to get to see the values of the variables.

*I tried to give the variables meaningful names. In most of the cases they are more or less equal to the function names._*

That really helps to read your code

Congratulations in meeting the specifications of the project! I hope you have enjoyed this project. Next, you will learn about another trading strategy which is called breakout strategy and also learn about time-series analysis. I hope that you're enjoying this nanodegree and excited to move ahead! Check out the below review and Good luck!

## Market Data

 - [x] The function  `resample_prices`  computes the monthly prices.

	![:thumbsup:](https://review.udacity.com/assets/images/emojis/thumbsup.png ":thumbsup:")

- [x] The function  `compute_log_returns`  computes the log returns from the prices.

	Raw return is defined as  `R = (p(t) - p(t-1)) / p(t-1)`, we can change to log return as follows;

	```
	R = p(t) / p(t-1) - p(t-1) / p(t-1) 
	R = p(t) / p(t-1) - 1
	```

	Taking logs on both sides;

	```
	lnR = ln(p(t) / p(t-1)) - ln(1) lnR = ln(p(t) / p(t-1)) where ln(1) = 0 
	lnR = ln(p(t)) - ln(p(t-1)) #using logarithmic rule
	```

- [x] The function  `shift_returns`  computes the shifted returns.

	With  `+ shift_n`  values, you can calculate past returns and with  `- shift_n`  values, you can calculate the look-ahead returns.


## Portfolio

- [x] The function  `get_top_n`  selects the  `top_n`  number of the top performing stocks.

- [x] The function  `portfolio_returns`  calculates the projected returns.

	The portfolio returns calculates the projected returns by following the trading strategy which forms a hypothesis for testing statistically if it holds true or not;

	Trading Strategy : For each month-end observation period, rank the stocks by previous returns, from the highest to the lowest. Select the top performing stocks for the long portfolio, and the bottom performing stocks for the short portfolio.

	This trading strategy is a momentum based trading strategy.

## Statistical Tests

- [x] The function  `analyze_alpha`  calculates the t-value and p-value.

	Here, alpha refers to the significance level of a hypothesis test.

- [x] The student correctly identifies the p-value they got. The student indicates what the p-value indicates about their signal.

	That's correct! The conclusion of the hypothesis testing is that the signal is not reliable enough to generate positive returns and may need to come up better trading strategy. In this case, we fail to reject the null hypothesis and conclude that the expected mean return from the signal might be zero, and that any positive mean observed here might be a matter of chance (within certain expected bounds of deviation).
