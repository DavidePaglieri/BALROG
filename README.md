<p align="center">
  <a href="https://balrogai.com">
    <img src="docs/imgs/balrog_banner.png" width="50%" alt="BALROG Agent" />
  </a>
</p>

---

# BALROG: Benchmarking Agentic LLM and VLM Reasoning On Games
BALROG is a novel benchmark evaluating agentic LLM and VLM capabilities on long-horizon interactive tasks using reinforcement learning environments. Check out how current models fare on our [leaderboard](https://balrogai.com). You can read more about BALROG in our [paper](https://arxiv.org/abs/2411.13543).

## Features
- Comprehensive evaluation of agentic abilities
- Support for both language and vision-language models
- Integration with popular AI APIs and local deployment
- Easy integration for custom agents, new environments and new models

## Installation
We advise using conda for the installation
```bash
conda create -n balrog python=3.10 -y
conda activate balrog

git clone https://github.com/balrog-ai/BALROG.git
cd BALROG
pip install -e .
balrog-post-install
```

## Docker
We have provided some docker images. Please see the [relevant README](docker/README.md).

## ⚡️ Evaluate using vLLM locally
We support running LLMs/VLMs locally using [vLLM](https://github.com/vllm-project/vllm). You can spin up a vLLM client and evaluate your agent on BALROG in the following way:

```bash
pip install vllm numpy==1.23
vllm serve meta-llama/Llama-3.2-1B-Instruct --port 8080

python eval.py \
  agent.type=naive \
  agent.max_image_history=0 \
  agent.max_history=16 \
  eval.num_workers=32 \
  client.client_name=vllm \
  client.model_id=meta-llama/Llama-3.2-1B-Instruct \
  client.base_url=http://0.0.0.0:8080/v1
```

Check out [vLLM](https://github.com/vllm-project/vllm) for more options on how to serve your models fast and efficiently.

## 🛜 Evaluate using popular APIs
We support out of the box clients for OpenAI, Anthropic and Google Gemini APIs. First set up your API key:

```bash
export OPENAI_API_KEY=<KEY>
export ANTHROPIC_API_KEY=<KEY>
export GEMINI_API_KEY=<KEY>
```

Then run the evaluation with:

```bash
python eval.py \
  agent.type=naive \
  agent.max_image_history=0 \
  eval.num_workers=64 \
  client.client_name=openai \
  client.model_id=gpt-4o-mini-2024-07-18
```

## Documentation
- [Evaluation Guide](https://github.com/balrog-ai/BALROG-dev/blob/main/docs/evaluation.md) - Detailed instructions for various evaluation scenarios
- [Agent Development](https://github.com/balrog-ai/BALROG-dev/blob/main/docs/agents.md) - Tutorial on creating custom agents

We welcome contributions! Please see our [Contributing Guidelines](https://github.com/balrog-ai/BALROG-dev/blob/main/docs/contribution.md) for details.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Citation
If you use BALROG in any of your work, please cite:

```
@article{paglieri2024balrog,
  title={Benchmarking Agentic LLM and VLM Reasoning On Games},
  author={Paglieri, Davide and and Cupia{\l}, Bart{\l}omiej and Coward, Sam and Piterbarg, Ulyana and Wo{\l}czyk, Maciej and Khan, Akbir and Pignatelli, Eduardo and Kuci{\'n}ski, {\L}ukasz and Pinto, Lerrel and Fergus, Rob and Foerster, Jakob Nicolaus and Parker-Holder, Jack and Rockt{\"a}schel, Tim},
  journal={arXiv preprint arXiv:2411.13543},
  year={2024}
}
```