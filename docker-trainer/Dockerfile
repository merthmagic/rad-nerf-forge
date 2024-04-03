# Use nvidia/cuda as the base image
FROM nvidia/cuda:11.7.1-devel-ubuntu22.04

# Replace the Ubuntu software source with Aliyun's mirror, and install necessary packages
RUN sed -i 's/http:\/\/archive.ubuntu.com/https:\/\/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    apt-get update && \
    apt-get install -y python3.10 python3-pip wget portaudio19-dev ffmpeg git vim && \
    ln -s /usr/bin/python3 /usr/bin/python

# Set pip to use Aliyun's Python package index, and install base and additional modules
RUN pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/ && \
    pip install edge-tts PyMCubes imageio[ffmpeg] torch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 torch-ema && \
    pip install numpy~=1.26.0 pyaudio~=0.2.13 soundfile~=0.12.1 resampy~=0.4.2 transformers~=4.32.1 requests~=2.31.0 scipy~=1.11.3 tqdm~=4.65.0 tensorboardx~=2.6.2.2 pandas~=2.1.1 opencv-python~=4.8.1.78 matplotlib~=3.8.1 trimesh~=4.0.2 imageio~=2.31.6 lpips~=0.1.4 rich~=13.6.0 packaging~=23.1 pillow~=10.0.1 setuptools~=68.0.0 jinja2~=3.1.2 pyyaml~=6.0.1 tabulate~=0.9.0 loguru~=0.7.2 pydub~=0.25.1 flask~=2.2.2 websockets flask-sock dynaconf~=3.2.4 torchvision~=0.15.2 nbformat~=5.9.2 beautifulsoup4~=4.12.2 nbconvert~=7.10.0 gradio~=4.18.0

# Copy local wheel packages to the container and install them
COPY ./wheels /wheels
WORKDIR /wheels
RUN pip install *.whl 

# Set the command to be executed when the container starts
CMD ["bash"]