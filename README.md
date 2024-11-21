# llm_setting

## Ollama Installation

### Linux

Download and extract the package:

```shell
curl -L https://ollama.com/download/ollama-linux-amd64.tgz -o ollama-linux-amd64.tgz
sudo tar -C /usr -xzf ollama-linux-amd64.tgz
```

Start Ollama:

```shell
ollama serve
```

In another terminal, verify that Ollama is running:

```shell
ollama -v
```


### Adding Ollama as a startup service (recommended)

Create a user and group for Ollama:

```shell
sudo useradd -r -s /bin/false -U -m -d /usr/share/ollama ollama
sudo usermod -a -G ollama $(whoami)
```

Create a service file in `/etc/systemd/system/ollama.service`:

```ini
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="PATH=$PATH"

[Install]
WantedBy=default.target
```

Then start the service:

```shell
sudo systemctl daemon-reload
sudo systemctl enable ollama
```

### Install CUDA drivers (optional)

[Download and install](https://developer.nvidia.com/cuda-downloads) CUDA.

Verify that the drivers are installed by running the following command, which should print details about your GPU:

```shell
nvidia-smi
```


## Download Models from huggingface
I choosed llama3.2-3B
https://huggingface.co/meta-llama/Llama-3.2-3B



