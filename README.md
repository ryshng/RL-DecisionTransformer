# GameMindsDT
Unleashing the Power of Decision Transformers in Reinforcement Learning for mastering a variety of games and tasks, from classic arcade challenges to complex strategic simulations. Join us in building a custom Transformer model from scratch and exploring new frontiers in AI-driven gameplay.

## Overview
Welcome to **GameMindsDT**, an innovative project at the intersection of Decision Transformers and Reinforcement Learning, aimed at mastering a variety of games and tasks. Our mission is to build a Transformer from scratch, design a robust RL model, and train it to excel in diverse virtual environments.

## Motivation
Decision Transformers represent a paradigm shift in reinforcement learning, offering a more efficient and flexible approach to decision-making. This project endeavors to unlock the full potential of Decision Transformers in various gaming and task-oriented scenarios, pushing the boundaries of what these architectures can achieve.

## Installation
```bash
git clone https://github.com/your-username/GameMindsDT.git
cd GameMindsDT
pip install -r requirements.txt
```
## Features
- **Transformer Building from Scratch**: Deep and personalized learning of Transformer mechanics.
- **Customized RL Model**: Tailoring and fine-tuning models for different types of games and challenges.
- **Rigorous Training and Testing**: Assessment across various games, ranging from classics to contemporary.

## Usage
Guidance on how to use the model with code examples.
```python
# Example code snippet
```
## Contributing
Contributions are welcome! Please read `CONTRIBUTING.md` for details on how you can contribute to our project.

## License
This project is licensed under the [MIT License](LICENSE).

## Team
- Omar Aguilera Vera
- Pol Fernández Blánquez
- Shuang Long Ji Qiu
- Edgar Planell
- Alex Barrachina

## Experiments

We have used docker and notebooks to run the experiments. The notebooks are in the folder `notebooks` and the docker files are in the folder `docker`.

### Docker Experiments

We use docker to run the experiments.

Before running the docker, you need to install the nvidia-docker2 if we want to use the GPU and you don't have installed yet. You need a nvidia GPU at least compatible with CUDA 11.0. You can check the version of CUDA with the command `nvidia-smi`

```bash
sudo apt install -y nvidia-docker2
sudo systemctl daemon-reload
sudo systemctl restart docker
```

To buid the docker, you need to run the command `docker build -t gamemindsdt:latest .` in the folder `docker`. This command will build the docker with the name `gamemindsdt:latest`. The docker will install all the requirements and will clone the repository in the folder `/home`.

To run the docker, you need to run the command `docker run -it --gpus all --rm -v $(pwd):/home gamemindsdt:latest bash`. This command will run the docker with the name `gamemindsdt:latest` and will mount the current folder in the folder `/home`. The command will open a bash in the docker.

```bash
docker build -t gamemindsdt:latest . 
docker run -it --gpus all --rm -v $(pwd):/home gamemindsdt:latest bash
```

To run the experiments, you need to run the command `python main.py <experiment_name>` in the folder `/home`. The command will run the experiment `<experiment_name>`. For example:
```bash
python main.py pendulum
```


### Pendulum
Perform the test on the simplest gym with d3rl to test the decision transformers. We choose the pendulum environment because it is the simplest and we can see if the DT is able to learn the optimal policy.
**TODO:** Hyperparemter tuning (the simplest possible model).    

### Compare DT with other algorithms
Test the same environments as in the original paper, for the DT, CQL, BC algorithms and compare the results.
Are better DT than CQL and BC?
#### Open AI Gym (HalfCheetah, Hopper, Walker, Reacher)
**TODO:**

#### Atari games (Breakout, QBert, Pong, Seaquest)
**TODO:**

#### Minigrid (Door Key)
This environment has a key that the agent must pick up in order to unlock a goal and then get to the green goal square. This environment is difficult, because of the sparse reward, to solve using classical RL algorithms. It is useful to experiment with curiosity or curriculum learning.
**TODO:**

### Test DT with different hyperparameters. 
Are important size of model, number of layers, number of heads, number of attention heads, number of epochs, learning rate, batch size, etc.?
Which are the best hyperparameters for DT in every game?
#### Open AI Gym (HalfCheetah, Hopper, Walker, Reacher)
**TODO:**

#### Atari games (Breakout, QBert, Pong, Seaquest)
**TODO:**

#### Minigrid (Door Key)
**TODO:**

### Test DT with different data experiences.
Are important the size of the dataset and the type of data?
#### Atari games (mixed, expert)
**TODO:**

#### Open AI Gym (medium, medium-replay, medium-expert)
**TODO:**


## Acknowledgements
TBD.

## Contact
TBD(Contact information for inquiries and collaborations.)


---
![Uploading Logo.png…]()


