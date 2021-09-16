Easylenguage/PowerLanguage studies operate on price data, organized as a series of data points, based on a defined interval and arranged in a chronological order. Each data point is a summary of a group of price points (ticks) that includes the price values of the first and of the last tick, as well as the range of price movement over the defined interval. Data points also include additional data, such as date and time of the last tick and trade volume.

The most popular format for visually presenting a data point is a bar. References to bars in this guide actually refer to data points. Any other visual formats for presenting data points, such as candlesticks, points, lines, etc., can equally well be substituted.

PowerLanguage studies are divided into two main types: **Indicators** and **Signals**.

An **Indicator** is a visual technical analysis tool, used to analyze market conditions and identify and forecast trends and market patterns. An indicator is a visualization of a mathematical formula, and consists of one or more Plots – lines, histograms, series of points or crosses, highs and lows, left and right ticks, or a combination of the above, displayed on a chart

A **Signal** is a mechanical technical analysis tool, used to systematically specify market entry or exit points according to a set of trading rules implemented in the signal's algorithm. The trade points are indicated on a chart by ticks and arrows. Strategies can easily be constructed by combining a number of signals. Market entry or exit points, specified by the signals, can be used to send orders electronically directly to a broker, fully automating the trading process.

## Indicators

The purpose of indicators is to plot visualizations of mathematical formulas on a chart. The plots are created based on one or more price data series

When applied to a chart, an indicator script first evaluates all the completed bars one-by-one, starting with the very first (oldest) bar on the chart.

Once all the completed bars on the chart have been evaluated, an indicator script will proceed to evaluate the last bar on the chart on tick-by-tick basis, without waiting for the bar to be completed.

Each time a new tick is received, the entire script will be executed for that bar, until the bar is completed and the next bar is started. Indicator scripts treat incomplete bars the same way as the bars that are completed, and can take action each time an incomplete bar is evaluated

Update on Every Tick option can be turned off in the MultiCharts settings.

### Completed Bars (Indicators)

A bar is considered completed when it is closed and no additional ticks can be added to it.

* For time-based charts, the bar is closed once the first tick with a time stamp past the bar's interval is received, or if no additional ticks are received for a period of three seconds.
* For tick-based charts, the bar is closed once the defined number of ticks has been reached.
* For range-based charts, the bar is closed once the tick with a price outside of the original bar's range has been received.
* For volume-based charts, the bar is closed once a tick, bringing the current bar's total to the defined number of contracts, has been received.
* For change-based charts, the bar is closed once a tick with a price, bringing the current bar's total number of price changes to the defined number, has been received.

## Signals

Signals are the basic building blocks of strategies. Signals are substantially more complex than indicators and take in to account a far greater number of factors.

When applied to a chart, a signal script first evaluates all the completed bars one-by-one, starting with the very first (oldest) bar on the chart. The entire script is executed once for each completed bar. On each bar, based on the results of the evaluation, a signal script may generate one or more trading orders. Orders are indicated by an arrow or a mark on the chart, by a visual or an audio alert, etc

By default, once all the completed bars on a chart are evaluated, the execution of a signal script is paused until a new bar is completed (a bar is completed once an interval, defined for each bar, is over), and then the entire script is executed again for the new bar.

### Completed Bars (Signals)
A bar is considered completed when it is closed and no additional ticks can be added to it.

* For time-based charts, the bar is closed once the first tick with a time stamp past the bar's interval is received, or if no additional ticks are received for a period of 300 seconds.
* For tick-based charts, the bar is closed once the defined number of ticks has been reached.
* For range-based charts, the bar is closed once the tick with a price outside of the original bar's range has been received.
* For volume-based charts, the bar is closed once a tick, bringing the current bar's total to the defined number of contracts, has been received.
* For change-based charts, the bar is closed once a tick with a price, bringing the current bar's total number of price changes to the defined number, has been received.