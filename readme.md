
```markdown
# 基于虚拟尺度因子与数据源的复杂工业过程监控根因分析
**Root Cause Analysis in Complex Industrial Process Monitoring via Virtual Scale Factor and Data Source**

<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&logo=PyTorch&logoColor=white)](https://pytorch.org/)
[![Paper Status](https://img.shields.io/badge/Paper-Under_Review-orange.svg)]()

**Official PyTorch Implementation** *论文目前在投于 Journal of Process Control*

</div>

---

## 📌 项目简介

可靠的故障检测与根因分析（Root Cause Analysis, RCA）对于保障复杂工业系统的安全稳定运行至关重要。然而，现代工业数据往往具有**高维、强非线性**和**多变量耦合**等特征，使得传统的归因方法面临梯度饱和、噪声敏感以及物理可解释性弱等挑战。

本项目是论文 **“Root Cause Analysis in complex industrial process monitoring via virtual scale factor and data source”** 的官方代码实现。我们提出了一种新型的 **虚拟尺度因子（VSF）归因框架**，并结合融合了重构误差与 T² 统计量的 **增强型自编码器（Enhanced AE）**，为工业异常检测与故障诊断提供了一套完整、鲁棒且具有极强物理可解释性的解决方案。

### ✨ 核心优势

* **更精准的分布捕捉**：相比于传统的梯度（Gradient）或基于 Shapley 值的归因方法，VSF 能够更准确地捕捉非线性多模态数据中的分布结构，有效避免“模态混淆”。
* **动态故障验证（FER）**：引入“故障消除率”（Fault Elimination Rate）指标，不仅提供静态的变量重要性排序，更能动态验证模型解释与检测机制之间的一致性。
* **物理可解释性**：基于梯度势场与状态演化方程，结合数据源（Data Source）模型，直接量化变量偏离正常工况的方向与程度。

---

## 📂 目录结构

```text
.
├── attribution.py          # 核心归因算法库：VSF、Gradient、IG、SHAP、DeepLIFT 实现
├── indicators.py           # 异常检测模型库：PCA、SVDD、Enhanced AE 及超参数配置
├── 2d_yuan.ipynb           # 2D 合成数据实验：单峰高斯分布归因图表
├── 2d_feng.ipynb           # 2D 合成数据实验：双峰混合高斯分布 (GMM) 归因图表
├── duo_tep.ipynb           # TEP 多维工业实验（一）：故障数据加载、评估与特征排序
├── duo_wei.ipynb           # TEP 多维工业实验（二）：故障消除率 (FER) 曲线绘制
├── image_d40ba3.png        # TEP 基准测试流程与架构示意图
├── requirements.txt        # 项目依赖清单
└── README.md               # 本文件

```

---

## ⚙️ 环境依赖与安装

本项目推荐使用 **Python 3.8 或更高版本**。建议使用虚拟环境（如 Conda 或 venv）进行隔离以避免依赖冲突。

### 安装步骤

**1. 克隆仓库**

```bash
git clone [https://github.com/YourUsername/YourRepoName.git](https://github.com/YourUsername/YourRepoName.git)
cd YourRepoName

```

**2. 安装核心依赖**

```bash
pip install torch numpy pandas scikit-learn scipy

```

**3. 安装可视化与可解释性辅助库**

```bash
pip install matplotlib tqdm captum shap jupyter

```

> **注**：`captum` 用于 DeepLIFT 等基线方法的实现，`shap` 用于 Shapley 值的近似计算。

---

## 🚀 快速开始与图表复现

我们提供了开箱即用的 Jupyter Notebook 脚本，可一键复现论文中的核心实验结果。所有图表默认以 PDF 格式自动保存在项目根目录下，方便直接用于学术排版。

**1. 2D 合成数据验证实验（图 1 和图 2）**

* **单峰分布**：运行 `2d_yuan.ipynb` 生成归因热力图。
* **双峰混合高斯分布（GMM）**：运行 `2d_feng.ipynb` 验证 VSF 在复杂分布下避免模态混淆的优势。

**2. TEP 多维工业数据集实验（图 3、图 4 和表 1）**

* **归因方法对比**：运行 `duo_tep.ipynb`，生成各方法在 T²、SVDD 和 Enhanced AE 模型下的 Top‑k 贡献变量排序与对比图表。
* **动态故障消除率曲线**：运行 `duo_wei.ipynb`，验证变量替换机制并绘制 FER 曲线。

---

## 🧠 核心模块深度解析

为便于二次开发与对比实验，核心逻辑已高度封装。

**增强型自编码器（Enhanced AE）** — 详见 `indicators.py`
突破传统 AE 仅依赖输入空间重构误差的局限，在损失函数和检测阈值中**融合重构误差与潜在空间马氏距离（T² 统计量）**，显著提升对微小漂移故障的检测敏感度与鲁棒性。

**虚拟尺度因子归因（VSF）** — 详见 `attribution.py` 中的 `VSFAttribution` 类
VSF 构建虚拟尺度扰动空间，通过求解梯度势场中的状态演化方程，定位系统稳定点（即“数据源”）。最终贡献度由**局部模型敏感度**与**稳态偏差**共同决定，兼具高精度与明确的物理意义。

---

## 📄 许可证

本项目采用 [MIT License](https://opensource.org/licenses/MIT) 开源协议，欢迎广大学者和开发者克隆、修改及用于学术交流。

---

> 如有任何问题、讨论或建议，欢迎通过 Issues 或 Pull Requests 与我们联系。

```

```
