Preliminaries
- Basic soft actor critic update loop for compatability with CalQL.
- lightweight FFN to parametrize control (2 layers,feedforward dim= 256,activation = GeLU)
- use offline datasets from minari: https://github.com/Farama-Foundation/Minari 
- task is half-cheetah from mujoco 

1. Dip in the training curve from offline to online

2. critic overestimation with warmstart only on offline expert 
- if we train do WRSL style td updates only on the offline expert,
then fine tune online, we would expect to see Q > MC rewards because of Q learning's tendency for overestimation bias. It will take a bit to unlearn this when we move to lnine RL.


3. critic underestimation with warmstart on pessimisic updates (calQL, WSRL, min Q updates, you pick)
- If we do CalQL style updates, too much regularization is enforced, which caues Q to be lower than actual MC returns. This promotes exploration but also leads to slower convergence. 
- Q-v.s. MC plots should demonstrate Q < MC 

4. critic estimation improving with larger ensemble sizes
- do 2., but take minimum over an ensemble of critics. Try an ensemble of size 2, 4, and 8. 



