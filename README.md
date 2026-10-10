# Robotic Brick Placement with Reinforcement Learning

A reinforcement-learning project focused on robotic brick placement in simulation (PyBullet + PPO). The objective is to train a policy that can reliably place a brick at a target pose while balancing speed and stability.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Chinnunoor/robotic-brick-placement-rl/blob/main/notebooks/robotic_brick_placement_rl_colab.ipynb)

> ✅ Existing implementation is intentionally preserved. This update focuses on documentation and workflow clarity.

---

## 1) Project Goals

- Train a policy for precise robotic brick placement.
- Evaluate placement accuracy, success rate, and training stability.
- Provide reproducible local and Colab workflows.

---

## 2) Repository Layout

```text
.
├── README.md
└── notebooks/
    └── robotic_brick_placement_rl_colab.ipynb
```

Use the notebook as the primary guided workflow for setup, training, and evaluation.

---

## 3) Environment Setup (Local)

> Use Python 3.10+.

```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install numpy matplotlib gymnasium pybullet stable-baselines3 torch
```

If your current implementation includes a requirements file, prefer:

```bash
pip install -r requirements.txt
```

---

## 4) Training Workflow

The expected training flow is:

1. Initialize the PyBullet environment for brick placement.
2. Define PPO policy/configuration.
3. Train for a fixed timestep budget.
4. Save checkpoints and final model.

Typical command shape (adapt to your implementation entrypoint):

```bash
python train.py \
  --algo ppo \
  --total-timesteps 1000000 \
  --save-dir runs/ppo-brick-placement
```

---

## 5) Evaluation Workflow

Evaluate with deterministic policy rollouts and log:

- **Success Rate (%)**: Fraction of episodes where brick is placed within tolerance.
- **Position Error (m)**: Euclidean distance from target position.
- **Orientation Error (deg/rad)**: Angular mismatch at final placement.
- **Episode Length**: Mean steps to complete or fail.
- **Reward Statistics**: Mean/std episodic return.

Suggested command shape:

```bash
python evaluate.py \
  --model-path runs/ppo-brick-placement/best_model.zip \
  --episodes 100
```

---

## 6) Current Limitations

- Simulation-only validation (no sim-to-real transfer guarantees).
- Action/reward shaping may overfit to a single target placement pattern.
- No explicit dynamic obstacle handling.
- Observation stack may rely on low-dimensional states rather than vision.

---

## 7) Future Improvements

Planned extensions for stronger robotics realism and generalization:

1. **Learned grasping** before placement (grasp + place pipeline).
2. **Camera-based observations** (RGB/RGB-D) with representation learning.
3. **Obstacle-aware placement** and collision-robust planning.
4. **Multi-target placement** with randomized goals per episode.
5. Domain randomization and sim-to-real transfer experiments.

---

## 8) Colab Quick Start

Open the notebook:

- `notebooks/robotic_brick_placement_rl_colab.ipynb`

It is structured as:

1. Runtime and dependency setup
2. Environment sanity checks
3. Training configuration
4. Training execution
5. Evaluation and visualization

---

## 9) Reproducibility Notes

For repeatable results:

- Set deterministic seeds (`numpy`, `torch`, environment).
- Log training configs and environment versions.
- Save best and final checkpoints for comparison.
