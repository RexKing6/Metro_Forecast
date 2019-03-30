# Metro_Forecast
这个星期抽空试了下[全球城市计算AI挑战赛](https://tianchi.aliyun.com/competition/entrance/231708/introduction)，成绩不能看。试的方法作下记录：

1. 普通特征：线性回归
2. 时序特征：LSTM
3. 规则法
4. 时空图网络模型（没试，但觉得可行）



## 赛题

> 大赛以“地铁乘客流量预测”为赛题，参赛者可通过分析地铁站的历史刷卡数据，预测站点未来的客流量变化，帮助实现更合理的出行路线选择，规避交通堵塞，提前部署站点安保措施等，最终实现用大数据和人工智能等技术助力未来城市安全出行。
>
> 大赛开放了20190101至20190125共25天地铁刷卡数据记录，共涉及3条线路81个地铁站约7000万条数据作为训练数据（Metro_train.zip），供选手搭建地铁站点乘客流量预测模型。训练数据（Metro_train.zip）解压后可以得到25个csv文件，每天的刷卡数据均单独存在一个csv文件中，以record为前缀。如2019年1月1日的所有线路所有站点的刷卡数据记录存储在record_2019-01-01.csv文件中，以此类推。同时大赛提供了路网地图，即各地铁站之间的连接关系表，存储在文件Metro_roadMap.csv文件中供选手使用。
>
> 测试阶段，大赛将提供某天所有线路所有站点的刷卡数据记录，选手需预测未来一天00时至24时以10分钟为单位各时段各站点的进站和出站人次。
>
> 预选赛阶段，测试集A集上，大赛将提供2019年1月28日的刷卡数据（testA_record_2019-01-28.csv），选手需对2019年1月29日全天各地铁站以10分钟为单位的人流量进行预测，淘汰赛和决赛将分别更新一批新的数据测试集B集和测试集C集。



## 数据集

https://tianchi.aliyun.com/competition/entrance/231708/information



## Requirements

* python==3.6.5
* numpy==1.16.2
* Pillow==5.4.1
* matplotlib==3.0.2
* scikit-learn==0.20.3
* torch==0.4.1
* torchvision==0.2.1



## 记录

* `testA_submit_2019-01-29_直接28.csv`：14.3743，直接聚合28日数据；
* `testA_submit_2019-01-29_平均.csv`：16.2706，将之前周二的数据加上28日数据取平均；
* `testA_submit_2019-01-29_线性回归+四舍五入.csv`：67.4638，直接当成普通特征，用浅层回归模型；
* `testA_submit_2019-01-29_LSTM_only weekday.csv`：65.3445，将工作日数据当成时序特征，用LSTM预测；
* `testA_submit_2019-01-29_规则.csv`：51.7500，2到25日的数据用规则法，中位数:平均数=4:6。



## 用法

1. 下载[官网数据](https://tianchi.aliyun.com/competition/entrance/231708/information)；
2. `Metro_day/view.ipynb`观察每天数据之间的规律；
3. `Metro_station/make_dataset.ipynb`提取特征，制作数据集；
4. 使用`1.General Feature`、`2.Time Series`、`3.Rules`中的`.ipynb`分割训练数据集与测试数据集，训练模型，之后预测；
5. `Metro_submit/compare.ipynb`分析比较各个提交结果。