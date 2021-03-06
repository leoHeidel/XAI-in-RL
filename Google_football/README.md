# XAI-in-RL: Google Football env

## Packages installation
```
sudo apt-get update && 
sudo apt-get install git cmake build-essential libgl1-mesa-dev libsdl2-dev \
libsdl2-image-dev libsdl2-ttf-dev libsdl2-gfx-dev libboost-all-dev \
libdirectfb-dev libst-dev mesa-utils xvfb x11vnc libsdl-sge-dev python3-pip \
cmake libopenmpi-dev python3-dev zlib1g-dev
```
## Environment installation (Anaconda)
*Note: Install Anaconda first. See [official website](https://docs.anaconda.com/anaconda/install/linux/) for further information.*
```bash
conda env create -f conda_env_football.yml
```

## Google football environment installation
```bash
cd gfootball_env
pip3 install .
```
## Training agents

You can start training new agents by running the `working_multiagent_google.py` script.
Here is an example for a 11 vs 11 match:
```bash
python working_multiagent_google.py --scenario-name "11_vs_11_stochastic" --num-agents 11 --num-policies 11 --num-iters 1000
```
This will create files called "checkpoints" that will be used to store model weights every fifty iterations.
They will be located on `~/ray_results/default/...`.

**By default, this script will resume training from the last checkpoint located in the `models` subdirectory.**
If you don't want this behaviour, just pass the `--no-resume` argument.

## Evaluating an agent

You can evaluate a trained agent by running the `rollout.py` script and passing the path to your model checkpoint file as an argument. Here is an example for a 11 vs 11 match:
```bash
python rollout.py path_to_your_checkpoint --env gfootball --run PPO --scenario-name "11_vs_11_stochastic" --num-agents 11 --episodes 20 --steps 10000
```
If you want to compute the agents' contributions using Shapley values, just pass the argument `--compute-shapley` to `rollout.py`.
