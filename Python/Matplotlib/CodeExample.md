


> Written with [StackEdit](https://stackedit.io/).

# `matplotlib` examples

## Multiple line plot
Code:
```python
# Import modules
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib as mpl
plt.style.use('seaborn-deep')

# Average Prc. Clients Inside LM by Driving Time (minutes) for all GOs
plt.figure(figsize=(10,7))
prc_cli1 = lm_exp_agg_raw['prcClientsInsideOne']
prc_cli2 = lm_exp_agg_raw['prcClientsInsideTwo']
line_chart1 = plt.plot(lm_exp_agg_raw['drivingTimeOne'], prc_cli1)
line_chart2 = plt.plot(lm_exp_agg_raw['drivingTimeOne'], prc_cli2)
plt.title('Prc. Clients Inside Local Market by Driving Time \n Average for all GOs')
plt.xlabel('Driving Time (minutes)')
plt.ylabel('Average Prc. Clients Inside LM')
plt.xticks(np.arange(20, 130, 10))
plt.legend(['Experiment One', 'Experiment Two'], loc=4)
plt.savefig('images/lm_exp_agg_raw.png')
plt.show()
```
Output:

![enter link description here](https://raw.githubusercontent.com/markeyser/Data-Science-Cookbook/master/imgs/lm_exp_agg_raw.png?_sm_au_=iVVqVkTbq0kFjjHNjfc06K6ttCjRt)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1Njc5NTYzNCwtNzMzNDY0NjcyXX0=
-->