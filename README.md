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

## 地图
地图通过经纬度标明位置，其中经度正数为东经，负数为西经，纬度正数为北纬，负数为南纬

地理空间数据常用的有几类：
DEM,POI,OSM

OSM 是Open Street Map的缩写，是一款由网络大众打造的免费开源、可编辑的地图服务。

DEM数据,数字高程模型（Digital Elevation Model)，简称DEM

POI数据,POI是“Point of Interest”的缩写，可以翻译成“兴趣点”，也有些叫做“Point of Information”，即“信息点”。电子地图上一般用气泡图标来表示POI，像电子地图上的景点、政府机构、公司、商场、饭馆等，都是POI。

### 工具
- [坐标拾取器](https://lbs.amap.com/tools/picker)
- [街道数据](https://www.openstreetmap.org/)
- [地理空间数据云](http://www.gscloud.cn/)
- [POI数据获取](http://guihuayun.com/poi/)
- [百度经纬度定位](https://lbsyun.baidu.com/jsdemo.htm#yLngLatLocation)

### 关于坐标
高德地图采用国家测绘地理信息局GCJ02坐标系（即俗称火星坐标系），百度采用自己的BD09坐标系，而国际来源地图大多采用WGS84坐标系，导致了多个来源的数据不能叠加在同一底图上，因此，需要在坐标之间相互转换

### GCJ02坐标系
国家测绘地理信息局为了保密需要，按照特殊的算法将坐标进行非线性加密，加密后的坐标为GCJ02坐标系，又称为火星坐标系统。
国内正式发布的电子地图大多数采用GCJ02坐标系，如高德地图、腾讯地图、谷歌地图中国区域等。

### 百度坐标系BD09
百度坐标系是在GCJ02坐标系的基础上进行二次加密而来，目前主要由百度地图使用。

### WGS84坐标系（即EPSG:4326)
一般从国际标准的GPS设备获取的坐标都是WGS84坐标，是国际地图提供商广泛使用的坐标系，如OpenStreetMap、ARCGIS 在线地图、必应地图等。



默认单位是米

> 另外还有 EPSG:3857(基于墨卡托坐标系)

### 坐标转换
不同坐标系的电子地图数据在叠加时会出现位置偏差，导致无法使用，需要进行坐标转换以消除偏差。有多种方法可以实现坐标之间的转换，例如直接编写算法实现；使用Web API实现或者使用现有的插件。

### 距离计算
经纬度属于球面坐标，而我们常规的距离是在平面维度上的，因此，在进行距离计算之前，首先需将球面坐标转换为平面坐标，这样之后才能进行平面距离的测算，计算出来的距离单位就是米了
## 位置
火锅店，烤肉、麻辣烫与奶茶店
医院与煲汤店