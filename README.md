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

---

### **Setup Instructions**
```bash
conda create -n fast_irl python=3.9
pip install stable-baselines3==0.8.0 pybullet==3.2.1 tqdm ipykernel==6.4.1 matplotlib==3.4.3 rliable "cython<3"
```

---

## **Debugging Process & Solutions**  

### **1️⃣ NumPy and Pandas Version Conflict**
#### **Issue**  
- `pandas` requires `NumPy >= 1.22.4`, but `stable-baselines3` depends on an older NumPy version.  
- Running `python learners/train.py` resulted in:  
  ```plaintext
  ImportError: this version of pandas is incompatible with numpy < 1.22.4
  ```

#### **Solution**  
- **Downgraded Pandas to a compatible version with NumPy 1.19.5**  
  ```bash
  pip uninstall -y pandas
  pip install --no-cache-dir "pandas==1.3.5"
  ```
- **Verified compatibility**  
  ```bash
  python -c "import pandas as pd, numpy as np; print(f'Pandas: {pd.__version__}, NumPy: {np.__version__}')"
  ```
  - Expected output:  
    ```
    Pandas: 1.3.5, NumPy: 1.19.5
    ```

---

### **3️⃣ `pybullet_envs` Requires `gym 0.21.0`**
#### **Issue**  
- Running `train.py` with `pybullet_envs` resulted in:  
  ```plaintext
  AttributeError: 'dict' object has no attribute 'env_specs'
  ```
- This happens because `pybullet_envs` expects an **older version of `gym`**.

#### **Solution**  
- **Downgraded `gym` to `0.21.0` to maintain compatibility**  
  ```bash
  pip install --force-reinstall "gym==0.21.0"
  ```
- **Verified that `Walker2DBulletEnv-v0` loads correctly**  
  ```python
  import gym
  env = gym.make("Walker2DBulletEnv-v0")
  obs = env.reset()
  print("Environment initialized successfully")
  ```

---

### **✅ Final Steps for Successful Execution**
After applying the above fixes, `train.py` ran successfully with:
```bash
python learners/train.py -a filter-br -e walker -s 10
```
