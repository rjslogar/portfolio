# Agent Throughput Predictor: Applying Basic Machine Learning

**TL;DR:** A PyTorch neural network that predicts how fast AI agents generate output from six workload inputs, validated on 1,000 unseen sessions, with documentation layered for different readers.

**Audience:** Interested readers with basic computing knowledge

**Reading time:** about 3 minutes

**Project documents:** [Summary](SUMMARY.md): project overview · [README](README.md): steps to set up and run the project · [Technical notes](TECHNICAL_NOTES.md): details for data results, code design, and project glossary

## At a glance

| | |
| **Problem** | AI agents slow down as they share hardware and take on longer, more complex work. Teams need to know in advance whether agents will meet their speed target |
| **What I built** | A PyTorch neural network that predicts an agent's tokens per second from six workload inputs, and a tool that checks each prediction against a 20 tokens/sec target |
| **Workload features** | Context length, tool calls, sub-agents, concurrent agents, cache hit rate and hardware tier |
| **Data** | 5,000 simulated agent sessions: 4,000 to train the model and 1,000 to test it |
| **Model tuning** | Training settings that can be adjusted before retraining: learning rate, epochs, batch size, hidden units, optimizer (Adam or SGD), dropout and weight decay |
| **Results** | 6.0% median prediction error, and the correct pass or fail call for 97.3% of test sessions |

## Problem

In an AI factory environment, AI agents don't just answer prompts; they reason over many turns, call tools, start sub-agents and share hardware with other agents. Each agent action and response affects how fast an agent produces output, measured in tokens per second. In multi-agent workflows, delays compound across steps, stall parent agents, and trigger timeouts and retries, reducing the robustness and efficiency of the whole agent ecosystem.

To run agentic workflows efficiently, operations teams need to know in advance:

- Whether an agent workload will meet its token output rate target
- How many agents a piece of hardware can serve
- Which settings to adjust

## What I built

This simplified neural network takes six workload features (context length, tool calls, sub-agents, concurrent agents, cache hit rate and hardware tier) and predicts throughput in tokens per second. The `predict_tps()` function turns the model into a capacity planning tool: enter the six workload inputs and it returns the predicted speed and whether it meets the target. Running it across different numbers of agents answers questions like *"Based on a specified set of constraints, how many agents can share the same hardware before each agent's throughput falls below 20 tokens/sec?"*

The training data is **simulated**: the notebook's `simulate_sessions()` function uses PyTorch's random number generator to create 5,000 agent sessions from a formula that mimics how agent workloads behave. It adds about 8% random noise to each result so the data resembles real measurements. The focus is to demonstrate the use of PyTorch and a neural network setup process, not real hardware performance.

The model uses three illustrative hardware tiers (small, medium and large), each roughly doubling the base speed of the one below. The 20 tokens/sec target is an example based on published benchmarks. See the [technical notes](TECHNICAL_NOTES.md#simulated-data-and-hardware-tiers) for details.

The README's example compares two workloads:

- **Workload 1:** a coding agent with a long context, one of 32 agents sharing a medium GPU
- **Workload 2:** the same agent, with better cache reuse and less sharing

| Workload input | Workload 1 | Workload 2 |
| --- | --- | --- |
| `context_tokens` | 64,000 | 64,000 |
| `tool_calls` | 8 | 8 |
| `subagents` | 2 | 2 |
| `concurrent_agents` | 32 | **8** |
| `cache_hit_rate` | 0.5 (50%) | **0.9 (90%)** |
| `hardware_tier` | 1 (medium) | 1 (medium) |
| **Predicted speed** | **18.9 tokens/sec (misses target)** | **53.8 tokens/sec (meets target)** |

## Results

On 1,000 test sessions the model had never seen:

| Measure | Result | What it means |
| --- | --- | --- |
| Median prediction error | 6.0% | Half of the predictions were within 6.0% of the actual speed; the rest were further off, up to 47.3% |
| Variation explained (R²) | 0.988 | The model explains about 98.8% of the differences in speed between sessions |
| Correct pass or fail against the 20 tokens/sec target | 97.3% | Correct in 973 of 1,000 cases; most misses were borderline sessions near the target |
| Precision, recall and F1 score for the pass or fail calls | 95.9%, 98.5%, 97.2% | When the model predicts a pass, it is right 95.9% of the time, and it catches 98.5% of sessions that actually pass. Nearly identical scores on the training set show the model is not overfitting |

For a heavier workload (96,000 context tokens, 10 tool calls, 2 sub-agents and 50% cache hits), the model estimates that medium hardware serves up to 19 agents at target speed and large hardware up to 61 agents.

The [technical notes](TECHNICAL_NOTES.md#detailed-test-results) show the full error distribution and explain each measure.

## How it works

1. **Data preparation:** split the data into training and test sets, normalized the inputs, and trained on the logarithm of tokens per second.
2. **Model:** `ThroughputNet`, a custom subclass of PyTorch's `nn.Module` with two hidden layers and 4,673 trainable weights and biases.
3. **Training and evaluation:** a mini-batch training loop with the Adam optimizer, judged only on unseen data.
4. **Tuning experiments:** controlled experiments on learning rate, model size, optimizer choice and overfitting, each changing one setting.
5. **Troubleshooting:** reproduced five common training bugs on purpose and documented each symptom, cause and fix.

See [Model design and training](TECHNICAL_NOTES.md#model-design-and-training) for the reasoning behind each step.

## Documentation

The documentation is layered by audience:

- **This summary:** the project in a few minutes
- **[README](README.md):** a user guide for running the model with different workload inputs, covering setup, a quick start, expected validation results, model tuning, and a troubleshooting table that includes real setup errors I hit while learning
- **[Technical notes](TECHNICAL_NOTES.md):** model design, code structure, a code reference, a project glossary, detailed test results and a production rollout plan

## Next steps

The next phase would be planning how the model fits into a live AI agent ecosystem, where a scheduler calls it automatically: collecting real data, retraining, packaging the model as a service, and rolling it out in stages. See [From notebook to production](TECHNICAL_NOTES.md#from-notebook-to-production) for the seven-stage plan and the documentation each stage needs.

## Author's note

This project was created in collaboration with Anthropic's Claude AI assistant. I defined the project scope and direction, refined the workload inputs and training settings, reviewed the results and reproduced them by running the notebook on my own machine, and revised the text of the summary, README and technical notes. Claude co-wrote the notebook code, including the simulated data formula, and drafted the initial text.

AI-assisted code and content can contain errors or imprecise wording. The results reported here come from running the notebook, and readers can reproduce them by running it themselves. Please verify any detail before relying on it.
