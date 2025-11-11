
# CodeAssist - AI Programming Assistant

CodeAssist is a completely private and local AI coding assistant, developed by Gensyn. It helps you practice programming problems and train a novel assistant to help you code.

Unlike typical code assistants, CodeAssist writes directly in your editor as you work. Every keystroke - whether you type, fix, delete, or leave its output untouched - becomes a learning signal. Over time, it adapts to your habits and style, acting more like an apprentice learning from your craft than a tool following commands.

[Docs](https://docs.gensyn.ai/testnet/codeassist) | [Tutorial](https://docs.gensyn.ai/testnet/codeassist/using-codeassist) | [Leaderboard](https://dashboard.gensyn.ai/?application=CodeAssist)

# Installation

Get started with installing CodeAssist.

## Install Dependecies
```
sudo apt-get update && sudo apt-get upgrade -y
```

## Docker (if you have already docker ignore this)
```
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Test Docker
sudo docker run hello-world

sudo systemctl enable docker
sudo systemctl restart docker
```

#!/bin/bash
# ==============================
# Gensyn CodeAssist VPS Setup
# ==============================

# Step 1: Create a new screen session
```screen -S codeassist```

# Step 2: Install UV (Python Packager)
```
curl -LsSf https://astral.sh/uv/install.sh
source ~/.bashrc
```

# Step 3: Clone the CodeAssist repository
```git clone https://github.com/gensyn-ai/codeassist.git
cd codeassist
```

# Step 4: Update compose.yml to change host port to 3001
```sed -i 's/3000:3000/3001:3000/' compose.yml```

# Step 5: Update run.py to expose web UI port 3001
```sed -i 's/"3000\/tcp": 3000,/"3000\/tcp": 3001,/' run.py```

# Step 6: Run the program (you will need to paste your Hugging Face token manually)
```uv run run.py```

# Step 7: Instructions for SSH tunnel (run from your LOCAL PC)
- echo "Run this on your LOCAL PC terminal:"
```ssh -L 3001:localhost:3001 -L 8000:localhost:8000 -L 8008:localhost:8008 root@[YOUR_VPS_IP]```

# Step 8: Open Web Interface
echo "Then open in your browser: http://localhost:3001"

# Step 9: To finish & trigger training
echo "After completing tasks in Web UI, return to VPS terminal and press Ctrl+C to start training"




## Formatting

This repository is formatted with `ruff format`. Any commits which do not meet Ruff's lint checks will have GitHub actions fail, and will need to be fixed before merging.

# License

CodeAssist is released under the (MIT) license.
