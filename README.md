<div align="center">
    <img alt="OpenRLHF logo" src="./docs/logo.png" style="height: 140px;" />
</div>
<div align="center">
<p align="center">
      <a href="https://github.com/OpenRLHF/OpenRLHF/graphs/contributors">
        <img alt="GitHub Contributors" src="https://img.shields.io/github/contributors/OpenRLHF/OpenRLHF" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/issues">
        <img alt="Issues" src="https://img.shields.io/github/issues/OpenRLHF/OpenRLHF?color=0088ff" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/discussions">
        <img alt="Issues" src="https://img.shields.io/github/discussions/OpenRLHF/OpenRLHF?color=0088ff" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/pulls">
        <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/OpenRLHF/OpenRLHF?color=0088ff" />
      <a href="https://github.com/OpenRLHF/OpenRLHF/stargazers">
        <img alt="GitHub stars" src="https://img.shields.io/github/stars/OpenRLHF/OpenRLHF?color=ccf" />
      </a>
      <a href="https://deepwiki.com/OpenRLHF/OpenRLHF"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
      <br>
      <em>Open-source / Comprehensive / Lightweight / Easy-to-use</em>
    </p>
</p>
</div>

<hr>

<span>[ English | <a href="README_zh.md">中文</a> | <a href="README_ja.md">日本語</a> ]</span>

OpenRLHF is the first easy-to-use, high-performance open-source RLHF framework built on Ray, vLLM, ZeRO-3 and HuggingFace Transformers, designed to make RLHF training simple and accessible:

