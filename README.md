# Equity-Index-Derivatives-Weighting-Arbitrage-and-Research-Dashboard-

Report and ipynb file inside zip
[Capstone Paper.docx](https://github.com/Jason-B-Ang/Equity-Index-Derivatives-Weighting-Arbitrage-and-Research-Dashboard-/files/10569875/Capstone.Paper.docx)
Equity-Index Derivatives Weighting, Arbitrage, and Research Dashboard 
By: Jason Ang, Ezzard Bradford, and Douglas Harrison 
Abstract
In financial management, managers of large funds engage in a myriad of investment strategies in an effort to outperform the market and simultaneously minimize risk. One investment strategy in particular, index arbitrage, is especially lucrative due to its low-risk and steady returns thanks to diversification. Our Equity-Index Derivatives Weighting, Arbitrage, and Research Dashboard (or Edward, for short) seeks to increase the ease with which fund managers engage in index arbitrage. 
Introduction 
Our group sought to demonstrate our mastery of the concepts taught in MAD2502 over the course of the fall semester. To best demonstrate our mastery of these concepts, we chose to apply our understanding of data frame manipulation, numerical methods, and object-oriented programming to an area of mutual interest: computational finance. The financial markets contain a plethora of data ranging from the noisiness of spot prices to the dictionary-worthy weightings of individual equities in equity indexes. 
Edward concerns itself with futures contracts on equity-indexes, and the individual equities underlying these indexes. Futures contracts are a type of a financial derivative: counterparties engage in a futures contract to buy or sell a particular commodity, currency, or security at a predetermined price at a specified time in the future. Some use futures contracts to hedge against adverse movements in the underlying assets of futures; others use futures contracts to speculate on favorable movements in the underlying assets of futures. Pick your poison: Edward chose to speculate.
For the sake of practicality, and time, we chose to tailor Edward to futures on the NASDAQ-100 equity index. The NASDAQ-100, or NDX, is an equity-index that tracks the market capitalizations of roughly 102 different equities across multiple sectors. Each equity’s weight in the index is proportional to their market capitalization (i.e., if the index’s total market capitalization is $19 trillion and Apple’s market capitalization is $2.3 trillion, then Apple’s weight in the NDX would be $2.3 trillion / $19 trillion = 0.12). The NDX provides a relatively whole view of the market, as such we decided to include its futures contracts in our universe of securities.
Related Work
The bulk of our work is built on the foundation established by Fama (1991) and Hull (2022): Fama being notable for coining the Efficient Market Hypothesis and Hull for increasing access to derivative pricing methods (of which are of great interest to us).
From Fama (1991), we learn that equities markets exist in equilibrium: equities (and the indexes containing them) experience means which they revert to over time. While Edward does not concern itself with determining mean reversion signals, it does have set instructions for portfolio construction based on the NDX’s disequilibria (i.e., changing equity and futures positions based on the NDX futures spot relative to the equity-index futures pricing model). These instructions, established by Hull (2022), are as follows: if the spot price of an equity index future is greater than the value calculated by the equity-index futures pricing model, go short the contract and go long its component equities. Else, go long the contract and short its component equities.
While we referred to Fama and Hull frequently, Hull served as the main source of information for equity-index pricing, arbitrage, and portfolio construction. Hull (2022) contains many models (or equations) for pricing various derivative products and offers both insight into each model’s limitations as well as real-world applications. From Hull (2022), we made the following assumptions:
1.	Market participants are subject to no transaction costs when they trade.
2.	Market participants can borrow at the same risk-free rate as that they lend.
3.	Market participants are able to self-finance, they are not obligated to borrow.
4.	Market participants take advantage of arbitrage opportunities as they occur.

Edward’s Evolution
Initially, we were very ambitious and wanted to price not only equity-index futures, but also equity-index futures options and equity-index swaps. Additionally, some members (Douglas) wanted to develop a webpage using the dash library. However, in the given timeline, we realized it would be impossible to produce a quality program that contained all the aforementioned features. As such, we settled on equity-index futures, and called it a day. Here’s some media recording this journey:









Our first brainstorming session…
 

And our most recent brainstorming session…
 


Our Problem: Constructing the Ideal Portfolio
Our group wanted to solve a problem faced by many fund managers: tackling idex arbitrage properly. We asked ourselves: “how can you construct a portfolio of equity and futures such that risk is optimally hedged?” What data would we need, and what numerical methods would we have to perform? How many contracts are we to go long or short? These are all questions we asked as we attempted to solve this problem. 

Solution
Our group decided to create a large class that examines the NDX and its components. Our Equity-Index Derivatives Weighting, Arbitrage, and Research Dashboard (Edward) takes user input concerning their risk tolerance, time horizon, and cash on hand and generates an ideal portfolio of said stock and n futures contracts on said stock such that the user’s risk is hedged. EDWARD uses theoretical concepts and formulas to create a derivative investing dashboard to help the end user to make better decisions and to help minimize risk and hedge the risk for their stocks against the volatility of the stock market using Futures contracts. It was developed through the collaboration of Jason Ang, Douglass Harrison, and Ezzard Bradford. 

Distribution of work
Each and every member wanted to contribute equal effort toward Edward’s success. Accordingly, we distributed responsibilities evenly: Jason (PEP 8 formatting, loops, class structure); Douglas (comments, numerical methods, portfolio construction); Ezzard (libraries, variables, validation). Each group member defined functions, wrote comments, worked on our paper, and formatted our PowerPoint..

Organization
For the sake of practicality, we decided to house all our functions within one large class. We make use of many functions, but each one serves one of three purposes: data cleaning (i.e., nasdaq100_weights), relevant numerical methods (i.e., futures_price), or data visualization (i.e., portfolio construction).

Beyond structure, we also made sure to code with consistency and purpose in mind. We not only strictly followed the PEP8 guide for coding in python but also eliminated excess code whenever possible. 
Implementation and Organization of Project
The project is organized in one class, Edward. To instantiate an object there are various input for the parameters of the constructor.

Variable name	Data Type	Purpose
tolerance	string	User’s risk tolerance
expiry	string	Expiration date of contract
liquid	float	Determining positions



Edward’s class attributes are as follows:
Attribute name	Data Type	Purpose
self.index_components	Csv file	Imports csv containing all components of NDX
self.tolerance	float	Stores float of User’s stated risk tolerance
self.today	string	Stores string for today’s date
self.t0	Datetime object	Stores datetime object for today’s date
self.tf	Datetime object	Stores datetime object for expiry date
self.dt	float	Stores time until expiry as a fraction of a year
self.n_c	float	Stores user’s cash (for self-financing)

Functions and Numerical Methods
Function Name	Data Type	Purpose
r_f	float	Calculates risk free rate using average 2 year inflation as well as par yield on treasury bond with a maturity closest to self.dt. Used in futures pricing and calculating metrics.
self.equity_ticker()	yFinance object, string	returns yFinance object with argument passed (i.e., symbol of stock, index, etc.)
self.equity_price()	yFinance object, float	Using self.equity_ticker(), returns ves spot price of argument passed using the yFinanc API
self.equity_yield()	yFinance object, float	Using self.equity_ticker(), returns mean dividend issue of argument passed using the yFinanc API, the nmultiplies that value by 4 / self.equity_price() to determine annual dividend yeid 
self.nasdaq100_components()	List of strins	Returns all components of Nasdaq 100 index 
self.nasdaq100_weights()	Comma delimited lists	Returns market caps of components, total market cap of Nasdaq 100 index, and fractional weights of components relative to Nasdaq 100
self.n_s()	List of floats	Returns number of shares of a given stock, dollar amount of equity in portfolio 
self.nasdaq100_yield()	float	Returns the cumulative annual yield of equities on the Nasdaq 100 index
self.settlements()	Csv file	Reads to csv settlement prices of arguments passed (i.e., tickers, indexes, etc.)
self.r()	Comma delimited lists and floats	Returns mean returns, standard deviation, and likelihood of upward price movement for equities
self. equity_performance()	Comma delimited floats	Returns weighted mean returns, weighted expected returns, and weighted standard deviations for equities
self. beta()	Comma delimited lists	Returns beta of two arguments, sum of weighted betas of NDX components
self.sharpe_s()	Comma delimited floats	Returns excess return  (of equity segment) divided by the standard deviation of excess returns. High sharpe ration indicates high performing portfolio
self.futures_price()	float	Returns value of equity-index futures contract based on Hull (2022)
self.r_futures()	Comma delimited lists and floats	Returns mean returns, standard deviation, and likelihood of upward price movement for futures
self. ideal_futures_contracts()	float	Returns ideal number of futures contracts to be pair with equity position
self. futures_performance()	Comma delimited floats	Returns weighted mean returns, weighted expected returns, and weighted standard deviations for futures
self. sharpe_futures()	Comma delimited floats	Returns excess return  (off utures segment) divided by the standard deviation of excess returns. High sharpe ration indicates high performing portfolio
self.signal()	Comma delimited floats	Returns shares of equity, number of contracts, and treasury bonds to hold in portfolio based on movements in the spot price of NDX futures contracts Hull’s pricing model for equity index futures
self. portfolio()	Pandas data frame	Returns portfolio of instruments (i.e., equity, futures, treasury bond) with names of instruments, trade prices, quantities, and settlement prices 
self. metrics	Pandas data frame	Returns the difference between the risk of the portfolio and the user-inputted risk tolerance, excess return of the portfolio, Sharpe of portfolio, and percentage profit and loss

Results
Our group’s results seem accurate according to the theoretical formulas and concepts given to us by the resources we used. However, we aren’t sure how accurate it would be in the real world since we don’t have access to adequate capital to test Edward’s output. Put simply, our code works in theory and would need to be integrated with a prime broker to work in the real world. Additionally, it is important that Edward be seen as a software-assisted decision-making tool, not a trading algorithm. In the case that an end-user would like to use Edward for the latter application, they best do the following: 1) get access to extremely powerful processing power, 2) increase execution times through parallel computing processes like vectorization, or 3) both. If these avenues are not pursued, Edward will serve little real-world purpose in high-frequency trading (or any form of algorithmic trading for that matter).

