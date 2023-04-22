---
layout: post
title: Zero Lag
description: Zero Lag
summary: Zero Lag
author:
- Pavan Donthireddy
usemathjax: true
tags: [filters, feedback]
original: zerolag
---

Here, we acknowledge the EMA filter has an error term. That error for the current data sample is just Price – EMA[1]. We introduce this error term into the equation in addition to the value of the new data sample. We further change the amplitude of the error term by multiplying the error by a gain term. We call the new filter EC (for Error Correcting) instead of EMA. So the equation for the EC filter is:

$$EC = \alpha*(Price + gain*(Price – EC[1])) + (1 – \alpha)*EC[1];$$

The equation is simple, but its results are profound. If the gain is zero, the EC becomes just an EMA.
If the gain is sufficiently large the error term causes EC to exactly track the price for all practical
purposes. That is, there is virtually no lag and virtually no smoothing. 

Therefore, we seek a value of gain that is a happy medium between tracing out the price and tracing out the EMA. We do this by limiting the maximum amount of allowable gain. If the difference between the price and the previous value of EC is small we do not want a large value of gain. Further, the previous value of EC can be either greater than or less than the current price. 

Therefore, to properly apply the error correction the gain must swing both positive and negative.



There are two user inputs: the length of the equivalent SMA and the Gain Limit. Actually the Gain Limit input is ten times the actual gain used in the computation because the error correcting loop variable increments in steps of 1 and we want the gain to be incremented in steps of 0.1. 

The smoothing factor alpha and EMA are computed after the variables are declared.
Next, a loop searches for the least amount of error, varying gain from the lower Gain Limit to the
upper Gain Limit. When a lower error is computed, the values of best gain and least error are
recorded. Once the loop has completed its work, the BestGain value is used to compute the Error
Corrected (EC) indicator. Then, both the EMA and EC are plotted on the chart.

```
Inputs:
	Length(20),
	GainLimit(50);
Vars:
	alpha(0),
	Gain(0),
	BestGain(0),
	EC(0),
	Error(0),
	LeastError(0),
	EMA(0);
alpha = 2 / (Length + 1);
EMA = alpha*Close + (1 - alpha)*EMA[1];
LeastError = 1000000;
For Value1 = -GainLimit to GainLimit Begin
	Gain = Value1 / 10;
	EC = alpha*(EMA + Gain*(Close - EC[1])) + (1 - alpha)*EC[1];
	Error = Close - EC;
	If AbsValue(Error) < LeastError Then Begin
		LeastError = AbsValue(Error);
		BestGain = Gain;
	End;
End;
EC = alpha*(EMA + BestGain*(Close - EC[1])) + (1 - alpha)*EC[1];
```

