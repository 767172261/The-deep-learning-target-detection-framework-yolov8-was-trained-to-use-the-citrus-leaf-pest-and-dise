柑橘叶片病虫害数据集。YOLO标注格式（TXT格式）
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2383bf6556c8433c962580f25bc84460.png)

数据集包含txt标注文件和图片文件，已经划分好训练集、验证集与测试集，其中训练集708张图片、验证集33张图片、测试集26张图片。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/677e8ffc0a7644c9ab46e56e13997f37.png)

类别描述文件data.yaml ，

数据集柑橘病虫害分为三类：柑橘炭疽病、柑橘叶片砂皮病、脂点黄斑病。![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a3c1a4242af74f96aa0673be3483cfcc.png)


基于柑橘叶片病虫害数据集使用YOLOv8进行目标检测任务。以下是详细的步骤，包括数据准备、模型训练和评估。

## 以下文章内容及代码仅供参考：

### 环境准备

确保您已经安装了以下软件和库：
- Python 3.8 或更高版本
- PyTorch 1.9 或更高版本
- torchvision 0.10 或更高版本
- OpenCV
- numpy
- pandas
- matplotlib
- scikit-image
- albumentations（用于数据增强）

您可以使用以下命令安装所需的Python库：

```bash
pip install torch torchvision opencv-python numpy pandas matplotlib scikit-image albumentations ultralytics
```

### 数据集准备

假设您的数据集已经按照标准格式组织好，并且包含训练集、验证集和测试集。以下是数据集的预期结构：

```
datasets/
└── citrus_leaf_disease_detection/
    ├── images/
    │   ├── train/
    │   ├── val/
    │   └── test/
    ├── labels/
    │   ├── train/
    │   ├── val/
    │   └── test/
    └── data.yaml
```

#### 类别描述文件 (`data.yaml`)

根据提供的信息，整理出以下类别描述文件：

```yaml
[<title="YOLOv8 Data Configuration File">]
train: ../datasets/citrus_leaf_disease_detection/images/train/
val: ../datasets/citrus_leaf_disease_detection/images/val/

nc: 3  # number of classes
names: ['Citrus Anthracnose', 'Citrus Scab', 'Citrus Spot']  # list of class names
```

### 训练代码

我们将使用YOLOv8进行训练。首先，克隆YOLOv8仓库并设置环境。

```bash
git clone https://github.com/ultralytics/ultralytics.git
cd ultralytics
pip install -r requirements.txt
```

#### 准备配置文件

我们已经在上一步中创建了 `data.yaml` 文件。

#### 训练模型

使用以下命令开始训练：

```bash
yolo task=detect mode=train model=yolov8n.pt data=../datasets/citrus_leaf_disease_detection/data.yaml epochs=100 imgsz=640 batch=16
```

### 结果评估

训练完成后，可以使用以下命令评估模型性能：

```bash
yolo task=detect mode=val model=runs/detect/train/weights/best.pt data=../datasets/citrus_leaf_disease_detection/data.yaml
```
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/1b1e1ccbb05b49dc9ff9e0d02dba0105.png)

### 使用说明

1. **配置路径**：
   - 确保 `datasets/citrus_leaf_disease_detection/` 目录结构正确。
   - 确保 `data.yaml` 中的路径和类别名称正确。

2. **运行脚本**：
   - 在终端中依次运行训练脚本和评估脚本。

3. **注意事项**：
   - 根据需要调整超参数和训练设置。
   - 可以通过修改 `model` 参数来选择不同的YOLOv8模型架构（如 `yolov8s.pt`, `yolov8m.pt`, `yolov8l.pt`, `yolov8x.pt`）。

### 示例

假设您的数据集文件夹结构如下：
```
datasets/
└── citrus_leaf_disease_detection/
    ├── images/
    │   ├── train/
    │   ├── val/
    │   └── test/
    ├── labels/
    │   ├── train/
    │   ├── val/
    │   └── test/
    └── data.yaml
```

并且 `all/` 目录包含所有的图片和对应的TXT标注文件。运行上述脚本后，您可以查看训练日志和最终的模型权重文件。

### 总结

通过上述步骤，我们可以构建一个全面的柑橘叶片病虫害检测系统，包括数据集准备、模型训练和结果评估。以下是所有相关的代码文件：

1. **YOLOv8数据集配置文件** (`data.yaml`)
2. **训练命令**

希望这些信息对你有所帮助！如果您有任何问题或需要进一步的帮助，请告诉我。

### 完整代码总结

以下是完整的配置文件和训练命令：

#### YOLOv8数据集配置文件 (`data.yaml`)

```yaml
[<title="YOLOv8 Data Configuration File">]
train: ../datasets/citrus_leaf_disease_detection/images/train/
val: ../datasets/citrus_leaf_disease_detection/images/val/

nc: 3  # number of classes
names: ['Citrus Anthracnose', 'Citrus Scab', 'Citrus Spot']  # list of class names
```

#### 训练命令

```bash
yolo task=detect mode=train model=yolov8n.pt data=../datasets/citrus_leaf_disease_detection/data.yaml epochs=100 imgsz=640 batch=16
```

#### 评估命令

```bash
yolo task=detect mode=val model=runs/detect/train/weights/best.pt data=../datasets/citrus_leaf_disease_detection/data.yaml
```

同学：希望这些信息能帮助您顺利进行模型训练和评估。
