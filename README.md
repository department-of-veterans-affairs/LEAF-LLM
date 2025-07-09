# LEAF Large Language Model (LLM)

This module provides natural language capability for specific features within [VA LEAF](https://github.com/department-of-veterans-affairs/LEAF), such as automatic categorization of IT issue tickets.

This leverages [llama.cpp](https://github.com/ggml-org/llama.cpp) to implement self-hosted inference tasks with open models such as [Gemma 3](https://huggingface.co/google/gemma-3-4b-it-qat-q4_0-gguf).

## Example Usage
Prerequisites:
- 6GB free RAM
- OCI-compliant container engine such as Docker or Podman

1. Download a compatible model, such as `gemma-3-4b-it-q4_0.gguf` from [Gemma 3](https://huggingface.co/google/gemma-3-4b-it-qat-q4_0-gguf)
2. Navigate to `./docker/cpu` or `./docker/cuda` depending on CUDA-compatible hardware availability
2. Update `./docker/*/docker-compose.yml` with the path to the model.
3. Start the container

To quickly check functionality, navigate to `http://localhost:8012` or the relevant hostname and send a message

## Configuraiton
1. Generate a secure hash, and set the environment variable `LLM_API_KEY`

## Integration with LEAF Agent
LEAF Agent environment variables:
1. `LLM_API_KEY` must match the key generated in this configuration
2. `LLM_CATEGORIZATION_URL` must match the URL of the llama.cpp OpenAI-compatible Chat Completions API endpoint (e.g. `http://localhost:8012/v1/chat/completions`)
