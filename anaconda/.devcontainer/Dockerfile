FROM ubuntu:24.04

ARG ANACONDA_FILE_NAME=Anaconda3-2024.02-1-Linux-x86_64.sh
ARG PYTHON_VERSION=3.11

RUN apt update && \
    apt install wget git -y && \
    wget https://repo.anaconda.com/archive/${ANACONDA_FILE_NAME} && \
    bash ${ANACONDA_FILE_NAME} -b && \
    rm ${ANACONDA_FILE_NAME} && \
    apt clean && rm -rf /var/lib/apt/lists/*

# condaコマンドを使用するためにパスを通す(このコマンドはDockerfile内でのみ有効)
# ログイン時に適用されるパス設定は`conda`コマンドを用いた初期化処理で実施される
ENV PATH /root/anaconda3/bin:$PATH

# condaの初期化
RUN conda create -n pythonenv python=${PYTHON_VERSION} -y
RUN conda init

# 起動時に仮想環境を有効化
RUN echo "conda activate pythonenv" >> ~/.bashrc

# Jupyter Notebookが利用できるようにパッケージをインストール
RUN conda install -n pythonenv ipykernel --update-deps --force-reinstall -y
