# FILTER: Fast Inverse Reinforcement Learning (Modified)

This repository is an **extended and modified** version of the original **[FILTER (Fast Inverse Reinforcement Learning)](https://github.com/gkswamy98/fast_irl)**.

### **🔹 Key Improvements**
- **Extended to support a broader range of RL environments**, including **Gym, MuJoCo, and Atari**.
- **Integrated KL divergence and reward-based evaluation** for improved benchmarking.
- **Refactored and optimized the codebase** to enhance stability and adaptability.

This project builds upon the original **FILTER** algorithm from [FILTER: Fast Inverse Reinforcement Learning](https://gokul.dev/filter/), making it applicable to a broader range of reinforcement learning tasks.

---

## Running Experiments
To train an expert, run:
```bash
python experts/train.py -e env_name
```

To train a learner, run:
```bash
python learners/train.py -a algo_name -e env_name -s seed
```

This package supports training via:
- Behavioral Cloning (bc)
- Moment Matching (mm)
- FILTER(NR) (filter-nr)
- FILTER(BR) (filter-br)

on the following environments:
- HalfCheetahBulletEnv-v0 (halfcheetah)
- HopperBulletEnv-v0 (hopper)
- WalkerBulletEnv-v0 (walker)
- antmaze-large-play-v2 (antmaze).

For the first three environments, we use Soft-Actor Critic as our baseline policy optimizer. For antmaze, we use T3D+BC. See learners/gym_wrappers.py for wrappers to speed up learning for your own inverse reinforcement learning algorithms.
