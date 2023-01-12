# 数据分析

## 工具库
安装包
```sh

conda install -c conda-forge geopandas
```
```python
import pandas as pd
```

## sklearn
参见
- [主页](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html)
一个机器学习框架

## 决策树
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

## 随机森林

```py
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_absolute_error

forest_model = RandomForestRegressor(random_state=1)
forest_model.fit(train_X, train_y)
melb_preds = forest_model.predict(val_X)
print(mean_absolute_error(val_y, melb_preds))
```

## 线性回归
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

## 地图库

地图
```py
import geopandas as gpd

# 画国家的边境线
# alpha 透明度
world = gpd.read_file(gpd.datasets.get_path('naturalearth_lowres'))
china = world.loc[world.name.str.contains('China')]
ax = china.plot(figsize=(12,12), color='white', linestyle=':', edgecolor='gray')
path.plot(ax=ax, color='red', markersize=30, alpha=0.4)
# 根据Point画出Line
```

过滤字符串
```
world.loc[world.name.str.contains('ina')]
```

地图标记
```py
import folium 
from folium import Marker
from folium.plugins import MarkerCluster

```

分级统计图
```py
import folium
from folium import Choropleth
from folium.plugins import HeatMap
# Create a base map
m_4 = folium.Map(location=[35,136], tiles='cartodbpositron', zoom_start=5)

# Your code here: create a map
# Create a map
def color_producer(magnitude):
    if magnitude > 6.5:
        return 'red'
    else:
        return 'green'

Choropleth(
    geo_data=prefectures['geometry'].__geo_interface__,
    data=stats['density'],
    key_on="feature.id",
    fill_color='BuPu',
    legend_name='Population density (per square kilometer)').add_to(m_4)

# 画圆
for i in range(0,len(earthquakes)):
    folium.Circle(
        location=[earthquakes.iloc[i]['Latitude'], earthquakes.iloc[i]['Longitude']],
        popup=("{} ({})").format(
            earthquakes.iloc[i]['Magnitude'],
            earthquakes.iloc[i]['DateTime'].year),
        radius=earthquakes.iloc[i]['Magnitude']**5.5,
        color=color_producer(earthquakes.iloc[i]['Magnitude'])).add_to(m_4)
```

## 位置
火锅店与奶茶店
医院与煲汤店