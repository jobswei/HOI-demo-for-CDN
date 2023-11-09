# HOI-demo-for-CDN
demo scripts for CDN algorithm

关于人物交互(HOI)，相继提出了很多算法。但是算法的code中没有demo文件。这里针对于[CDN算法](https://github.com/YueLiao/CDN.git)写了一下demo的脚本，由于HOI算法代码结构相似，稍加修改后也可以用于其他算法。

* 对于单张图片的预测
* 预测结果的可视化
* 标注格式以及动作/物体种类基于HICO-Det数据集(详见annotation文件夹)

下面详细介绍各脚本的功能

#### [predictor.py](./utils/predictor.py)

基于CDN算法中对于HICODet数据集的eval方法，加以修改得到的对于单张任意图片的predict方法。
`model` 为读入的预训练模型，`correct_mat_path` 是对应于HICODet数据集的匹配矩阵，`source`是输入图片的路径
```python
class Predictor:
    def __init__(self,model,postprocessors,correct_mat_path,args) -> None:
        pass
    def predict(self,source):
        ...
        return preds
```
#### [demo_utils.py](./utils/demo_utils.py)
* `filter_res_score` 基于hoi对的`score`进行过滤，保留`score`大于`thre`的所有pair
* `filter_res_num` 基于数量过滤。按照`score`值从大到小排序，保留前`num`个pair
* `show_hoi` 将`preds`中的数据格式，结合物体/动作的对应编号，转化为自然语言词汇后输出
    * `obj_path` 和 `verb_path` 为编号文件的路径

#### [demo.py](./utils/demo.py)
* 在执行区域设置参数，参数设置和CDN的规则一样。需要注意，有一些参数可能是无用的！
* `main`函数为图片输入，predict得到结果，可视化结果的全过程

如有补充或疑问，欢迎联系 3031864345@qq.com