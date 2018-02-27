# 侦测走神司机

## 简介

本项目通过Keras搭建一个深度卷积神经网络来对驾驶员开车时的照片进行分类。

- 模型输入：驾驶员的照片
- 模型输出：驾驶员分类打各个状态的概率

我们对以下十种状态进行侦测：

1. 安全驾驶
2. 右手打字
3. 右手打电话
4. 左手打字
5. 左手打电话
6. 调节收音机
7. 喝饮料
8. 那后面东西
9. 整理头发和化妆
10. 和其他乘客说话

我们可以看到，除了第一种状态安全驾驶，其他九种状态都是司机开车时的危险动作。

## 项目评估与报告

我最终训练出来的模型，在测试集上评估的LogLoss为0.28486，在[Kaggle排行榜](https://www.kaggle.com/c/state-farm-distracted-driver-detection/leaderboard)，排名前13%。具体实施方案详见[本项目报告](https://github.com/NaughtyFlame/distracted_driver_detection/blob/master/capstone.pdf)。

## 数据

这个项目训练、测试用的数据是来自于一个Kaggle竞赛State Farm Distracted Driver Detection([数据集现在链接](https://www.kaggle.com/c/state-farm-distracted-driver-detection/data))。

这个竞赛提供数据文件有：

- driver_imgs_list.csv.zip - 一个训练数据集的列表，每列是图片的文件名以及它所对应的状态类别和司机的编号

- img.zip - 一个打包文件夹，里面包含训练集和测试集

- sample_submission.csv - 提交在kaggle上进行评分的文件模板


## 项目代码说明

1. 数据集分析和挖掘

[data_visualisation.ipynb](https://github.com/NaughtyFlame/distracted_driver_detection/blob/master/data_visualisation.ipynb)

2. 模型训练

[distracted_driver_detection.ipynb](https://github.com/NaughtyFlame/distracted_driver_detection/blob/master/distracted_driver_detection.ipynb)

3. 预测结果做均值融合

[submission_merge.ipynb](https://github.com/NaughtyFlame/distracted_driver_detection/blob/master/submission_merge.ipynb)

此外，运行以上代码，文件夹的布局为：
```
|--- dataset
        |--- train (22424 images)
              |--- c0 (2489 images)
              |--- c1 (2267 images)
               .....            
        |--- to_prediction
               |--- test (79726 images)
|--- subm (存放导出的预测submission)
|--- models (训练的模型)
```
需要说明的是使用kares中`flow_from_directory`方法，需要传入一个包含子目录的目录，所以测试集文件放置，安排了两层。
