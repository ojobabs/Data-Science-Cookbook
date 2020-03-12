


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
## References

- [Line plot or Line chart in Python with Legends](http://www.datasciencemadesimple.com/line-plot-line-chart-in-python-legends/)
- [Matplotlib Style Gallery](https://tonysyu.github.io/raw_content/matplotlib-style-gallery/gallery.html)
-  [Customizing Matplotlib with style sheets and rcParams](https://matplotlib.org/tutorials/introductory/customizing.html)
- [matplotlib](https://matplotlib.org/index.html)

## Spaghetti Line Plot

```python
plt.figure(figsize=(10,7))
prc_cli1 = expOneTwo[expOneTwo['go'] == 'D54']['prcClientsInsideOne']
prc_cli2 = expOneTwo[expOneTwo['go'] == 'S27']['prcClientsInsideOne']
prc_cli3 = expOneTwo[expOneTwo['go'] == 'V68']['prcClientsInsideOne']
prc_cli4 = expOneTwo[expOneTwo['go'] == 'V79']['prcClientsInsideOne']
prc_cli5 = expOneTwo[expOneTwo['go'] == 'V65']['prcClientsInsideOne']
prc_cli6 = expOneTwo[expOneTwo['go'] == 'V73']['prcClientsInsideOne']
prc_cli7 = expOneTwo[expOneTwo['go'] == 'V46']['prcClientsInsideOne']
prc_cli8 = expOneTwo[expOneTwo['go'] == 'S51']['prcClientsInsideOne']
prc_cli9 = expOneTwo[expOneTwo['go'] == 'V61']['prcClientsInsideOne']
prc_cli10 = expOneTwo[expOneTwo['go'] == 'V56']['prcClientsInsideOne']
prc_cli11 = expOneTwo[expOneTwo['go'] == 'A22']['prcClientsInsideOne']
prc_cli12 = expOneTwo[expOneTwo['go'] == 'V42']['prcClientsInsideOne']
prc_cli13 = expOneTwo[expOneTwo['go'] == 'D57']['prcClientsInsideOne']
prc_cli14 = expOneTwo[expOneTwo['go'] == 'D56']['prcClientsInsideOne']
prc_cli15 = expOneTwo[expOneTwo['go'] == 'S19']['prcClientsInsideOne']
prc_cli16 = expOneTwo[expOneTwo['go'] == 'A64']['prcClientsInsideOne']
prc_cli17 = expOneTwo[expOneTwo['go'] == 'S89']['prcClientsInsideOne']
prc_cli18 = expOneTwo[expOneTwo['go'] == 'A29']['prcClientsInsideOne']
prc_cli19 = expOneTwo[expOneTwo['go'] == 'S82']['prcClientsInsideOne']
prc_cli20 = expOneTwo[expOneTwo['go'] == 'D07']['prcClientsInsideOne']
prc_cli21 = expOneTwo[expOneTwo['go'] == 'S69']['prcClientsInsideOne']
prc_cli22 = expOneTwo[expOneTwo['go'] == 'S75']['prcClientsInsideOne']
prc_cli23 = expOneTwo[expOneTwo['go'] == 'S68']['prcClientsInsideOne']
prc_cli24 = expOneTwo[expOneTwo['go'] == 'S74']['prcClientsInsideOne']
line_chart1 = plt.plot(np.arange(20, 130, 10), prc_cli1)
line_chart2 = plt.plot(np.arange(20, 130, 10), prc_cli2)
line_chart3 = plt.plot(np.arange(20, 130, 10), prc_cli3)
line_chart4 = plt.plot(np.arange(20, 130, 10), prc_cli4)
line_chart5 = plt.plot(np.arange(20, 130, 10), prc_cli5)
line_chart6 = plt.plot(np.arange(20, 130, 10), prc_cli6)
line_chart7 = plt.plot(np.arange(20, 130, 10), prc_cli7)
line_chart8 = plt.plot(np.arange(20, 130, 10), prc_cli8)
line_chart9 = plt.plot(np.arange(20, 130, 10), prc_cli9)
line_chart10 = plt.plot(np.arange(20, 130, 10), prc_cli10)
line_chart11 = plt.plot(np.arange(20, 130, 10), prc_cli11)
line_chart12 = plt.plot(np.arange(20, 130, 10), prc_cli12)
line_chart13 = plt.plot(np.arange(20, 130, 10), prc_cli13)
line_chart14 = plt.plot(np.arange(20, 130, 10), prc_cli14)
line_chart15 = plt.plot(np.arange(20, 130, 10), prc_cli15)
line_chart16 = plt.plot(np.arange(20, 130, 10), prc_cli16)
line_chart17 = plt.plot(np.arange(20, 130, 10), prc_cli17)
line_chart18 = plt.plot(np.arange(20, 130, 10), prc_cli18)
line_chart19 = plt.plot(np.arange(20, 130, 10), prc_cli19)
line_chart20 = plt.plot(np.arange(20, 130, 10), prc_cli20)
line_chart21 = plt.plot(np.arange(20, 130, 10), prc_cli21)
line_chart22 = plt.plot(np.arange(20, 130, 10), prc_cli22)
line_chart23 = plt.plot(np.arange(20, 130, 10), prc_cli23)
line_chart24 = plt.plot(np.arange(20, 130, 10), prc_cli24)
plt.title('Prc. Clients Inside Local Market by Driving Time \n All GOs')
plt.xlabel('Driving Time (minutes)')
plt.ylabel('Prc. Clients Inside LM')
plt.xticks(np.arange(20, 130, 10))
plt.legend(['D54-KANSAS', 'S27-GR. SAN FRANCISCO', 'V68-QUEENS',
            'V79-BROOKLYN', 'V65-LONG ISLAND', 'V73-GREATER NEW YORK',
            'V46-NORTHEASTERN PENN.', 'S51-SEATTLE', 'V61-NASSAU',
            'V56-BOSTON', 'A22-SAVANNAH', 'V42-GREATER PHILADELPHIA',
            'D57-CEDAR RAPIDS', 'D56-WISCONSIN', 'S19-SANTA CLARA',
            'A64-NORTHERN OHIO', 'S89-HAWAII', 'A29-GREENVILLE', 'S82-UTAH',
            'D07', 'S69-LOS ANGELES', 'S75-GREATER PASADENA',
            'S68-SAN FERNANDO VALLEY', 'S74-ORANGE COAST'], loc='upper center',
            bbox_to_anchor=(0.5, -0.10), fancybox=True, shadow=True, ncol=3)
#plt.savefig('images/lm_exp_spaghetti.png') # do not work propertly
plt.show()
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczOTcwNTcyNSw0NTk5MTcyMzQsLTczMz
Q2NDY3Ml19
-->