To expand upon this, Edward can take minutes at a time to construct a list or data frame. This is impractical and requires the aforementioned updates. Another limitation we found was an edge case where certain days during the year when markets closed were unable to provide pricing data.

We overcame many challenges in this project like finding compatible data frames for us to manipulate into what we want because the libraries we use weren’t always as straightforward as just grabbing information. Sometimes we need to adjust what we have to make things work. For example, we had a data frame that wouldn’t let us index the dates since it wasn’t a column we could access, so we had to transfer data to a  csv file and convert it back to a data frame to be able to grab the dates. A particular challenge some members of the group faced was just simply conceptualizing the financial topics involved in creating the dashboard. It was not easy understanding what was going on because of our lack of experience in this type of field. Nonetheless, we were able to learn and understand through online resources. 
Conclusion
Everyone in the group learned many new methods to use for data analysis and application of concepts we learned throughout the course. Specifically, we learned how to apply and manipulate classes, data frames, csv files,  and define interesting numerical methods using application programming interfaces and libraries.

Our group believes we achieved a lot in the limited timeframe that was given, but there were still many ideas we thought about implementing to add on to this project. Our group could create a csv file of all the stock ticker symbols in indexes other than the NDX, and create multiple portfolios and rank them by Sharpe ratio. We could also learn how to weigh metrics to help create a more accurate portfolio for use. 









