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

### 2. NMS
NMS用于合并最后的候选框

![](../../figs/Theory/NMS/NMS_example.png)

假设在目标检测中定位到了一个车辆，利用算法找到了一堆候选方框，我们需要判别哪些矩形方框是没有意义的

假定存在6个候选框，首先根据 __分类器的分类概率__ 进行排序，假设从小到大属于车辆的概率分别为 A-B-C-D-E-F
- 从最大概率的矩形框F开始,先将F添加到输出列表中, 并将其从候选框列表中删除, 依次判定A~E与F的重叠度(IoU)是否大于某个设定的阈值, 如果大于某个阈值的话, 表明这两个候选框很可能检测到同一个类别的物体
- 假设B和D与F的重叠度超过阈值, 那么就在候选框列表中删除B和D
- 从剩下的矩形框A,C,E中，选择概率最大的E, 加入输出列表中, 然后判断E与A和C的IoU, 如果大于一定的阈值, 就从候选框列表中删除, 并标记E为保留下来的第二个矩形框
- 重复上述过程, 直到候选框列表为空, 返回输出列表

Details:
- 输入的是所有的候选框, 候选框包括所框定的位置, 以及框定区域所属的类别, NMS可以帮助去重

Code:
- [NMS.py](https://github.com/rentainhe/mini-detection/blob/master/core/NMS.py)

## Reference
- [NMS算法详解(附Pytorch代码实现)](https://zhuanlan.zhihu.com/p/54709759)
- [非极大值抑制(Non-Maximum Suppression)](https://www.cnblogs.com/makefile/p/nms.html)