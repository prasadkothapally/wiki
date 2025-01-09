#Tables

##list
Table Name	|	Source	|	Description
----	|	----	|	----
scheme_lt	|	Morningstar	|	Lookup table for the isins/funds. Contains benchmark, category and fund details of the funds.
stg_cams_schemes	|	RTA	|	Direct data dump of Cams schemes without validations
stg_karvy_schemes	|	RTA	|	Direct data dump of Karvy schemes without validations
stg_cams_transactions	|	RTA	|	Direct data dump of Cams transactions without validations
stg_karvy_transactions	|	RTA	|	Direct data dump of Karvy transactions without validations
cams_schemes	|	RTA	|	Validated Cams schemes
karvy_schemes	|	RTA	|	Validated Karvy schemes
cams_transactions	|	RTA	|	Validated Cams transactions
karvy_transactions	|	RTA	|	Validated Karvy transactions
schemes	|	RTA	|	Combined data of Cams and Karvy schemes
transactions	|	RTA	|	Combined data of Cams and Karvy transactions
import_errors	|	Internal	|	To track any errors in the data
accounting	|	Internal	|	Accounting data performed on top of RTA transactions
scheme_lt_amfi	|	Amfiindia	|	Lookup table for the funds from amfiindia
scheme_navs	|	Amfiindia	|	Scheme Navs data in columnar format
net_asset_value	|	Amfiindia	|	Scheme Navs data in row format
benchmark_lt	|	Morningstar	|	Lookup table for benchmark data
benchmark_nav	|	Morningstar	|	Benchmark Navs data
performance_metrics	|	Internal	|	Contains returns calculated on top of accouting data for pan-folio-isin level
benchmark_analytics	|	Prashanta Das (Python Code)	|	Monthly analytics of benchmark
category_analytics	|	Prashanta Das (Python Code)	|	Monthly anlytics of category
fund_analytics	|	Prashanta Das (Python Code)	|	Monthly analytics of fund
fund_facts_daily_return	|	Morningstar	|	Daily returns of funds
fund_facts_monthly_return	|	Morningstar	|	Monthly returns of funds
category_average_daily_return	|	Morningstar	|	Daily returns of category averages
category_average_monthly_return	|	Morningstar	|	Monthly returns of category averages
benchmark_daily_return	|	Morningstar	|	Daily returns of benchmark data
benchmark_monthly_return	|	Morningstar	|	Monthly returns of benchmark data
benchmark_facts	|	Morningstar	|	Combined data of daily and monthyly returns of benchmark
category_facts	|	Morningstar	|	Combined data of daily and monthly returns of category averages
fund_facts	|	Morningstar	|	Combined data of daily and monthly returns of funds
benchmark_p2p_returns	|	Internal	|	p2p returns of benchmark
benchmark_cy_returns	|	Internal	|	cy returns of benchmark
benchmark_sip_returns	|	Internal	|	SIP returns of benchmark
category_avg_p2p_returns	|	Internal	|	p2p returns of category averages
category_avg_cy_returns	|	Internal	|	cy returns of category averages
category_avg_sip_returns	|	Internal	|	SIP returns of category averages
fund_p2p_returns	|	Internal	|	p2p returns of funds
fund_cy_returns	|	Internal	|	cy returns of funds
fund_sip_returns	|	Internal	|	SIP returns of funds
fund_attributes	|	RTA and Morningstar	|	Fund level details required for UI team
category_avg_daily_navs	|	Internal	|	Category averages daily wise
category_avg_month_end_navs	|	Internal	|	Category averages monthly wise
benchmark_month_end_nav	|	Internal	|	Benchmark month end navs - loaded once in month
category_avg_month_end_navs_returns	|	Internal	|	
benchmark_monthly_returns	|	Internal	|	
scheme_month_end_nav	|	Internal	|	
scheme_monthly_returns	|	Internal	|	
category_lt	|	Morningstar	|	Lookup table for categories

Click [here](https://techwaveinc.sharepoint.com/:x:/r/sites/TW-VPLCoE-CoreTeam/_layouts/15/Doc.aspx?sourcedoc=%7B0876879C-959B-4C74-BB1D-36B29EFCBFB9%7D&file=TablesList.xlsx&action=default&mobileredirect=true) for the description of the tables.

