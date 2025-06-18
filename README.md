# LEAF Large Language Model (LLM)

This module provides natural language capability for specific features within [VA LEAF](https://github.com/department-of-veterans-affairs/LEAF), such as automatic categorization of IT issue tickets.

This leverages [llama.cpp](https://github.com/ggml-org/llama.cpp) to implement self-hosted inference tasks with open models such as [Gemma 3](https://huggingface.co/google/gemma-3-4b-it-qat-q4_0-gguf).

## Example Usage
Prerequisites:
- 6GB free RAM
- OCI-compliant container engine such as Docker or Podman

1. Download a compatible model, such as `gemma-3-4b-it-q4_0.gguf` from [Gemma 3](https://huggingface.co/google/gemma-3-4b-it-qat-q4_0-gguf)
2. Update the `./docker/docker-compose.yml` file with the path to the model.
3. Start the container

To quickly check functionality, navigate to `http://localhost:8012` or the relevant hostname and send a message

## Integration with LEAF Agent
In the LEAF Agent configuration:
1. `LLM_API_KEY` must match
2. `APP_AGENT_LLM_URL_CATEGORIZATION` must match the URL of the LLM
