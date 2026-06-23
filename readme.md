这是去除了所有 Emoji 表情符号的纯净版本，格式严谨，您可以直接点击代码块右上角的“复制”按钮将其保存为 `README.md` 文件：

```markdown   ”“减价
# Root Cause Analysis in Complex Industrial Process Monitoring via Virtual Scale Factor and Data Source基于虚拟尺度因子和数据源的复杂工业过程监控的根本原因分析

<div align="center">   <div align="center"><div align="center">   <div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)[![条款:](https://img.shields.io/badge/License-MIT-blue.svg)] (https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)[![Python 3.8](https://img.shields.io/badge/python-3.8 -blue.svg)]（https://www.python.org/downloads/）
[![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&logo=PyTorch&logoColor=white)](https://pytorch.org/)[! [PyTorch] (https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&标志= PyTorch& logoColor = white)] (https://pytorch.org/)
[![Paper Status](https://img.shields.io/badge/Paper-Under_Review-orange.svg)]()[!(纸状态)(https://img.shields.io/badge/Paper-Under_Review-orange.svg)) ()

**基于虚拟尺度因子与数据源的复杂工业过程监控根因分析** *(Official PyTorch Implementation)*

</div>   < / div>

---

## 项目简介

可靠的故障检测与根因分析（Root Cause Analysis, RCA）对于保障复杂工业系统的安全稳定运行至关重要。然而，现代工业数据往往具有高维、强非线性和多变量耦合等特征，使得传统的归因方法面临梯度饱和、噪声敏感以及物理可解释性弱等挑战。

本项目为论文 **"Root Cause Analysis in complex industrial process monitoring via virtual scale factor and data source"**（目前在投于 *Journal of Process Control*）的官方代码实现。我们提出了一种新型的**虚拟尺度因子（VSF）归因框架**，并结合融合了重构误差与 $T^2$ 统计量的**增强型自编码器（Enhanced AE）**，为工业异常检测与故障诊断提供了一套完整、鲁棒且具有极强物理可解释性的解决方案。本项目为论文 **"Root Cause Analysis in complex industrial process monitoring via virtual scale factor and data source"**（目前在投于 *Journal of Process Control*）的官方代码实现。我们提出了一种新型的**虚拟尺度因子（VSF）归因框架**，并结合融合了重构误差与 $T^2$ 统计量的**增强型自编码器（Enhanced AE）**，为工业异常检测与故障诊断提供了一套完整、鲁棒且具有极强物理可解释性的解决方案。

### 核心优势
- **更精准的分布捕捉**：相比于传统的梯度（Gradient）或基于 Shapley 值的归因方法，我们的 VSF 方法能够更准确地捕捉非线性多模态数据中的分布结构，有效避免“模态混淆”。
- **动态故障验证（FER）**：引入“故障消除率”（Fault Elimination Rate）指标，不仅提供静态的变量重要性排序，更能动态验证模型解释与检测机制之间的一致性。
- **物理可解释性**：基于梯度势场与状态演化方程，结合数据源（Data Source）模型，直接量化变量偏离正常工况的方向与程度。

---

## 目录结构

本项目代码结构清晰，包含了核心算法模块以及用于复现论文二维及多维（TEP）实验结果的完整工作流：

```text   ' ' '文本
├── attribution.py       # 核心归因算法库：包含 VSF、Gradient、IG、SHAP、DeepLIFT 的底层实现及标准化输出
├── indicators.py        # 异常检测模型库：包含 PCA、SVDD、Enhanced AE 的模型构建与超参数配置 (ExpConfig)
├── 2d_yuan.ipynb        # 2D 合成数据实验：单峰高斯分布下的特征归因图表复现
├── 2d_feng.ipynb        # 2D 合成数据实验：双峰混合高斯分布 (GMM) 下的特征归因图表复现
├── duo_tep.ipynb        # TEP 多维工业实验 (一)：故障数据加载、模型评估与特征重要性排序
├── duo_wei.ipynb        # TEP 多维工业实验 (二)：故障消除率 (FER) 曲线绘制及变量替换机制验证
├── image_d40ba3.png     # TEP 基准测试流程与架构示意图
├── requirements.txt     # 项目依赖清单
└── README.md            # 项目说明文档

