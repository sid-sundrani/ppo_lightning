# Promixal Policy Optimization with PyTorch  
This repository implements [promixal policy optimization](https://arxiv.org/abs/1707.06347) using the PyTorch Lightning package. PyTorch Lightning helps reduce boilerplate code and modularize model training. Hence, different parts such as the loss function, advantage calculation, or training configurations can be easily modified as per users' experiments. 

This implementation is inspired by OpenAI baselines for [PPO](https://github.com/openai/baselines/tree/master/baselines/ppo2) and implementation 
of other RL algorithms in [PyTorch Lightning Bolts](https://github.com/PyTorchLightning/pytorch-lightning-bolts/)

## Details 
This PPO implemenation works with both discrete and continous action-space environments via OpenAI Gym. Implements PPO Actor-Critic Style. Continous actor uses normal distribution to predict actions wheres discrete actor uses multinomial distribution (Categorical distribution in Torch) to predict actions. 

GPU training is supported. It can be enabled normally through PyTorch Lightning itself: `trainer = Trainer(gpus=-1)`. Note: If default MLP actor and critic networks are being used, GPU training is likely to be slower than CPU because of the overhead of pushing each sample to device during trajectory collection. If the user is using deep networks for actor or critic, then GPU speedups can be realized.  

## Requirements 
* Python3 >= 3.6 
* OpenAI Gym 
* PyTorch
* PyTorch Lightning 

## Results 
Results with default parameters on categorical and continous action spaces. PyBullet's envirnoment was used instead of MuJoCo for Hopper and Walker. 

Parameters: 
`batch_size = 512`, `nb_optim_iters = 4`,`clip_ratio = 2`, `gamma = 0.99`, 
`lam = 0.95`, `lr_actor = 3e-4`, `lr_critic = 1e-3`

| CartPole-v0    | HopperBulletEnv-v0 | Walker2DBulletEnv-v0 |
| -------------- | -------------- | -------------- |  
| ![](results/CartPole-v0.JPG) | ![](results/HopperBulletEnv-v0.JPG) | ![](results/Walker2DBulletEnv-v0.JPG) |
