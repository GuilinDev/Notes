## 1. Dependencies
```txt
setuptools==65.5.0
wheel<0.40.0

gym==0.21.0
gym-super-mario-bros==7.3.0

tensorboard
six
protobuf==3.20.3
icecream
imageio
opencv-python
nes_py==8.2.1
numpy==1.24.4


shimmy>=2.0
stable_baselines3==1.6.0
```
> Important: other versions may not work!

## 2. Training Model
```python
import os
import uuid

from nes_py.wrappers import JoypadSpace
import gym_super_mario_bros
from gym_super_mario_bros.actions import COMPLEX_MOVEMENT,SIMPLE_MOVEMENT
from stable_baselines3 import PPO
from gym.wrappers import GrayScaleObservation, ResizeObservation
from stable_baselines3.common.vec_env import DummyVecEnv,SubprocVecEnv
from stable_baselines3.common.vec_env import VecFrameStack
from stable_baselines3.common.monitor import Monitor
from util_class import SaveOnBestTrainingRewardCallback, SkipFrame



def make_env():
    env = gym_super_mario_bros.make('SuperMarioBros-v0')
    env = JoypadSpace(env, SIMPLE_MOVEMENT)
    env = SkipFrame(env, 4)
    env = GrayScaleObservation(env, keep_dim=True)
    env = ResizeObservation(env, shape=(84, 84))
    monitor_dir = r'./monitor_log/'
    env = Monitor(env, filename=os.path.join(monitor_dir, str(uuid.uuid4())))
    return env

def train_fn():
    total_timesteps = 40e6
    check_frq=100000
    num_envs = 1
    model_params = {
        'learning_rate': 3e-4,  # learning rate
        'n_steps': 2048,  # The number of steps per environment per update
        'batch_size': 8192,  # data to randomly extract
        'ent_coef': 0.1,  # Entropy term coefficient, affecting explorability

        'gamma': 0.95,  # Short-sighted or long-term
        'clip_range': 0.1,  # Cutoff range
        'gae_lambda':0.95,  # GAE parameter
        "target_kl": 0.03,  # Set KL divergence early stopping threshold
        'n_epochs': 10,  # Update times
        "vf_coef": 0.5,  # Increase the value function weight
        "max_grad_norm": 0.8,  # gradient crop
        'device': 'cuda',

        # log
        'tensorboard_log':r'./tensorboard_log/',
        'verbose':1,
        'policy':"CnnPolicy"
    }

    # LOG
    monitor_dir = r'./monitor_log/'
    os.makedirs(monitor_dir, exist_ok=True)
    callback = SaveOnBestTrainingRewardCallback( check_frq,monitor_dir)

    env = SubprocVecEnv([make_env for _ in range(num_envs)])
    env = VecFrameStack(env, 4, channels_order='last')  # frame overlay
    # Train the model
    # model=PPO.load('monitor_log/best_model/best_model.zip', env=env, **model_params)
    model = PPO(env= env, **model_params)
    model.learn(total_timesteps=total_timesteps,callback=callback)



if __name__ == '__main__':
    train_fn()

```

## 3. Run the model
```python
import os
from gym.wrappers import GrayScaleObservation, ResizeObservation
from icecream import ic
from stable_baselines3.common.vec_env import DummyVecEnv, SubprocVecEnv
from stable_baselines3.common.vec_env import VecFrameStack
from stable_baselines3 import PPO
import gym_super_mario_bros
from gym_super_mario_bros.actions import SIMPLE_MOVEMENT,COMPLEX_MOVEMENT
from nes_py.wrappers import JoypadSpace
import imageio
from util_class import SkipFrame,RewardWrapper
from train_model import make_env

def main():
    # path
    model_dir= r'monitor_log/best_model/best_model12413593.zip' # change to your model path
    # Init env
    env = SubprocVecEnv([make_env for _ in range(1)])
    env = VecFrameStack(env, 4, channels_order='last')  # frame overlay
    model = PPO.load(model_dir, env=env)
    # Start playing
    obs = env.reset()
    ep_len = 10000
    for i in range(ep_len):
        obs = obs.copy()  # Copy array to avoid negative stride problem
        action, _ = model.predict(obs)
        obs, reward, done, info = env.step(action)
        print('reward:',reward)
        env.render('human')  # Show game screen
        # print reward
        # print('reward_sum:', reward_sum)
        if done:
            obs = env.reset()


if __name__ == '__main__':
    main()

```


## Monitor the training progress

![image](https://github.com/user-attachments/assets/ae7d5958-ae02-469a-9b91-5ed40a954726)

![image](https://github.com/user-attachments/assets/c8e88a93-9ab3-4bd3-94ea-1d29e8d28a2c)