- **Distributed Architecture with Ray**  
  OpenRLHF leverages [Ray](https://github.com/ray-project/ray) for efficient distributed scheduling. It separates the Actor, Reward, Reference, and Critic models across different GPUs, enabling scalable training for models up to 70B parameters.  
  It also supports **Hybrid Engine** scheduling, allowing all models and vLLM engines to share GPU resources—minimizing idle time and maximizing GPU utilization.
- **vLLM Inference Acceleration + AutoTP**  
  RLHF training spends 80% of the time on the sample generation stage. Powered by [vLLM](https://github.com/vllm-project/vllm) and Auto Tensor Parallelism (AutoTP), OpenRLHF delivers high-throughput, memory-efficient samples generation. Native integration with HuggingFace Transformers ensures seamless and fast generation, making it the fastest RLHF framework available.
- **Memory-Efficient Training with ZeRO-3 / AutoTP**  
  Built on [DeepSpeed's](https://github.com/deepspeedai/DeepSpeed) ZeRO-3, [deepcompile](https://github.com/deepspeedai/DeepSpeed/blob/master/blogs/deepcompile/README.md) and [AutoTP](https://github.com/deepspeedai/DeepSpeed/blob/master/blogs/huggingface-tp/README.md), OpenRLHF enables large model training without heavyweight frameworks. It works directly with HuggingFace for easy loading and fine-tuning of pretrained models.
- **Optimized PPO Implementation**  
  Incorporates advanced PPO tricks inspired by practical guides and community best practices, enhancing training stability and reward quality in RLHF workflows. Referencing [Zhihu](https://zhuanlan.zhihu.com/p/622134699) and [Advanced Tricks for Training Large Language Models with Proximal Policy Optimization](https://hijkzzz.notion.site/rlhf-implementation-tricks?v=158d9a33ecc98132bf9e000c39227361).

More details are in [Slides](https://docs.google.com/presentation/d/1JRhB1d7csofx0PIZBmfyBdMluxNd5JLPpUHrrvVhGnk/edit?usp=sharing) | [Technical Report](https://arxiv.org/abs/2405.11143) | [Documents](https://openrlhf.readthedocs.io/)

## News
- [2025/6] [Magistral](https://mistral.ai/static/research/magistral.pdf) uses the REINFORCE++-baseline to train the reasoning models.
- [2025/5] [MARTI](https://github.com/TsinghuaC3I/MARTI) has been released as a fork of OpenRLHF. It is designed to train LLM-based multi-agent systems using RL, by integrating centralized multi-agent interactions with distributed policy training.
- [2025/5] OpenRLHF 0.8.0 supports [Async Pipeline RLHF](./examples/scripts/train_reinforce_baseline_llama_ray_async.sh) (`--async_train`) and [Async Agent RLHF](./examples/scripts/train_reinforce_baseline_llama_ray_agent_async.sh)(`--agent_func_path`)
- [2025/4] Post the blog [Accelerating RLHF with vLLM, Best Practice from OpenRLHF](https://blog.vllm.ai/2025/04/23/openrlhf-vllm.html)
- [2025/4] Clean OpenRLHF: Refactored the source code based on Single Controller and Unified Packing Samples
- [2025/3] The CMU [Advanced Natural Language Processing Spring 2025](https://cmu-l3.github.io/anlp-spring2025/) course uses OpenRLHF as the RLHF framework teaching case.
- [2025/2] [Logic-RL](https://arxiv.org/abs/2502.14768) and [PRIME](https://arxiv.org/abs/2502.01456) demonstrate that REINFORCE++ is more stable in training compared to GRPO and faster than PPO.
- [2025/2] [LMM-R1](https://github.com/TideDra/lmm-r1) is a fork of OpenRLHF, aimed at providing high-performance RL infrastructure for reproduction of DeepSeek-R1 on multimodal tasks.
- [2025/2] MIT & Microsoft proposed the [On the Emergence of Thinking in LLMs I: Searching for the Right Intuition](https://arxiv.org/pdf/2502.06773) using OpenRLHF
- [2025/1] HKUST reproduced the [DeepSeek-R1-Zero and DeepSeek-R1 training on small models using OpenRLHF](https://github.com/hkust-nlp/simpleRL-reason)
- [2024/12] We "proposed" 😊 the [REINFORCE++: A Simple and Efficient Approach for Aligning Large Language Models](https://www.researchgate.net/publication/387487679_REINFORCE_A_SIMPLE_AND_EFFICIENT_APPROACH_FOR_ALIGNING_LARGE_LANGUAGE_MODELS).
- [2024/12] We analyzed the PPO, REINFORCE++, GRPO and RLOO in the [Notion Blogpost](https://hijkzzz.notion.site/unraveling-rlhf-and-its-variants-engineering-insights#147d9a33ecc9806090f3d5c749d31f05).
- [2023/8] OpenRLHF was open-sourced. 


## Features

- Distributed [PPO](./examples/scripts/train_ppo_llama_ray.sh) and [REINFORCE++/REINFORCE++-baseline/GRPO/RLOO](./examples/scripts/train_reinforce_llama_ray_hybrid_engine.sh) implementations based on Ray.  
- Support Ray-based [PPO](./examples/scripts/train_ppo_llama_ray_hybrid_engine.sh) and [REINFORCE++/REINFORCE++-baseline/GRPO/RLOO](./examples/scripts/train_reinforce_llama_ray_hybrid_engine.sh) using Hybrid Engine  (`--colocate_all_models`, `--vllm_enable_sleep` and `--vllm_gpu_memory_utilization 0.5`)
- [Ray-based Reinforced Finetuning](./examples/scripts/train_ppo_llama_with_reward_fn.sh)
- Integration with vLLM for accelerated generation in RLHF tasks (`--vllm_num_engines`).  
- Support RL Dynamic Sampling from DAPO(`--dynamic_filtering` and `--dynamic_filtering_reward_range`)
- Support [DeepSpeed AutoTP training](./examples/scripts/train_sft_llama_tensor_parallelism.sh) (`--ds_tensor_parallel_size`)
- Implementation of [RingAttention](./examples/scripts/train_dpo_ring_llama.sh) (`--ring_attn_size`, `--ring_head_stride`).  
- Implementation of [DPO (Direct Preference Optimization)/IPO/cDPO](./examples/scripts/train_dpo_llama.sh) and [Kahneman-Tversky Optimization (KTO)](./examples/scripts/train_kto_llama.sh).  
- Support for [Iterative DPO](./examples/scripts/train_iterative_dpo_llama.sh) ([GitHub: Online-RLHF](https://github.com/RLHFlow/Online-RLHF)).  
- Support for [Rejection Sampling](./examples/scripts/train_rejection_sampling_llama.sh).  
- Implementation of [Conditional SFT](./examples/scripts/train_conditional_llama.sh) ([arXiv:2308.12050](https://arxiv.org/abs/2308.12050)).  
- Support for [Knowledge Distillation](./examples/scripts/train_knowledge_distillation.sh) ([Microsoft: minillm](https://github.com/microsoft/LMOps/tree/main/minillm)).  
- Integration of [Process Reward Model (PRM)](./examples/scripts/train_prm_mistral.sh).  
- Packing of training samples for SFT, DPO, RM, PRM, and PPO (`--packing_samples`).  
- Support for [Mixture of Experts (MoE)](./examples/test_scripts/train_sft_mixtral_lora.sh) (`--aux_loss_coef`).  
- Integration of FlashAttention2 (`--flash_attn`).  
- Support for QLoRA (`--load_in_4bit`) and [LoRA](./examples/scripts/train_sft_mixtral_lora.sh) (`--lora_rank`, `--target_modules`).  
- Compatibility with HuggingFace's `tokenizer.apply_chat_template` for datasets (`--apply_chat_template` and `--input_key`).  
- Logging support with Wandb (`--use_wandb`) and TensorBoard (`--use_tensorboard`).  
- Checkpoint recovery functionality (`--load_checkpoint` and `--save_steps`).  
- Provided multi-node training scripts, such as [DPO](./examples/scripts/train_llama_slurm.sh) and [Ray PPO](./examples/scripts/train_ppo_llama_ray_slurm.sh).

## Quick Start

### Installation

To use OpenRLHF, first launch the docker container (**Recommended**) and `pip install` openrlhf inside the docker container:

```bash
# Launch the docker container
docker run --runtime=nvidia -it --rm --shm-size="10g" --cap-add=SYS_ADMIN -v $PWD:/openrlhf nvcr.io/nvidia/pytorch:25.02-py3 bash
sudo pip uninstall xgboost transformer_engine flash_attn pynvml -y

# pip install
pip install openrlhf

# If you want to use vLLM acceleration (Install vLLM 0.9.0.1)
pip install openrlhf[vllm]
# latest vLLM is also supported
pip install openrlhf[vllm_latest]
# Install vLLM, ring-flash-attention and Liger-Kernel
pip install openrlhf[vllm,ring,liger]

# Install flash-attn 2.7.4.post1 for PyTorch 2.7
# Example for Python 3.12, replace filename if using 3.10 or 3.11
pip install https://github.com/OpenRLHF/flash-attn-2.7.4.post1-builds/releases/download/v0.1/flash_attn-2.7.4.post1+pt270cu128cxx11abiTRUE-cp312-cp312-linux_x86_64.whl

# pip install the latest version
pip install git+https://github.com/OpenRLHF/OpenRLHF.git

# Or git clone
git clone https://github.com/OpenRLHF/OpenRLHF.git
cd OpenRLHF
pip install -e .
```

> [!NOTE]
>We recommend using vLLM 0.9.0.1 or higher.
>We also provided the [Dockerfiles for vLLM](./dockerfile/) and [One-Click Installation Script of Nvidia-Docker](./examples/scripts/nvidia_docker_install.sh).

### Prepare Datasets
OpenRLHF provides multiple data processing methods in our dataset classes.
Such as in the [Prompt Dataset](https://github.com/OpenRLHF/OpenRLHF/blob/main/openrlhf/datasets/prompts_dataset.py#L6):

```python
def preprocess_data(data, input_template=None, input_key="input", apply_chat_template=None) -> str:
    if apply_chat_template:
        chat = data[input_key]
        if isinstance(chat, str):
            chat = [{"role": "user", "content": chat}]
        prompt = apply_chat_template(chat, tokenize=False, add_generation_prompt=True)
    else:
        prompt = data[input_key]
        if input_template:
            prompt = input_template.format(prompt)
    return prompt
```

- We can use `--input_key` to specify the `JSON key name` of the input datasets `--prompt_data {name or path}` (PPO) or `--dataset {name or path}`, and use `--apply_chat_template` to utilize the `chat_template` from the [Huggingface Tokenizer](https://huggingface.co/docs/transformers/main/en/chat_templating).
- If you don't want to use `--apply_chat_template`, you can use `--input_template` instead, or preprocess the datasets offline in advance.
- OpenRLHF also support mixing multiple datasets using `--prompt_data_probs 0.1,0.4,0.5` (PPO) or `--dataset_probs 0.1,0.4,0.5`.

How Chat Templating Works:

```python
dataset = [{"input_key": [
  {"role": "user", "content": "Hello, how are you?"},
  {"role": "assistant", "content": "I'm doing great. How can I help you today?"},
  {"role": "user", "content": "I'd like to show off how chat templating works!"},
]}]

tokenizer.apply_chat_template(dataset[0]["input_key"], tokenize=False)

"<s>[INST] Hello, how are you? [/INST]I'm doing great. How can I help you today?</s> [INST] I'd like to show off how chat templating works! [/INST]"
```

How to specify test datasets ?

Please set test datasets path using ``--eval_dataset {name or path}``.


> [!NOTE]
> The ``JSON key`` options depends on the specific datasets. See [Reward Dataset](https://github.com/OpenRLHF/OpenRLHF/blob/main/openrlhf/datasets/reward_dataset.py#L10) and [SFT Dataset](https://github.com/OpenRLHF/OpenRLHF/blob/main/openrlhf/datasets/sft_dataset.py#L9)

### Supervised Fine-tuning

OpenRLHF's model checkpoint is fully compatible with HuggingFace models. You can specify the model name or path using `--pretrain  {name or path}`, `--reward_pretrain  {name or path}` and `--critic_pretrain  {name or path}`. We have provided some pre-trained checkpoints and datasets on [HuggingFace OpenRLHF](https://huggingface.co/OpenRLHF).

Then you can use the startup scripts we provide in the [examples/scripts](./examples/scripts/) directory, or start the training using the following commands.

```bash 
deepspeed --module openrlhf.cli.train_sft \
   --max_len 4096 \
   --dataset Open-Orca/OpenOrca \
   --input_key question \
   --output_key response \
   --input_template $'User: {}\nAssistant: ' \
   --train_batch_size 256 \
   --micro_train_batch_size 2 \
   --max_samples 500000 \
   --pretrain meta-llama/Meta-Llama-3-8B \
   --save_path ./checkpoint/llama3-8b-sft \
   --save_steps -1 \
   --logging_steps 1 \
   --eval_steps -1 \
   --zero_stage 2 \
   --max_epochs 1 \
   --packing_samples \
   --bf16 \
   --flash_attn \
   --learning_rate 5e-6 \
   --gradient_checkpointing \
   --use_wandb {wandb_token}

# Support HF tokenizer.apply_chat_template
# --apply_chat_template 
# --tokenizer_chat_template {HF Chat Template}

# Support RingAttention
# pip install ring_flash_attn
#   --ring_attn_size 2 \
#   --ring_head_stride 2 \

# Multi-turn fine-tuning loss
# --multiturn

# Can also be used for continued pre-training
# --pretrain_mode
```

> [!NOTE]
> OpenRLHF SFT/DPO/RewardModel/PPO trainers support `--packing_samples` [based on `--flash_attn`](https://github.com/MeetKai/functionary/tree/main/functionary/train/packing)


### Reward Model Training
```bash
deepspeed --module openrlhf.cli.train_rm \
   --save_path ./checkpoint/llama3-8b-rm \
   --save_steps -1 \
   --logging_steps 1 \
   --eval_steps -1 \
   --train_batch_size 256 \
   --micro_train_batch_size 1 \
   --pretrain OpenRLHF/Llama-3-8b-sft-mixture \
   --bf16 \
   --max_epochs 1 \
   --max_len 8192 \
   --zero_stage 3 \
   --learning_rate 9e-6 \
   --dataset OpenRLHF/preference_dataset_mixture2_and_safe_pku \
   --apply_chat_template \
   --chosen_key chosen \
   --rejected_key rejected \
   --flash_attn \
   --packing_samples \
   --gradient_checkpointing \
   --use_wandb {wandb_token}

```

It is recommended to set the `--value_prefix_head` option of the Reward Model to `score`, so that we can load the model using `AutoModelForSequenceClassification`:

```python
reward_model = AutoModelForSequenceClassification.from_pretrained(
              reward_model_path,
              num_labels=1,
              torch_dtype=torch.bfloat16,
              attn_implementation="flash_attention_2",
              use_cache=False,
          )
inputs = xxxx (Left Padding Input Tokens)
reward = reward_model.model(*inputs).last_hidden_state
reward = reward_model.score(reward)[:, -1]
```

### PPO/REINFORCE++ with Ray and vLLM

To improve RLHF training speed or support 70B models, we can use the PPO with Ray and vLLM acceleration (Hybrid Engine)

```bash
# launch the master node of ray in container
ray start --head --node-ip-address 0.0.0.0 --num-gpus 8

# if you want to launch ray on more nodes, use
ray start --address {MASTER-NODE-ADDRESS}:6379  --num-gpus 8

ray job submit --address="http://127.0.0.1:8265" \
   --runtime-env-json='{"working_dir": "/openrlhf"}' \
   -- python3 -m openrlhf.cli.train_ppo_ray \
   --ref_num_nodes 1 \
   --ref_num_gpus_per_node 8 \
   --reward_num_nodes 1 \
   --reward_num_gpus_per_node 8 \
   --critic_num_nodes 1 \
   --critic_num_gpus_per_node 8 \
   --actor_num_nodes 1 \
   --actor_num_gpus_per_node 8 \
   --vllm_num_engines 4 \
   --vllm_tensor_parallel_size 2 \
   --colocate_all_models \
   --vllm_gpu_memory_utilization 0.5 \
   --pretrain OpenRLHF/Llama-3-8b-sft-mixture \
   --reward_pretrain OpenRLHF/Llama-3-8b-rm-700k \
   --save_path /openrlhf/examples/test_scripts/final/llama3-8b-rlhf \
   --ckpt_path /openrlhf/examples/test_scripts/ckpt/llama3-8b-rlhf \
   --save_hf_ckpt \
   --micro_train_batch_size 8 \
   --train_batch_size 128 \
   --micro_rollout_batch_size 16 \
   --rollout_batch_size 1024 \
   --n_samples_per_prompt 1 \
   --max_epochs 1 \
   --prompt_max_len 1024 \
   --max_samples 100000 \
   --generate_max_len 1024 \
   --zero_stage 3 \
   --bf16 \
   --actor_learning_rate 5e-7 \
   --critic_learning_rate 9e-6 \
   --init_kl_coef 0.01 \
   --prompt_data OpenRLHF/prompt-collection-v0.1 \
   --input_key context_messages \
   --apply_chat_template \
   --normalize_reward \
   --gradient_checkpointing \
   --packing_samples \
   --vllm_sync_backend nccl \
   --enforce_eager \
   --vllm_enable_sleep \
   --deepspeed_enable_sleep
   --use_wandb {wandb_token}

# Support REINFORCE++  | RLOO | REINFORCE++-baseline | GRPO | Dr. GRPO
# --advantage_estimator reinforce | rloo | reinforce_baseline | group_norm | dr_grpo

# Set --init_kl_coef to 0 will not launch the reference model

# Support remote reward model (HTTP)
# --remote_rm_url http://localhost:5000/get_reward

# Support N samples
# --n_samples_per_prompt 4
```
> [!NOTE]
> You can also use ``setup_commands`` to let Ray automatically deploy the environment, such as `--runtime-env-json='{"setup_commands": ["pip install openrlhf[vllm]"]}'`.

> [!NOTE]
> RLOO and REINFORCE++-baseline in OPENRLHF are a modification based on REINFORCE++:
> - REINFORCE++ integrates key optimization techniques from PPO (such as advantage normalization and PPO-clip loss) into REINFORCE while eliminating the need for a critic network.
> - REINFORCE++-baseline uses the `mean reward of multiple samples from the same prompt` as the baseline to reshape the rewards then apply the global advantage normalization in REINFORCE++.
> - RLOO in OpenRLHF modifies the original version by incorporating the `per-token KL reward` and utilizing the `PPO-clip loss`.
> - Dr. GRPO remove the local group normalization `/std` in GRPO.


> [!NOTE]
> If you you encounter an error related to index out of range when deepspeed sets up the GPU devices, you can try to set the environment variable [`RAY_EXPERIMENTAL_NOSET_*_VISIBLE_DEVICES`](openrlhf/trainer/ray/utils.py) as a workaround.
>   ```bash
>   # For NVIDIA GPUs:
>   export RAY_EXPERIMENTAL_NOSET_CUDA_VISIBLE_DEVICES=1
>   ```

The launch scripts and documents for supported algorithms are in [example/scripts](./examples/scripts/) and [Documents - Usage](https://openrlhf.readthedocs.io/en/latest/usage.html)

## Reinforced Fine-tuning

OpenRLHF supports convenient and efficient Reinforced Fine-tuning. You only need to implement a [file containing the custom `reward_func` function](./examples/scripts/reward_func.py) and pass its path to the `remote_rm_url` parameter. Such as

```python
# reward_func.py
import torch

def reward_func(queries, prompts, labels):
    # queries is prompts + responses
    # labels is answers
    print(queries)

    # Generate random rewards as an example
    # In real applications, this should be replaced with actual reward calculation logic
    reward = torch.randint(0, 2, (len(queries),)).float()

    return {
        "rewards": reward,  # Rewards for advantage calculation
        "scores": reward,  # Scores for dynamic filtering (0-1 reward)
        "extra_logs": {"dummy_scores": reward},  # Additional logging info for wandb
    }
```

then just set

```shell 
ray job submit --address="http://127.0.0.1:8265" \
  --runtime-env-json='{"working_dir": "/openrlhf"}' \
  -- python3 -m openrlhf.cli.train_ppo_ray \
  ...
  --remote_rm_url /path/to/reward_func.py \
  --label_key answer
```

where the `label_key` parameter is used to pass additional sample information such as answer to the reward function.

## Async RLHF & Agent RLHF

OpenRLHF provides comprehensive support for both Asynchronous RLHF and Agent-based RLHF implementations. To utilize these features, simply include the `--async_train` and `--agent_func_path` parameters in your training configuration. 

```python
# agent_func.py
step_idx = 0
max_steps = 2

# A n-step random environment
async def step(observation, action, label, **kwargs) -> Dict[str, Any]:
    global step_idx, max_steps
    print(f"step_idx: {step_idx}, max_steps: {max_steps}")

    # End after verification
    if step_idx >= max_steps:
        done = True
        # Generate a random reward using torch.rand
        reward = torch.randint(0, 2, (1,)).float()
        next_observation = (
            observation
            + action
            + "\n\nHuman: [VERIFICATION RESULT: CORRECT]\nYour solution is valid and complete. The verification process is finished.\n</s>"
        )
    else:
        done = False
        reward = torch.tensor(0)
        # Update observation
        next_observation = (
            observation
            + action
            + "\n\nHuman: [VERIFICATION RESULT: INCORRECT]\nLet's analyze what needs improvement:\n1. What are the key issues in the current solution?\n2. How can we make it more robust?\n3. What additional considerations should we take into account?\n\nPlease provide your revised solution:\n</s>\n\nAssistant: "
        )
    step_idx += 1

    return {
        "rewards": reward,  # Rewards for advantage calculation
        "scores": reward,  # Scores for dynamic filtering (0-1 reward)
        "next_observation": next_observation,  # The updated observation for vLLM inference in next step
        "done": done,  # Boolean indicating if the episode is complete
        "sampling_params": kwargs.get("sampling_params", None),  # Parameters for vLLM sampling in next step
        "extra_logs": {"dummy_scores": reward},  # Additional logging information
    }
```

You can also configure the maximum number of concurrent agents per vLLM engine by setting `export OPENRLHF_ASYNC_NUM_TASKS=128`. 
Additionally, you can control the degree of off-policy sampling by setting `export OPENRLHF_ASYNC_QUEUE_SIZE=1` (this parameter controls how many batches of data can be stored in the buffer at most) in your environment.

> [!NOTE] 
> OpenRLHF's Agent RLHF also supports Hybrid Engine training. To enable this feature, please remove the `--async_train` flag and enable `--colocate_all_models`.

> [!WARNING] 
> Asynchronous training may affect the training stability. It is recommended to prioritize using Hybrid Engine or synchronous training mode.

### LoRA
If you use `LoRA (Low-Rank Adaptation)`, `OpenRLHF` will not save the full weights by default instead of `LoRA Adapter`. To continue in your task normally, you should combine the `Adapter` with weights of your base model

```bash
python -m openrlhf.cli.lora_combiner \
    --model_path meta-llama/Meta-Llama-3-8B \
    --lora_path ./checkpoint/llama3-8b-rm \
    --output_path ./checkpoint/llama-3-8b-rm-combined \
    --is_rm \
    --bf16
```

### Performance Tuning Guide

To achieve optimal performance, we recommend allocating nodes `vLLM:Actor:Critic = 1:1:1`. 

- For example, for a 70B model with 48 A100 GPUs, it is advised to allocate 16 A100 GPUs to the vLLM Engine, 16 GPUs to the Actor model, and the remaining 16 GPUs to the Critic model. 
- Enable asynchronous training `--async_train` when the convergence of the RL algorithm meets requirements.
- Using hybrid engine `--colocate_all_models` and `--vllm_enable_sleep` and `--deepspeed_enable_sleep` rather than distributed RLHF when there are enough GPU memory.
- Enable the `--colocate_critic_reward`, `--colocate_actor_ref` options to merge nodes.  
- You should increase the `rollout_micro_batch_size` (and minimize the TP size of vLLM engine) as much as possible. During the training phase, a larger `--micro_train_batch_size` is better and enable `--packing_samples`.
- When there are enough GPU memory, please disable `--adam_offload` and enable `--overlap_comm`.  Also enable ``--deepcompile`` to speed up the training.
- For vLLM, please use `--vllm_sync_backend nccl`
- Enable [enable_prefix_caching](https://docs.vllm.ai/en/stable/automatic_prefix_caching/apc.html) in vLLM generation when `n_samples_per_prompts` > 1.
- For a large base model, if an OOM occurs, do not use any `--colocate_xxxx` options.


## Companies and Organizations using OpenRLHF

- Google
- ByteDance
- Tencent
- Alibaba
- Baidu
- China Telecom
- Vivo
- Allen AI
- NexusFlow
- Jülich Supercomputing Centre (JSC)
- Berkeley Starling Team
- M-A-P
- ...

## Join Us

**How to Join?**

1. Email us at janhu9527@gmail.com or join [GitHub Organization](https://github.com/OpenRLHF). Please include the following details:
   - Your name
   - Your GitHub username
   - Your areas of interest
   - Your skills and experience related to NLP and/or AI
1. You can also join us through the official GitHub [OpenRLHF ↗](https://github.com/OpenRLHF/OpenRLHF) project page. Just create an issue about your interest to contribute and we will get back to you.

**What can you do?**

1. Join the team and participate in the development of the OpenRLHF project.
1. Contribute to the project by submitting pull requests.
1. Help improve documentation, fix bugs, or create new features.
1. Share the project and help us grow the community.

## Sponsor Us

Your sponsorship can help us maintain and improve OpenRLHF. If you find this project useful, please consider sponsoring us. You can sponsor us on [Open Collective ↗](https://opencollective.com/OpenRLHF).

## Starchart

[![Star History Chart](https://api.star-history.com/svg?repos=OpenRLHF/OpenRLHF&type=Date)](https://star-history.com/#OpenRLHF/OpenRLHF&Date)

## Contributors

A big thank you to all our contributors! If you want to contribute, feel free to make a pull request or create an issue.

<a href="https://github.com/OpenRLHF/OpenRLHF/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=OpenRLHF/OpenRLHF" />
</a>

## References & Acknowledgements

We would like to express our gratitude to the following projects and organizations for their contributions to the field of AI and NLP:

- [Hugging Face Transformers ↗](https://github.com/huggingface/transformers)
- [OpenAI GPT ↗](https://github.com/openai/gpt-3)
- [LLaMA ↗](https://llama.meta.com/)
- [DeepSpeed ↗](https://github.com/microsoft/DeepSpeed)
- [Ray ↗](https://github.com/ray-project/ray)

Our project would also like to thank [ColossalChat](https://github.com/hpcaitech/ColossalAI/tree/main/applications/ColossalChat) and [DeepSpeedChat](https://github.com/microsoft/DeepSpeedExamples/tree/master/applications/DeepSpeed-Chat). In the early stages of the project, we referred to their code design. 
Our project would like to thank [Netmind.AI](https://www.netmind.ai/) for the GPU support of developing ring attention.

(2024/7) Our GitHub organization has changed from OpenLLMAI to OpenRLHF.

## Citation
```
@article{hu2024openrlhf,
  title={OpenRLHF: An Easy-to-use, Scalable and High-performance RLHF Framework},
  author={Jian Hu and Xibin Wu and Zilin Zhu and Xianyu and Weixun Wang and Dehao Zhang and Yu Cao},
  journal={arXiv preprint arXiv:2405.11143},
  year={2024}
}
```

______________________________________________________________________

*OpenRLHF © 2025 OpenRLHF. All Rights Reserved.*
