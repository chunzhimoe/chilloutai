FROM runpod/stable-diffusion:web-automatic-1.5.16

SHELL ["/bin/bash", "-c"]

ENV PATH="${PATH}:/workspace/stable-diffusion-webui/venv/bin"

WORKDIR /

# 下载模型文
RUN mkdir -p /workspace/stable-diffusion-webui/models/Lora && \
    wget -O /workspace/stable-diffusion-webui/models/Lora/Moxin_1010.safetensors https://civitai.com/api/download/models/17518 && \
    wget -O /workspace/stable-diffusion-webui/models/basemodel.safetensors https://civitai.com/api/download/models/106289

RUN rm /workspace/v1-5-pruned-emaonly.ckpt

ADD relauncher.py .
ADD webui-user.sh .
ADD start.sh /start.sh
RUN chmod a+x /start.sh

SHELL ["/bin/bash", "--login", "-c"]
CMD [ "/start.sh" ]
