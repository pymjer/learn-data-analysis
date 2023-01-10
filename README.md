# my-first-binder

## 工具库
```python
import pandas as pd
```

## sklearn
参见
- [主页](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html)
一个机器学习框架

决策树
```py
from sklearn.model_selection import train_test_split

# split data into training and validation data
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 0)
# Define model
# final_model = DecisionTreeRegressor(max_leaf_nodes=best_tree_size, random_state=1)
melbourne_model = DecisionTreeRegressor()
# Fit model
melbourne_model.fit(train_X, train_y)

# get predicted prices on validation data
val_predictions = melbourne_model.predict(val_X)
print(mean_absolute_error(val_y, val_predictions))
```

线性回归
```py
from sklearn.linear_model import LinearRegression
reg = LinearRegression().fit(X, y)
reg.predict(np.array([[3, 5]]))
```

结果偏差度
```py
from sklearn.metrics import mean_absolute_error

predicted_home_prices = melbourne_model.predict(X)
mean_absolute_error(y, predicted_home_prices)
```

分离训练数据和验证数据
```py
from sklearn.model_selection import train_test_split
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 0)
```

### 随机森林

```py
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

forest_model = RandomForestRegressor(random_state=1)
forest_model.fit(train_X, train_y)
melb_preds = forest_model.predict(val_X)
print(mean_absolute_error(val_y, melb_preds))
```