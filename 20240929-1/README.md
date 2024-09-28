Scores from 859,000 games starting from 8,590 positions (played 100 times each).

Data is grouped by position, includes the average final score for convenience, followed by each individual score.

These games were played using the prediction model of turbostack at revision adc1d9e.

To generate each position:
- The model was used to play a complete game using temperature 1.5
  - This increases the diversity of positions, including more errors to help the model quantify the impact of errors
- Then the larger of two `Math.random()` values was taken (in the range 0 to 1 but biased towards 1)
- This number was used to pick a position from the game biased towards the end of the game
  - Endgame positions are easier to learn because the reduced uncertainty results in the final score averages being closer to their true averages
  - This also increases the speed of data generation

From each position, the game was then played 100 times using temperature 0 to obtain each final score sample.

With 100 games played per position, the uncertainty in the finalScore average is reduced by 10x. These uncertainties after the 10x reduction are often still substantial.

Here are some stats from the first 5 positions:

| Mean  | Stdev | Est Mean Error | Est Mean Rel Error |
|-------|-------|----------------|--------------------|
|  1708 |  4246 |            425 |              24.9% |
| 12569 |  4714 |            471 |               3.7% |
|  1057 |  3336 |            334 |              31.6% |
| 11900 |  7525 |            753 |               6.3% |
| 12810 |  7476 |            748 |               5.8% |

To clarify some meanings:
- **Est Mean Error**: The estimated difference between the reported mean based on 100 samples and the true mean (as a stdev)
- **Est Mean Rel Error**: The previous value expressed as a percentage of the reported mean

Scores are all reported without level scaling. Multiply by 19 for the L18 score.

## Minor Issue

Games end for two reasons - having no legal moves ('topping out') and running out of lines. Having few lines remaining would be a very strong signal for estimating the final score.

Because of the intentional poor play used to generate positions, the number of lines cleared is typically low even though each position was taken towards the end of the game. This means the lines remaining is typically high, which is the opposite of what we want.

In the next version of this dataset we should also randomize the total lines available (`linesClearedMax`) and bias towards zero.
