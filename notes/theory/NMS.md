## Non Maximum Suppression

### 1. IoU
![](../../figs/Theory/NMS/IoU.png)

AB重叠的面积占AB并集面积的比例

计算流程如下:
- 首先计算两个box左上角点坐标的最大值, 和右下角点坐标的最小值
- 计算交集面积
- 最后把交集面积除以对应的并集面积

code:
- [IoU.py]()

### 2. NMS Theory
NMS用于合并最后的候选框

![](../../figs/Theory/NMS/NMS_example.png)

假设在目标检测中定位到了一个车辆，利用算法找到了一堆候选方框，我们需要判别哪些矩形方框是没有意义的

假定存在6个候选框，首先根据 __分类器的分类概率__ 进行排序，假设从小到大属于车辆的概率分别为 A-B-C-D-E-F
- 从最大概率的矩形框F开始, 依次判定A~E与F的重叠度(IoU)是否大于某个设定的阈值
- 假设B和D与F的重叠度超过阈值, 那么就抛弃B和D, 并标记第一个矩形框F

## Reference
- [NMS算法详解(附Pytorch代码实现)](https://zhuanlan.zhihu.com/p/54709759)