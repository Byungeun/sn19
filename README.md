# sn19

# 체인 등록
fiber-post-ip --netuid 19 --subtensor.network finney --external_port 4001 --wallet.name testcold --wallet.hotkey testhot --external_ip 160.187.202.151

# 마이너 실행
pm2 start "python3" --name miner -- \
  -m uvicorn miner.server:app \
  --host 0.0.0.0 --port 4001 --log-level debug \
  --env-file .default.env


# 실행 명령어 
docker run -d --runtime=nvidia --gpus all \
  -v ~/.cache/huggingface:/root/.cache/huggingface \
  -p 8000:8000 \
  --ipc=host \
  -e VLLM_ALLOW_LONG_MAX_MODEL_LEN=1 \
  -e VLLM_USE_FLASHINFER=0 \
  vllm/vllm-openai:latest \
  --model Qwen/QwQ-32B \
  --served-model-name Qwen/QwQ-32B \
  --max-model-len 131072 \
  --gpu-memory-utilization 0.9 \
  --dtype bfloat16 \
  --disable-log-requests



