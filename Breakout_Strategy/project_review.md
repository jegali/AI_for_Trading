# Breakout Strategy

This is the project review I got for the project "Breakout Strategy" in the "AI for trading" nanodegree


## Meets Specifications

You have demonstrated a very good understanding of the breakout strategy.

Tips:

You can also read more about processing large dataset with pandas at:  [https://pandas.pydata.org/pandas-docs/stable/user_guide/scale.html](https://pandas.pydata.org/pandas-docs/stable/user_guide/scale.html)

To learn more about the breakout strategy you can read this article  [breakout strategy](https://tradingstrategyguides.com/best-breakout-trading-strategy/)

This article is also great to understand ways to implement the breakout strategy.  [3 ways to implement breakout strategy](https://www.thebalance.com/three-better-ways-to-day-trade-breakouts-1030880)

Great job! and good luck in your future projects.

## Generate Signal

- [x] The function  `get_high_lows_lookback`  computes the maximum and minimum of the closing prices over a window of days.

	Great job!  ![:100:](https://review.udacity.com/assets/images/emojis/100.png ":100:")

- [x] The function  `get_long_short`  computes long and short signals using a breakout strategy.

- [x] The function  `filter_signals`  filters out repeated long or short signals.

	You have filtered the correct signals.  	![:thumbsup:](https://review.udacity.com/assets/images/emojis/thumbsup.png ":thumbsup:")

	To help increase performance, as you work with larger datasets, you can use the apply() method provided by pandas. The apply method allows you to use a function on each row/column in a dataframe. You can read more about this with some examples at  [https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.apply.html)

	```
	long = long.apply(lambda signals: clear_signals(signals, lookahead_days))
	short = short.apply(lambda signals: clear_signals(signals, lookahead_days))
	```

	This would reduce the amount of memory you need, and will process the data a lot faster.

- [x] The function  `get_lookahead_prices`  gets the close price days ahead in time.

	well done!

- [x] The function  `get_return_lookahead`  generates the log price return between the closing  - [x] price and the lookahead price.

- [x] The function  `get_signal_return`  generates the signal returns.

	Fantastic!

## Evaluate Signal

- [x] Correctly answers the question “What do the histograms tell you about the signal returns?"

	You have correctly identify the distributions are not normal due to outliers.

## Outliers

- [x] The function  `calculate_kstest`  calculates the ks and p values.

- [x] The function  `find_outliers`  returns the list of outlying symbols.

	Correct calculation of the ks and p values.  ![:thumbsup:](https://review.udacity.com/assets/images/emojis/thumbsup.png ":thumbsup:")
