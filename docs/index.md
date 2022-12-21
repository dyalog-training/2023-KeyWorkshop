---
hide:
  - navigation
---

# Key Workshop
For this workshop, please attempt to solve the following problems. We recommend using the Key operator `⌸` for the main parts of the computations.

## The data
The comma-separated values file [order_data.csv](./order_data.csv) contains information about orders on a Brazilian E-commerce website from 3rd October 2016 to 29th August 2018, inclusive. This data has been adapted from [data made available by Olist Store](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

The data has the following columns:

|column name|description|type
|--|--|--|
id | unique ID for this order | number
timestamp | timestamp for this order in the format `YYYY-MM-DD hh:mm:ss` | character
city | city of residence for this customer | character
state | 2-letter state code for the state of residence for this customer | character
payment | payment amount in Brazilian Real | number
category | product category name | character

## Problems

### Payment per state
Write a function `PaymentPerState` which:

- accepts a nested vector of character vectors of state codes
- returns the total payment in each given state across the whole dataset.

```
      PaymentPerState 'GO' 'TO' 'SC'
319766.98 58068.18 579297.82
```

### Payment per city
Write a function `PaymentPerCity` which:

- accepts a nested matrix `city` in which `city[;1]` is a 2-letter state code and `city[;2]` is the name of a city within that state.
- returns the total payment in each city across the whole dataset.

```
      PaymentPerCity ↑('MS' 'bonito')('MT' 'alta floresta')('RJ' 'rio de janeiro')('SP' 'lavinia')
1085.12 4103.33 1082928.76 390.41
```

### Payment per month
Write a function `PaymentPerMonth` which:

- accepts a nested vector of character vectors of state codes
- returns a simple numeric vector or matrix of the total payment in each state in each month of 2017 in order top-to-bottom from January to December.

```
      months←'Jan' 'Feb' 'Mar' 'Apr' 'May' 'Jun' 'Jul' 'Aug' 'Sep' 'Oct' 'Nov' 'Dec'
      states←'SP' 'RJ' 'PI' 'MT'

      PaymentPerMonth 'SP'
80348.6 1886.3 239321.27 231109.84 3387.11 391137.77 2518.52 197902.88 185274.77 188394.13 140767.23 0

	  ppm←PaymentPerMonth states

	  ((⊂''),states)⍪months,ppm
             SP         RJ        PI        MT
 Jan   80348.6    33197.29   3298.4    3583.36
 Feb    1886.3   124392.15   3482     10296.63
 Mar  239321.27  108026.61   4544.47  12828.51
 Apr  231109.84  104566.94   3242.68   8101.66
 May    3387.11    1427.42  16233.55   5180.18
 Jun  391137.77  166838.56   3745.39  13144.66
 Jul    2518.52   85555.98   5072.72   6939.29
 Aug  197902.88   84167.86   2938.77  11235.49
 Sep  185274.77   59246.08   2626.96   4788.16
 Oct  188394.13   75293.52   6679.58   7560.36
 Nov  140767.23   59495.67   2582.92   2702.55
 Dec       0        825.51  13139.53    463.13
```

### Payment per quarter
Write a function `PaymentPerQuarter` which:

- accepts a nested vector of character vectors of state codes
- returns a simple numeric vector or matrix of the total payment in each state in each quarter of 2017.

```
      quarters←'Jan-Mar' 'Apr-Jun' 'Jul-Sep' 'Oct-Dec'
	  states←'SP' 'RJ' 'PI' 'MT'
      ppq←PaymentPerQuarter states

      ((⊂''),states)⍪quarters,ppq
                 SP         RJ        PI        MT
 Jan-Mar  321556.17  265616.05  11324.87  26708.5
 Apr-Jun  625634.72  272832.92  23221.62  26426.5
 Jul-Sep  385696.17  228969.92  10638.45  22962.94
 Oct-Dec  329161.36  135614.7   22402.03  10726.04
```

### Orders by category
Write a function `OrdersByCategory` which:

- accepts a nested vector of character vectors of state codes
- returns a numeric matrix `orders` for which `orders[;1]`  and `orders[;2]`

```
      states←'SP' 'RJ' 'PI' 'MT'
      (obc cat)←OrdersByCategory states
      
      ((⍳5)(1,4+⍳4))⌷((⊂''),cat)⍪states,obc
     arts_and_craftmanship  audio  auto  baby
 SP                      0      4    49    31
 RJ                      0      4    27    11
 PI                      0     54   400   330
 MT                     15    137  1576  1120
      
      ((⍳5)(1,55+⍳4))⌷((⊂''),cat)⍪states,obc
     market_place  music  musical_instruments  office_furniture
 SP             5      0                    5                14
 RJ             2      0                    5                 8
 PI            30      8                   73               210
 MT           100     11                  245               499
```
