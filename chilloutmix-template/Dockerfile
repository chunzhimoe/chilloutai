FROM runpod/stable-diffusion:web-automatic-1.5.16

SHELL ["/bin/bash", "-c"]

ENV PATH="${PATH}:/workspace/stable-diffusion-webui/venv/bin"

WORKDIR /

RUN rm /workspace/v1-5-pruned-emaonly.ckpt

# 安装wget并下载模型
RUN apk add --no-cache wget && \
    # 下载基础模型到Stable-diffusion目录
    wget -q -O /workspace/stable-diffusion-webui/models/Stable-diffusion/chilloutmix.safetensors https://civitai.com/api/download/models/11745?type=Model&format=SafeTensor&size=full&fp=fp16 && \
    # 下载Lora模型 (替换YOUR_LORA_ID为实际的模型ID)
    wget -q -O /workspace/stable-diffusion-webui/models/Lora/hanguo.safetensors https://civitai.com/api/download/models/31284?type=Model&format=SafeTensor&size=full&fp=fp16 && \
    wget -q -O /workspace/stable-diffusion-webui/models/Lora/riben.safetensors https://civitai.com/api/download/models/34562?type=Model&format=SafeTensor&size=full&fp=fp16 && \
    wget -q -O /workspace/stable-diffusion-webui/models/Lora/taiwan.safetensors https://civitai.com/api/download/models/52974?type=Model&format=SafeTensor && \
    wget -q -O /workspace/stable-diffusion-webui/models/Lora/zhongguo.safetensors https://civitai.com/api/download/models/66172?type=Model&format=SafeTensor 


RUN pip install -U xformers
RUN pip install runpod

ADD webui.py /workspace/stable-diffusion-webui/webui.py
ADD handler.py .
ADD start.sh /start.sh
RUN chmod +x /start.sh


SHELL ["/bin/bash", "--login", "-c"]
CMD [ "/start.sh" ]
