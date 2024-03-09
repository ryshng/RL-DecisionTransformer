# Decision Transformer for Atari

## Motivation
hey are more intricate than simple environments but not as complex as real-world robotic tasks.

We decided to train Atari games using a decision transformer for some reasons:
- Complexity: Atari games offer a visually rich and diverse environment, in some cases more complex than other more simpler environments often used in RL. Some Atari games are specially challenging due to the difficulty of credit assignment arising from the delay between actions and resulting rewards
- Benchmarking: Atari games serve as a well-established benchmark for RL algorithms, that allows us to compare the performance of owr model with other RL techniques.

## Implementation
We implemented from scratch another Decision Transformer to try to solve Atari games. This DT is very similar to the previous one, except that:
- convolutional encoder: In a transition, the state is an image of the game screen. In fact, a stack of images of the last 4 transitions (to catch information like velocity objects). The state is fed into a convolutional encoder instead of a linear layer to obtain token embeddings. The fact that the states are images and take up much more space complicates the data management.
- cross-entropy loss function: An Atari game typically have a discrete set of actions (e.g., jump, move left, shoot). So, we use the cross-entropy loss function instead of the mean-squared error. 

![vpt_schema](https://github.com/SwissTonyStark/GameMindsDT/assets/155813568/dabd6445-2d82-4a65-94df-8969acd390d2)
*Credits for some images*: https://cdn.openai.com/vpt/Paper.pdf, https://arxiv.org/pdf/2106.01345.pdf, https://www.minecraft.net/

We use a different version of gym and a dedicated version of D4rl, to have access to the Atari datasets 
https://github.com/takuseno/d4rl-atari

The original paper uses Tanh (hyperbolic tangents) instead of LayerNorm  after the embeddings, but we obtained the same or worst results using Tanhs.
We adapted the position encoding with an alternative version that improves the performance thanks to the d3lply library
https://github.com/takuseno/d3rlpy

We have used hyperparameter values similar to those of the original paper:
    * embedding dimension 128
    * layers (blocks) 6
    * attention heads 8
    * context length 30
    * Return-to-go conditioning 
        * Qbert 2500
        * Seaquest 1450
        * Space Invaders 20000
        * Breakout 90
    * The same as the end-of-episode reward

We inspired our implementation on the following repositories:
https://github.com/kzl/decision-transformer
https://github.com/nikhilbarhate99/min-decision-transformer

## Results

We trained the Breakout, Qbert, Space_invaders and Seaquest.
In the evaluation, As the reward may vary between episodes, after every epoch we calcule the mean of the total rewards of 100 episodes.
We trained the model with a dataset of 1.000.000 trajectories and we observed that the model overfit after aproximately 3/4 epochs.

Atari games perform better when trained with expert data. We trained Breakout with mixed data and, as a result, the performance is not as good as the other games.

At test time the DT is handed the first return-to-go token, indicating the desirable return to reach in the task. Til aprox. 5 times the maximum return-to-go in the dataset, he results show a correlation between desired target return and true observed return. We used higher initial return-to-go with a similar result as 5x the maximum in the dataset.
 
Our results are similar as the original DT paper, and usually better than other RL techniques.

![dt_rollouts](https://github.com/SwissTonyStark/GameMindsDT/assets/155813568/a0bbe1d2-6a97-46d9-87b6-757fb8daae83)

## Conclusions & Future work



# Installation:

## Installation options:

### 1/ just run our colab:
https://colab.research.google.com/drive/1KhUZoDw-3lbm41GLiuoboDp6pn4dfAoe?usp=sharing
or execute the notebook in the repository `DT_from_scratch_Atari_Simplified.ipynb

### 2/ local installation:

Dependencies can be installed with the following command:

```
conda create --name dt python=3.10.12
conda activate dt
pip install git+https://github.com/takuseno/d4rl-atari
#brew install cmake zlib # on mac only
#pip install gym[atari]
#pip install autorom[accept-rom-license]
#pip install autorom
pip install 'gym [atari,accept-rom-license]==0.25.2'
pip install -r requirements.txt
```

Example usage

Scripts to reproduce our Decision Transformer results can be found in `train_.sh`.

By default:
```
python main.py
```


### Demo videos

The agent not only learns to find caves. It also learns other basic skills such as escaping from zombies, avoiding obstacles, getting out of traps, exploring, navigating through caves, swimming, etc. Here are some demonstration shortcuts from the many journeys our agent has made.

[hole_in_one.webm](https://github.com/SwissTonyStark/GameMindsDT/assets/155813568/3d89bbda-cee0-4db3-8fa4-9f6dfd3207bd)


## Multi-game Decision Transformer

  
![minedojo_hdt](https://github.com/SwissTonyStark/GameMindsDT/assets/155813568/0516f842-b7dd-40e6-9352-8580fc8f1be8)





## Acknowledgements:
**Mine_rl** MineRL is a rich Python 3 library which provides a OpenAI Gym interface for interacting with the video game Minecraft, accompanied with datasets of human gameplay. 
(https://minerl.readthedocs.io/en/latest/)

**vpt_lib:** OpenAI Video PreTraining (VPT): Learning to Act by Watching Unlabeled Online Videos: (https://github.com/openai/Video-Pre-Training)
- We have used the VPT library to extract the features from the videos and use them as input to the model. 
- We slightly modified the code to fit our needs. Concretly, we have separated the button actions from the camera actions. We have also deactivated inventory actions (for cave search).

**basalt and basalt-benchmark:**
- **Basalt:** NeurIPS 2022: MineRL BASALT Behavioural Cloning Baseline: (https://github.com/minerllabs/basalt-2022-behavioural-cloning-baseline)
- **Basalt-benchmark:** (https://github.com/minerllabs/basalt-benchmark)
- We have adapted and reorganized the code from the basalt library to fit our Decision Transformer agent.

**d3rlpy:**
-   **d3rlpy:** A collection of Reinforcement Learning baselines and algorithms for model-based reinforcement learning: We have use his GlobalPositionEncoding. (https://github.com/takuseno/d3rlpy/tree/v2.3.0)

**hugging_face:**
-   **Hugging Face:** We have used the Hugging Face library to use the GPT-2 model and the Decision Transformer model. (https://huggingface.co/docs/transformers/model_doc/decision_transformer)

**other libraries:**
-   We have used other libraries such as numpy, pandas, torch, torchvision, etc.