Works Cited
“API documentation,” API Documentation - yahoofinance documentation. [Online]. Available: https://python-yahoofinance.readthedocs.io/en/latest/api.html. [Accessed: 12-Dec-2022].

“E-mini NASDAQ-100 overview - CME group,” Futures &amp; Options Trading for Risk Management - CME Group. [Online]. Available: https://www.cmegroup.com/markets/equities/nasdaq/e-mini-nasdaq-100.html. [Accessed: 12-Dec-2022].
“Efficient Capital Markets II,” Fama, E. (1991) Efficient Capital Markets II. Journal of Finance, 46, 1575-1617. - references - scientific research publishing. [Online]. Available: https://www.scirp.org/(S(czeh2tfqyw2orz553k1w0r45))/reference/referencespapers.aspx?referenceid=2448119. [Accessed: 12-Dec-2022]. 

“Inflation nowcasting,” Federal Reserve Bank of Cleveland. [Online]. Available: https://www.clevelandfed.org/indicators-and-data/inflation-nowcasting. [Accessed: 12-Dec-2022].

J. Hull, Options, futures, and other derivatives. New York, NY: Pearson, 2022.

“Daily Treasury Par Yield Curve Rates,” U.S. Department of the Treasury. [Online]. Available: https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_yield_curve&amp;field_tdr_date_value=2022. [Accessed: 12-Dec-2022].



Appendix
Application Programming Interfaces and Libraries
•	Pandas/pandas_datareader: We used pandas to create data frames to help organize and grab data from API/Libraries and CSV files more efficiently
o	Handle settlement data for equity and NDX
o	Display portfolio in a data frame format


•	 Yfinance: We used Yfinance to grab real-time  equity data to for late use in our program


•	 Numpy: We used numpy to perform both proprietary numerical methods as well as those found in Hull (2022)


•	 Datetime: We used Datetime to determine the current date in addition to other dates relevant to our calculations
o	  Calculated elapsed time between time periods relevant to portfolio construction

