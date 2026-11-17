# SO101 数据集与 LeRobot 策略模型

本项目保存 SO101 机械臂的示教数据，以及使用同一数据集训练的 ACT 策略最终模型。

## 数据集

- 路径为 `local/dataset11-16_20261116_144131/`。
- 数据格式为 LeRobot v3.0，机器人类型为 `so_follower`。
- 包含 50 条示教轨迹、23,506 帧和 1 个任务。采样频率为 30 FPS。
- `data/` 保存 Parquet 数据，包含 6 维关节状态和 6 维动作。关节顺序和字段定义见 `meta/info.json`。
- `videos/` 保存 `cam1` 和 `cam2` 的 640 × 480 视频。视频采用 AV1 编码，容器格式为 MP4。
- `meta/` 保存数据集元信息、统计量、任务及轨迹索引。数据集元信息将全部 50 条轨迹标为训练集。

## 策略模型

| 策略 | 批大小 | 最终步数 | `pretrained_model` 路径 |
| --- | ---: | ---: | --- |
| ACT | 8 | 10,000 | `outputs/train/act_batch8_10k/checkpoints/010000/pretrained_model/` |

模型目录包含 `model.safetensors`、策略配置 `config.json`、训练参数 `train_config.json`，以及前处理和后处理配置与参数。加载策略时，使用对应的整个 `pretrained_model` 目录作为本地模型路径。Diffusion Policy 和 SmolVLA 的权重体积较大，保存在本地训练输出目录。

## 获取文件

安装 Git LFS 后，在本地运行以下命令。视频和 Safetensors 文件由 Git LFS 下载。

```bash
git lfs install
git clone https://github.com/PYL-CSU/lerobot-training-results.git
cd lerobot-training-results
git lfs pull
```

检出后，数据集根目录为 `local/dataset11-16_20261116_144131`。可在 [数据集元信息](local/dataset11-16_20261116_144131/meta/info.json) 中核对视频配置、字段和数据规模。
