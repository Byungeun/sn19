# sn19

# 실행 명령어 
docker run -d --name llama3_2_3b \
  --gpus all \
  -e VLLM_LOGGING_LEVEL=DEBUG \
  -v /home/s24-1/models/llama3-2-3b:/model \
  -p 8000:8000 \
  vllm/vllm-openai:latest \
  --model /model \
  --tokenizer unsloth/Llama-3.2-3B-Instruct \
  --served-model-name unsloth/Llama-3.2-3B-Instruct \
  --max-model-len 2048 \
  --gpu-memory-utilization 0.7

docker run -d --name llama3_2_3b \
  --gpus all \
  -e VLLM_LOGGING_LEVEL=DEBUG \
  -v /home/s24-2/models/llama3-2-3b:/model \
  -p 8000:8000 \
  vllm/vllm-openai:latest \
  --model /model \
  --tokenizer unsloth/Llama-3.2-3B-Instruct \
  --served-model-name unsloth/Llama-3.2-3B-Instruct \
  --max-model-len 2048 \
  --gpu-memory-utilization 0.7


# 테스트 명령어 

curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "unsloth/Llama-3.2-3B-Instruct",
    "messages": [{"role": "user", "content": "대한민국의 수도는 어디인가요?"}]
  }'
