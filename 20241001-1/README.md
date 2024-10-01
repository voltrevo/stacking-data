Scores from 3,708,700 games from 37,087 starting positions (played 100 times each).

Data is grouped by position, includes the average final score for convenience, followed by each individual score.

These games were played using a combination of the score and prediction models of turbostack at revision 879be83.

To generate each position:
- The score model was used to play a complete game
- A random position was taken from the game
- Then the smaller of three `Math.random()` values was taken (in the range 0 to 1 but biased towards 0)
- This number was used to pick a number of lines remaining in the range `[0,stdMaxLines)`
  - Endgame positions are easier to learn because the reduced uncertainty results in the final score averages being closer to their true averages
  - This also increases the speed of data generation
- 50% of the time an extra random move was played
  - This reflects the type of positions the model will be asked to evaluate, since we always ask to evaluate all possible moves from a given position

From each position, the game was then played 100 times to obtain each final score sample.

With 100 games played per position, the uncertainty in the finalScore average is reduced by 10x. These uncertainties after the 10x reduction are often still substantial.

Here are some stats from the first 5 positions (from a previous similar dataset):

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
