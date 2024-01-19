# Mirror Chart Expert Advisor

The Mirror Chart Expert Advisor is a trading tool that allows users to display two different currency pairs on a single chart. It utilizes colored candles to visually represent the correlation between the two pairs, making it easier for traders to identify and analyze the relationship between the pairs. The expert advisor is compatible with various trading instruments and ensures accurate and reliable data representation.

## Features
- Displays two different currency pairs on one chart.
- Uses colored candles to visually represent the correlation between the pairs.
- Enables easy distinction between correlated pairs.
- Streamlines information for easy comprehension.
- Provides compatibility with various trading instruments.
- Ensures accurate and reliable data representation.

## Usage
1. Set the desired currency pair symbols for Symbol 1 (`g_symbol1`) and Symbol 2 (`g_symbol2`) in the global variables section.
2. Set the desired colors for the candles of Symbol 1 (`g_color1`) and Symbol 2 (`g_color2`) in the global variables section.
3. Run the expert advisor.
4. The main chart will display Symbol 1, and the mirror chart will display Symbol 2.
5. The correlation between the pairs will be visually represented by the colored candles on both charts.

## Example
```mql5
#include <Trade\Trade.mqh>

string g_symbol1 = 'EURUSD';  // Symbol 1
string g_symbol2 = 'GBPUSD';  // Symbol 2
color g_color1 = clrRed;      // Color for Symbol 1
color g_color2 = clrBlue;     // Color for Symbol 2

void OnStart()
{
   // Open the main chart
   ChartOpen(g_symbol1, 0);

   // Open the mirror chart
   ChartOpen(g_symbol2, 1);

   // Set chart properties
   ChartSetInteger(0, CHART_MODE, CHART_MODE_MIRROR);
   ChartSetInteger(1, CHART_MODE, CHART_MODE_MIRROR);

   // Display the correlation between the pairs
   DisplayCorrelation();
}

void DisplayCorrelation()
{
   int timeframe = PERIOD_CURRENT;  // Current timeframe

   // Loop through the chart
   for (int i = 0; i < Bars(g_symbol1, timeframe); i++)
   {
      // Get the open, high, low, and close prices for Symbol 1
      double open1 = iOpen(g_symbol1, timeframe, i);
      double high1 = iHigh(g_symbol1, timeframe, i);
      double low1 = iLow(g_symbol1, timeframe, i);
      double close1 = iClose(g_symbol1, timeframe, i);

      // Get the open, high, low, and close prices for Symbol 2
      double open2 = iOpen(g_symbol2, timeframe, i);
      double high2 = iHigh(g_symbol2, timeframe, i);
      double low2 = iLow(g_symbol2, timeframe, i);
      double close2 = iClose(g_symbol2, timeframe, i);

      // Draw the candles for Symbol 1
      DrawCandle(0, i, open1, high1, low1, close1, g_color1);

      // Draw the candles for Symbol 2
      DrawCandle(1, i, open2, high2, low2, close2, g_color2);
   }
}

void DrawCandle(int chartIndex, int index, double open, double high, double low, double close, color color)
{
   // Select the chart
   ChartSetInteger(chartIndex, CHART_WINDOW_IS_VISIBLE, true);
   ChartSetSymbolPeriod(chartIndex, g_symbol1, PERIOD_CURRENT);

   // Draw the candle
   ObjectCreate(chartIndex, 'Candle' + index, OBJ_TREND, 0, Time[index], low, Time[index], high);
   ObjectSetInteger(chartIndex, 'Candle' + index, OBJPROP_COLOR, color);
   ObjectSetInteger(chartIndex, 'Candle' + index, OBJPROP_STYLE, STYLE_CANDLE);
   ObjectSetDouble(chartIndex, 'Candle' + index, OBJPROP_PRICE_OPEN, open);
   ObjectSetDouble(chartIndex, 'Candle' + index, OBJPROP_PRICE_CLOSE, close);
}
```

For detailed reviews and trading results of this product, you can visit [Forex Robot Easy](https://forexroboteasy.com/forex-robot-review/mirror-chart-review-simplified-forex-trading-with-visual-correlation/). Please note that ForexRobotEasy is not the official developer of this product. This code serves as a sample that can work as described in the product. To find the official developer of this product, please use MQL5.