```

---

## 环境依赖与安装

本项目推荐使用 **Python 3.8 或更高版本**。请在您的虚拟环境（如 Conda 或 venv）中执行以下命令以安装所需依赖：

```bash   ”“bash   “bash”;“bash
# 1. 克隆本仓库到本地
git clone [https://github.com/YourUsername/YourRepoName.git](https://github.com/YourUsername/YourRepoName.git)git clone [https://github.com/YourUsername/YourRepoName.git](https://github.com/YourUsername/YourRepoName.git]git clone [https://github.com/YourUsername/YourRepoName.git](https://github.com/YourUsername/YourRepoName.git)git clone [https://github.com/YourUsername/YourRepoName.git](https://github.com/YourUsername/YourRepoName.git] .
cd YourRepoName

# 2. 安装核心计算与深度学习依赖
pip install torch numpy pandas scikit-learn scipyPIP安装火炬numpy熊猫scikit-学习scipy

# 3. 安装可视化与可解释性辅助库
pip install matplotlib tqdm captum shap jupyter

```

> **注**：本项目使用 `Captum` 库辅助实现 DeepLIFT 等深度学习基线方法，使用 `SHAP` 库实现 Shapley 值的近似计算。

---

## 快速开始与图表复现

我们提供了开箱即用的 Jupyter Notebook 脚本，您可以直接运行这些脚本以一键复现论文中的核心实验结果与精美图表：

### 1. 2D 合成数据验证实验 (图 1 & 图 2)

本部分直观地验证了 VSF 方法在不同数据分布下定位故障源的稳定性。

* 打开并运行 `2d_yuan.ipynb`：复现单峰分布下的归因热力图。
* 打开并运行 `2d_feng.ipynb`：复现双峰高斯混合分布（GMM）下的归因热力图，验证 VSF 在复杂分布下避免模态混淆的优越能力。

### 2. TEP 多维工业数据集实验 (图 3、图 4 & 表 1)

本部分在经典的田纳西伊斯曼过程（Tennessee Eastman Process, TEP）基准上系统评估了各归因方法的故障隔离能力。

* 打开并运行 `duo_tep.ipynb`：生成各归因方法在 $T^2$、SVDD 和 Enhanced AE 模型下的 Top-k 贡献变量排序报告与对比图表。
* 打开并运行 `duo_wei.ipynb`：验证变量替换机制，并绘制随替换变量数量变化的**动态故障消除率 (FER) 曲线**。

*(说明：所有生成的实验图表如需高清矢量图，脚本中已内置 PDF 导出代码，默认将自动保存在项目根目录下。)*

---

## 核心模块深度解析

为了方便同行学者进行二次开发与对比实验，我们将核心逻辑进行了高度封装：

### 1. 增强型自编码器 (Enhanced AE)

**对应文件：** `indicators.py`

突破了传统 AE 仅依赖输入空间重构误差的局限。通过在损失函数和检测阈值中融合重构误差（Reconstruction Error）与潜在空间（Latent Space）的马氏距离（即 $T^2$ 统计量），显著提升了模型对复杂工业系统中微小漂移故障的检测敏感度与整体鲁棒性。

### 2. 虚拟尺度因子归因 (VSF)

**对应文件：** `attribution.py` 中的 `VSFAttribution` 类

区别于仅关注局部梯度的传统方法，VSF 方法构建了一个虚拟尺度扰动空间。通过求解梯度势场中的状态演化方程，定位系统稳定点（即“数据源 Data Source”）。最终的变量贡献度由**局部模型敏感度**与**稳态偏差**共同决定，使得归因结果兼具高精度与明确的物理意义。



---

## 许可证

本项目遵循 [MIT License](https://opensource.org/licenses/MIT) 开源协议。欢迎广大学者和开发者克隆、修改及用于学术交流！

```

```
