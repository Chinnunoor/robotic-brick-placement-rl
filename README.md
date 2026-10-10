# Robotic Brick Placement with Reinforcement Learning

A reinforcement-learning project for teaching a simulated Panda robotic arm to place bricks accurately in PyBullet. The controller uses PPO with a Gymnasium environment and reports measured placement success and error instead of assuming a result.

## What this project demonstrates

- Cartesian arm control with inverse kinematics.
- PPO training with Stable-Baselines3.
- Randomized target positions and held-out evaluation episodes.
- Placement success, position error, and uprightness checks.
- A three-brick showcase video with scripted pickup/retreat presentation motion and learned travel/alignment.

This is a simulation proof of concept. Grasping and release are simplified: the brick begins attached to the gripper and is released automatically near the target. It is not a real-world deployment or a claim of sim-to-real performance.

## Quick start with Google Colab

Open the notebook:

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Chinnunoor/robotic-brick-placement-rl/blob/main/brick_placement_rl_colab.ipynb)

1. Choose a compatible Python runtime in **Runtime → Change runtime type**. The 2025.07 runtime is recommended if the latest runtime tries to compile PyBullet from source.
2. Connect the CPU runtime; a GPU is not required.
3. Run the notebook from top to bottom. It installs PyBullet, Gymnasium, Stable-Baselines3, ImageIO, and plotting/video dependencies.
4. Run the sanity check, train PPO, evaluate on new target positions, and record the showcase.

The final showcase produces <code>brick_placement_showcase_32s.mp4</code> and reports an outcome for each of three target locations. Colab runtimes are temporary, so download the trained policy and video before disconnecting.

## Local setup

Use Python 3.10 or newer:

~~~bash
python -m venv .venv
source .venv/bin/activate  # macOS/Linux
python -m pip install --upgrade pip
python -m pip install numpy matplotlib gymnasium pybullet stable-baselines3 imageio imageio-ffmpeg
~~~

## Workflow

1. Create the PyBullet environment and run the Gymnasium API check.
2. Train PPO in two phases, beginning with smaller offsets and then widening the target-start distribution.
3. Evaluate deterministic rollouts on held-out target positions.
4. Record the three-brick showcase and inspect the measured results.

Success means the settled brick is within the environment's placement tolerance and remains upright. Training time and success rate depend on runtime capacity and random seed.

## Current limitations and next steps

- Simulation-only validation; no sim-to-real guarantee.
- Simplified grasping and automatic release.
- Low-dimensional state observations rather than camera input.
- No dynamic obstacle handling.

Natural extensions include learned grasping, RGB/RGB-D observations, obstacle-aware planning, randomized physics, and multi-target or cluttered-scene placement.

## Repository layout

~~~text
README.md
brick_placement_rl_colab.ipynb
~~~

## License

Add the project's intended license before redistributing the code or trained models.

## Citation and references

- [Gymnasium custom environments](https://gymnasium.farama.org/tutorials/gymnasium_basics/environment_creation/)
- [PyBullet](https://pybullet.org/wordpress/)
- [Stable-Baselines3 custom environments](https://stable-baselines3.readthedocs.io/en/master/guide/custom_env.html)
