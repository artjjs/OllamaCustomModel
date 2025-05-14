# OllamaCustomModel
The process to customize a Ollama model file for super basic settings

First we want to investigate what exactly we can setup about the LLM Infrence process

To startout we have the FROM instruction
  this instruction sets the model to apply the settings to
  Example:
  FROM llama3.2:1b
  Depending on the type of model you are trying to use you need to use the instruction a little diffrent
    for GGUF models taken from huggyface
      FROM ./ollama-model.gguf
    for safetensors model
      FROM <model directory>
After the model to use as the brain we want to start changing settings
  There are a bunch of PARAMETER <parameter> <parametervalue> we can change
  Ref at https://ollama.qubitpi.org/modelfile/
  We can also setup chat templates to constrain how the responce is formatted and how the input get formatted before actually sending it into the inrence process
  We use the model specific template langugage to define the order of information flow
  Here is an example from qwen3
  {{ if .System }}<|im_start|>system
  {{ .System }}<|im_end|>{{ end }}<|im_start|>user
  {{ .Prompt }}<|im_end|>
  <|im_start|>assistant
  As far as I can tell it's going to have the system prompt followed by the user then the assistant responce as the final text
