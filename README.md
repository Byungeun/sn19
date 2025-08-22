# sn19

# 실행 명령어 
docker run -d --runtime=nvidia --gpus all \
  -v ~/.cache/huggingface:/root/.cache/huggingface \
  -p 8000:8000 \
  --ipc=host \
  -e VLLM_ALLOW_LONG_MAX_MODEL_LEN=1 \
  vllm/vllm-openai:latest \
  --model Qwen/QwQ-32B \
  --served-model-name Qwen/QwQ-32B \
  --max-model-len 131072 \
  --gpu-memory-utilization 0.9 \
  --dtype bfloat16



# 테스트 명령어 

curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "unsloth/Llama-3.2-3B-Instruct",
    "messages": [{"role": "user", "content": "대한민국의 수도는 어디인가요?"}]
  }'
