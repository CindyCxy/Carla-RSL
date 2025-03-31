# Carla-RSL
Simulation datasets created based on CARLA

# CARLA-RSL 数据集

## 数据集简介

`Carla-RSL` 数据集旨在评估路侧激光雷达在不同部署位置中的感知性能。该数据集基于 CARLA 模拟器的 Town03 地图，涵盖了五叉路口和环岛路口两个典型场景，包含 10414 帧数据，涵盖点云数据（PCD 格式）和 3D 标注标签数据。

## 数据集特点

- **多样化场景**：包含五叉路口和环岛路口两种复杂交通场景。
- **丰富的部署位置**：五叉路口场景下有 12 个部署位置，主要用于评估部署位置横向变化对感知性能的影响；环岛路口场景下有 25 个部署位置，主要用于评估部署高度和俯仰角变化对感知性能的影响。
- **高质量标注**：提供精确的 3D 标注标签数据，便于进行目标检测、跟踪和语义分割等任务。
- **大规模数据量**：包含 10414 帧数据，为研究者提供了丰富的实验素材。

## 数据集结构

数据集的文件结构如下：

```
carla-RSL-dataset/
├── README.md
├── data/
│   ├── five_way_intersection/
│   │   ├── 1-1/
│   │   |   ├── pcd/
│   │   │   |   ├──000000.pcd
│   │   |   ├── label/
│   │   │   |   ├──000000.json
│   │   │   ├── 1-1_config.toml
│   │   ├── 1-2/
│   │   |   ├── pcd/
│   │   │   |   ├──000000.pcd
│   │   |   ├── label/
│   │   │   |   ├──000000.json
│   │   │   ├── 1-2_config.toml
│   │   ├── ...
│   ├── roundabout/
│   │   ├── 1-1/
│   │   |   ├── pcd/
│   │   │   |   ├──000000.pcd
│   │   |   ├── label/
│   │   │   |   ├──000000.json
│   │   │   ├── 1-1_config.toml
│   │   ├── 1-2/
│   │   |   ├── pcd/
│   │   │   |   ├──000000.pcd
│   │   |   ├── label/
│   │   │   |   ├──000000.json
│   │   │   ├── 1-2_config.toml
│   │   ├── ...
```

- **`data/`**：包含所有数据文件，按场景和部署位置进行分层组织。
  - **`five_way_intersection/`**：五叉路口场景的数据。
  - **`roundabout/`**：环岛路口场景的数据。

## 数据格式说明

### 点云数据（PCD 格式）

- 每个点云文件（`.pcd`）包含一帧激光雷达扫描的点云数据。
- 数据格式遵循 PCD 文件标准，包含点的三维坐标（X, Y, Z）以及强度。

### 3D 标注标签数据（JSON 格式）

- 每个标注文件（`.json`）与对应的点云文件一一对应。

- 标注文件包含目标的类别、边界框（3D Bounding Box）的中心坐标、边界框尺寸等信息。

- 示例标注格式：

  ```json
  {
          "type": "Car",
          "type_id": "vehicle.lincoln.mkz_2020",
          "occluded_state": 0,
          "truncated_state": 0,
          "track_id": 0,
          "crowding": 0,
          "ignore": 0,
          "alpha": 0,
          "2d_box": {
              "xmin": 487,
              "ymin": 455,
              "xmax": 565,
              "ymax": 522
          },
          "3d_dimensions": {
              "h": 1.490277647972107,
              "w": 1.8367133140563965,
              "l": 4.89238166809082
          },
  
          "3d_location": {
              "x": 12.723139762878418,
              "y": 57.69520950317383,
              "z": -5.508650779724121
          },
          "rotation": 1.567081093788147
      },
  
  ```

## 数据集使用指南

### 数据下载

我们的数据集可向研究人员免费使用。请将以下信息发送至，提供的电子邮件地址（cindychen_73@163.com）。您将在一周内收到下载链接。下载数据后，请将数据放在以下结构中：

```
请求的数据/代码：
组织/公司：
全名:
地址：
电子邮件:
请求原因：
```

### 数据加载

- 使用 Python 和相关库（如 Open3D 或 PCL）加载点云数据：

  ```python
  import open3d as o3d
  
  pcd = o3d.io.read_point_cloud("path/to/000000.pcd")
  o3d.visualization.draw_geometries([pcd])
  ```

- 加载标注数据：

  ```python
  import json
  
  with open("path/to/000000.json", "r") as f:
      labels = json.load(f)
  ```
