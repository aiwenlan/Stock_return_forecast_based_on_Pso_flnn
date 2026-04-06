# Stock return forecast with PSO–FLNN

**English:** This repository predicts **weekly stock returns** using a **Functional Link Neural Network (FLNN)** trained by **Particle Swarm Optimization (PSO)**. Predicted returns can replace historical returns when computing statistics (mean return vector, variance, skewness, etc.), providing a data basis for prediction-based multi-objective portfolio models in related research.

**中文：** 利用**粒子群优化（PSO）**训练**函数链神经网络（FLNN）**预测股票**周收益**。用预测收益替代历史收益，可计算收益均值向量、方差、偏度等统计量，为构建基于预测的多目标（如三目标）模型提供数据基础。

## Repository layout

| Path | Role |
|------|------|
| `model.py` | FLNN training loop, scaling, Chebyshev (etc.) expansion, evaluation |
| `pso.py` / `particle.py` | PSO population and particle fitness / updates |
| `expand_data.py` | Feature expansion (Chebyshev, power series, Laguerre, Legendre) |
| `train_and_test.py` | Batch read per-stock CSV features and write predicted returns |
| `data/` | Sample data and folders for 100-stock feature / prediction sets |

## Dependencies

- Python 3.x  
- `numpy`, `pandas`, `scikit-learn`, `matplotlib`

Install example:

```bash
pip install numpy pandas scikit-learn matplotlib
```

## How to run

1. Prepare CSV files with the same column layout as the samples under `data/100只股票三维特征数据集合/` (drop `Unnamed: 0` and `周数` in code as in `train_and_test.py`).
2. Open `train_and_test.py` and **replace the hardcoded paths** (`file_dir`, `csv_file`, output `to_csv` path) with paths on your machine, or change them to paths **relative to this project** (e.g. under `data/...`).
3. Adjust `stock` to the symbols you want (default in repo is a single test ticker `600345.SH.csv`).
4. Run:

```bash
python train_and_test.py
```

Training window is controlled in `train_and_test.py` via `train_idx` and `test_idx` (e.g. 140 train / 52 test weeks as in the script). Hyperparameters such as population size and PSO coefficients are set in `Model` inside `model.py`.

## Note

`model.py` saves optional plots/results under `data\预测模型下载数据\` when those code paths are enabled; ensure that directory exists or adjust paths if you use the plotting / CSV export helpers.
