
# Backtesting

This is the project review I got for the project "Backtesting" in the "AI for trading" nanodegree




## Meets Specifications

Great job, you are ready to go! 💯Clearly, you have acquired all the important concepts from this project. Congrats on completing this course! Hope you find all the previous sharing resources helpful.

Tip: If you are interested in knowing more about backtesting, I would suggest that you could read  [this great article](https://www.quantstart.com/articles/Successful-Backtesting-of-Algorithmic-Trading-Strategies-Part-I)  and take a look  [this python package](https://kernc.github.io/backtesting.py/).

## Shift Daily Returns Data

- [x] The variable  `frames`  contains the data from  `daily_return`  and  `data`  correctly shifted.

	Well done! You correctly prepare the required data  `frames`  with  `merge`  function💯

	```
	date_shifts = zip(
	        sorted(data.keys()),
	        sorted(daily_return.keys())[dlyreturn_n_days_delay:len(data) + dlyreturn_n_days_delay])
	```

## Build Universe Based on Filters

- [x] The function  `get_universe`  correctly creates a stock universe by selecting only those companies that have a market capitalization of at least 1 billion dollars (1e9) OR that are in the previous day's holdings, even if on the current day, the company no longer meets the 1 billion dollar criteria.

	They should use the  `.copy()`  attribute to create a copy of the data and they should drop the column containing the daily return from the universe dataframe.

	The returned  `universe`  dataframe should have a shape of (2265, 93)

	Good job! You successfully get the right universe.👍

	-   `df['IssuerMarketCap'] >= 1e9`  => market capitalization of at least 1 billion dollars
	-   `abs(df['h.opt.previous']) > 0`  => that are in the previous day's holdings

## Factor covariance matrix

- [x] The function  `diagonal_factor_cov`  correctly creates the factor covariance matrix. The factor matrix must be scaled by (0.01**2). They must use the given  `colnames`  function to get the column names from  `X`  and use the statement 'covariance[date]' to get the covariances for the given  `date`.

	The returned factor covariance matrix should have shape (77, 77)

	Perfect! You correctly create the factor covariance matrix and scale it with a correct weight  `0.01**2`🎉

	```
	Fm[i,i] = (0.01 ** 2) * get_pairwise_cov(cov, fac, fac)
	```

## Alpha Combination

- [x] The function  `get_B_alpha`  correctly creates a matrix of alpha factors. They must use the given  `get_formula`  and  `model_matrix`  functions.

	The returned  `B_alpha`  should be of type patsy.design_info.DesignMatrix and it should have shape (2265, 4). The 4 columns of this matrix should correspond to the 4 alpha factors chosen at the beginning, namely:

	"USFASTD_1DREVRSL"  
"USFASTD_EARNYILD"  
"USFASTD_VALUE"  
"USFASTD_SENTMT"

	Fantastic! You correctly create a matrix of alpha factors with  `model_matrix`  and  `get_formula`  functions👍

	```
	model_matrix(get_formula(alpha_factors, "SpecRisk"), data = universe)
	```

- [x] The function  `get_alpha_vec`  correctly creates a vector of alpha factors. To do this, they must add the rows of the Matrix of Alpha Factors and multiply the result by 1e-4.

	The returned  `alpha_vac`  should have shape (2265,)

	Good job! You correctly create a vector of alpha factors with the required scaling  `1e-4`.🙌

	```
	alpha_vec =  1e-4 * B_alpha.sum(axis=1)
	```

## Objective function

- [x] The  `obj_func(h)`  function correctly implements the objective function. The equation of the objective function is given in the notebook.

	Great! You successfully implement the objective function.👍

	```
	risk_factor = 0.5 * risk_aversion * scipy.linalg.norm(Q @ h) ** 2
	idiosyncratic_risk = 0.5 * risk_aversion * np.dot(h ** 2, specVar)
	portfolio_return = np.dot(h, alpha_vec)
	trans_cost = np.dot((h - h0) ** 2, Lambda)
	f = risk_factor + idiosyncratic_risk - portfolio_return + trans_cost
	```

## Gradient

- [x] The  `grad_func(h)`  function correctly implements the gradient of the objective function. The equation of the gradient of the objective function is given in the notebook.

	Well done, you successfully implement the gradient of the objective function with  `np.matmul`.👏

	```
	g = risk_aversion * (np.matmul(QT, np.matmul(Q,h)) + (specVar * h) ) - alpha_vec + 2 * (h-h0) * Lambda
	```

## Optimize

- [x] The function  `get_h_star`  correctly optimizes the objective function using the following functions  `obj_func`,  `grad_func`, and  `scipy.optimize.fmin_l_bfgs_b`.

	The returned  `h_star`  should have shape (2265,)

	Well done! You correctly optimize the objective function with  `scipy.optimize.fmin_l_bfgs_b`💯

## Risk Exposures

- [x] The function  `get_risk_exposures`  correctly calculates the portfolio's risk exposures

	The returned  `risk_exposures`  Pandas series should have shape (77,). The index of this Pandas Series should correspond to the risk factors such as 'USFASTD_AERODEF', 'USFASTD_AIRLINES', 'USFASTD_ALUMSTEL', ......

	Perfect! You correctly calculate the portfolio's risk exposures with  `np.matmul`  function👍

	```
	risk_exposures = np.matmul(BT, h_star)
	```

- [x] The function  `get_portfolio_alpha_exposure`  correctly calculates the portfolio's alpha exposures.

	The returned  `portfolio_alpha_exposure`  Pandas series should have shape (4,). The index of this Pandas Series should should correspond to the 4 alpha factors chosen at the beginning, namely:

	"USFASTD_1DREVRSL"  
"USFASTD_EARNYILD"  
"USFASTD_VALUE"  
"USFASTD_SENTMT"

	Fantastic! You correctly calculate the portfolio's alpha exposures with the given  `B_alpha`  matrix .🎉

	```
	alpha_exposures = pd.Series(np.matmul(B_alpha.transpose(), h_star), index = colnames(B_alpha))
	```

## Transaction Costs

- [x] The function  `get_total_transaction_costs`  correctly calculates the total transaction costs according to the equation given in the notebook.

	Perfect! You correctly calculate the total transaction costs according to the equation given in the notebook.🎉

	```
	total_transaction_costs = np.dot((h_star - h0) ** 2, Lambda)
	```

## Profit-and-Loss (PnL) attribution

- [x] Correctly calculate the PnL attributed to the alpha factors, the PnL attributed to the risk factors, and attribution to cost.

	To calculate the alpha and risk exposures they must use the provided  `partial_dot_product`  function

	Good job! You correctly calculate all the related PnL.💯

	```
	df.at[dt,"attribution.alpha.pnl"] = partial_dot_product(fr, p["alpha.exposures"])
	df.at[dt,"attribution.risk.pnl"] = partial_dot_product(fr, p["risk.exposures"])
	df.at[dt,"attribution.cost"] = p["total.cost"]
	```

## Build portfolio characteristics

- [x] Correctly calculates the sum of long positions, short positions, net positions, gross market value, and amount of dollars traded.

	Good job! You correctly calculate all the numbers👍

	```
	df.at[dt,"long"] = np.sum(h[h > 0])
	df.at[dt,"short"] = np.sum(h[h < 0])
	df.at[dt,"net"] = np.sum(h)
	df.at[dt,"gmv"] = np.sum(abs(h))
	df.at[dt,"traded"] = np.sum(np.abs(tradelist['h.opt'] - tradelist['h.opt.previous']))
	```
