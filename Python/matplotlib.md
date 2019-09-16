


> Written with [StackEdit](https://stackedit.io/).

# Matplotlibe notes


### Create plots using a loop

```python
def one_hot_econdig_plot(df, var):
    df = df.copy()
    df.groupby(var)[var].count().plot.bar()
    plt.title(var)
    plt.ylabel('Number of agents')
    plt.savefig('images/pipeline-05-discretization' + var + '.png')
    plt.show()

for var in variables_for_plot:
    one_hot_econdig_plot(train_t_o, var)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU3NzEzNjQ5MF19
-->