To demonstrate how to make lines and text in easylanguage(powerlanguage) we can create a study which goal is to track the daily extremes and to **display** them on the chart. We want to be able to see the current extremes for the day and also show yesterday’s extremes on today’s data. 

* We need to be able to find the **highest high** and **lowest low** for each day
* The study should use trendlines to display yesterday’s extremes
* We want to be able to change the appearance on the chart via inputs
* The study should display text on the chart that labels the lines

## Simple Program Logic

* Track daily high and low with a variable throughout the day
* Store the previous daily extremes on a new day and reset the tracking variables
* Draw text and trendlines for the previous extremes on today’s data and update it with every new bar
* Add inputs to be able to conveniently change the text and trendline looks (color, size etc.)

## Trendlines

Each Trendline has his own ID assigned automatically by Multicharts, to create a new trendline we need to use `TL_New` follow by 6 parameters, bellow we will create a variable to store the ID and we will name the different parameter, just to make it easier to read

```
TLID = TL_New(StartDate, StartTime, StartValue, EndDate, EndTime, EndValue);
```

so a simple code that will draw a horizontal line will be

```
Variables:
            TLID            (-1) // can be 0 but just for debugging we use -1

once
    begin
        // draw a trendline spacing over eleven bars
        TLID = TL_New(Date[10], Time[10], Close, Date, Time, Close);
    end;
```

the result will be something like:

![text_trendinglines_001](../images/text_trendinglines_001.png)

there are some characteristics of the line that we can change, those will be:

* Color: TL_SetColor(TLID,Color);
* Size: TL_SetSize(TLID,size); size will be from 0 to 6
* Style: TL_SetStyle(TLID,Style) for the style we have 5 different types, we can use reserve words or numbers as bellow

![text_trendinglines_002](../images/text_trendinglines_002.png)

so let see how the statement change after adding this settings

```
TLID =  TL_New(Date[10], Time[10], Close, Date, Time, Close);
        TL_SetColor(TLID, red);
        TL_SetSize(TLID,2);
        TL_SetStyle(TLID,2); // 2 can be change for Tool_Dashed
```

and the result will be similar to this:

![text_trendinglines_003](../images/text_trendinglines_003.png)

