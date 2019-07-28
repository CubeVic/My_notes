To plot we use the function `plot#()` were # is a number that identify the plot, this number can be from 1 to 99

The basic structure of a plot statement for an indicator:
**PlotN:** PlotN(numeric expression, "plot name"); *//(where N = 1 to 99, no space)*

*Usage Example1:*
Plot1(Close, "The Close");
*Usage Example2:*
Plot1(High, "The High"); Plot2(Low, "The Low");

## Modify structure of `plot`

The complete structure of a plot statement for an indicator:
**PlotN:** PlotN(numeric expression, "plot name", foreground color, background color, width);

*Usage Example:*
Plot1(Close, "The Close", Red, Default, 3);

*Note:** It is generally more useful to set colors and width for an indicator conditionally based on some technical condition than to hard-code colors in the plot statement. There are three reserved words that can be used for this purpose: `SetPlotColor`, `SetPlotBGColor`, and `SetPlotWidth`.

## PlotPB
The `PlotPB` statement is a specialized plot statement that is used in PaintBar studies. 

It instructs Multicharts where to draw on a bar so that the bar is painted a different color from the other bars based on some conditional criteria. 

The structure of a PlotPB statement for a PaintBar is:

**PlotPB:** PlotPB(Price Point, Price Point, "plot name");

*Usage Example1 (paint full bar) :*
```
if Close > Close[1] then
    PlotPB(High, Low, "Up Bar"); Usage Example2 (paint top half of the bar):
if Close > Close[1] then
    PlotPB(High, High - Range * .5, "Up Bar");
```

In these examples the reserved word PlotPB is used to paint the bars, or a portion of the bar, a different color based on a specified condition.

*Usage Example3 (paint entire bar and set color):* 
```
if Close > Close[1] then
    PlotPB(High, Low, "Up Bar", Cyan);
```

In these examples the reserved word PlotPB is used to paint the bar a different color and the color is specified in the PlotPB statement.

## NoPlot

The `NoPlot` statement removes a specified drawn plot from the current bar. It is most often used to remove ShowMe or PaintBar plots that are no longer true on the current in-progress bar. If a ShowMe or PaintBar condition is true on the real-time in-progress bar, but during the same bar becomes false before the close of the bar, the drawn ShowMe or PaintBar can be removed with NoPlot.
The structure of a NoPlot statement for an indicator is: 

*NoPlot:* `NoPlot(plot number);`

*Usage Example:*
```
if (High < Low[1]) Then
    Plot1(Low[1], "GapDown")
Else
    NoPlot(1) ;
```

This ShowMe example marks the low price of a gap-down bar, but removes the ShowMe marker if the condition is no longer true on the real-time bar.

*Usage Example:*

```if Close > Average(Close,10) then
          PlotPB(High, Low, "Up Bar")
Else
    NoPlot(1);
```

This PaintBar example paints the entire bar if the Close is greater than the average Close but removes the PaintBar if the condition is no longer true on the real-time bar. You may use number 1 to refer to a PlotPB statement in the NoPlot parameter.

## Displacing Plots

Displacing plots allows you to visually move any analysis technique plots left or right on the chart by some number of specified bars. A positive number moves the plot to the left and a negative number moves the plot to the right. Space to the right of the last bar must be sufficient to accommodate the displaced plots or an error will occur.
 
The structure of a NoPlot statement for an indicator is:

**Plot1[+/-N ] ** Square brackets after the Plot statement are used to indicate the number of bars to displace the plot left or right. Positive = left and Negative = right.

*Usage Example1 (displacing a plot into the future):* 
```
Plot1[-5](Average(Close,5), “avg close”);
```

*Usage Example2 (displacing a plot historically):*
```
Plot1[5](Average(Close,5), “avg close”);
```

These examples move the plot right and left, respectively, on the chart.