# Custom Chat Template in SGLang Runtime

**NOTE**: There are two chat template systems in SGLang project. This document is about setting a custom chat template for the OpenAI-compatible API server (defined at [conversation.py](../../python/sglang/srt/conversation.py)). It is NOT related to the chat template used in the SGLang language frontend (defined at [chat_template.py](../../python/sglang/lang/chat_template.py)).

By default, the server uses the chat template specified in the model tokenizer from Hugging Face.
It should just work for most official models such as Llama-2/Llama-3.

If needed, you can also override the chat template when launching the server:

```
python -m sglang.launch_server --model-path meta-llama/Llama-2-7b-chat-hf --port 30000 --chat-template llama-2
```

If the chat template you are looking for is missing, you are welcome to contribute it.
Meanwhile, you can also temporarily register your chat template as follows:

```json
{
  "name": "my_model",
  "system": "<|im_start|>system",
  "user": "<|im_start|>user",
  "assistant": "<|im_start|>assistant",
  "sep_style": "CHATML",
  "sep": "<|im_end|>",
  "stop_str": ["<|im_end|>", "<|im_start|>"]
}
```

```
python -m sglang.launch_server --model-path meta-llama/Llama-2-7b-chat-hf --port 30000 --chat-template ./my_model_template.json
```