# Deploying Ollama with Docker on Linux

## Prerequisites 📋
- Linux operating system
- Docker installed and running
- Git (optional, for cloning the repository)
- Basic knowledge of Docker commands

## Step 1: Install Docker (if not already installed) ⚙️

```bash
# Update package lists
sudo apt-get update

# Install required packages
sudo apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set up the stable repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt-get update
sudo apt-get install -y docker-ce docker-ce-cli containerd.io

# Verify Docker installation
sudo docker run hello-world
```

## Step 2: Pull and Run Ollama Docker Image 📥

```bash
# Pull the official Ollama Docker image
docker pull ollama/ollama

# Create a directory for Ollama data persistence
mkdir -p ~/.ollama

# Run Ollama container
docker run -d \
  --restart=always \
  --name ollama \
  -p 11434:11434 \
  -v ~/.ollama:/root/.ollama \
  ollama/ollama
```

## Step 3: Verify Ollama Installation ✅

```bash
# Check if the container is running
docker ps | grep ollama

# Check API port is listenning.
netstat -tlpn | grep 11434

# Check logs of it(If required)
docker logs ollama -f

# Test Ollama by pulling and running a model
docker exec -it ollama ollama pull llama2
```

## Step 4: Using Ollama 🛠️

### Basic Usage
```bash
# List installed ollama models
docker exec -it ollama ollama list

# Pull a model
docker exec -it ollama ollama pull <model-name>
# Example:
docker exec -it ollama ollama pull llama3.2:3b

# Run a model
docker exec -it ollama ollama run <model-name>
Example:
docker exec -it ollama ollama run llama3.2:3b
```

### Common Models 🧠
- llama2
- mistral
- codellama
- gemma

<a href="https://ollama.com/library" target="_blank">Model Reference:</a>

## Step 5: Managing the Container 🛑

```bash
# Stop the container
docker stop ollama

# Start the container
docker start ollama

# Remove the container
docker rm ollama

# View logs
docker logs ollama
```

## Step 6: Optional - Test API 🖥️

```bash
# Check llama status frm browser
http://YOUR_IP:11434/

# Get some answer in chunk using curl command to test it.
curl http://localhost:11434/api/generate -d '{"model": "llama3.2", "prompt": "Why is the sky blue?", "stream": false}'

# Ollama API Guide
https://github.com/ollama/ollama/blob/main/docs/api.md

```

## Step 7: Setup Openwebui to access Ollama. 🌐
##### Change "YOUR_IP" to your private IP of host in below command then run.

```bash
docker run -itd \
  --restart always \
  --name open-webui \
  -p 8080:8080 \
  -v open-webui:/app/backend/data \
  -e OLLAMA_BASE_URL=http://YOUR_IP:11434 \
  ghcr.io/open-webui/open-webui:main

```

```bash
# Verify webui is running
docker ps

# Check logs and wait for finish deployment.
docker logs open-webui -f
```

**Note:** ⏳ Please wait for 2-5 minutes to download the latest update.

```bash
# Create Account in webui
http://YOUR_IP:8080/

# Settings available on
http://YOUR_IP:8080/admin/settings
```
## Troubleshooting 🛠️

### Common Issues ⚠️
1. **Port Conflict**: If port 11434 is already in use, change the port mapping in the docker run command.
2. **Permission Issues**: If you encounter permission issues, try running with sudo or add your user to the docker group:
   ```bash
   sudo usermod -aG docker $USER
   ```
3. **Storage Issues**: If you run out of space, check the ~/.ollama directory and clean up unused models.

### Checking Container Status 📊
```bash
# Check container logs
docker logs ollama

# Check container status
docker inspect ollama
```

## Security Considerations 🔒
1. By default, Ollama is accessible on port 11434. Consider using a firewall to restrict access.
2. The container runs with root privileges. For production use, consider implementing additional security measures.
3. Regularly update the Docker image to get security patches:
   ```bash
   docker pull ollama/ollama:latest
   ```

## Additional Resources 📚
- [Ollama Documentation](https://ollama.ai/docs)
- [Docker Documentation](https://docs.docker.com)
- [Ollama GitHub Repository](https://github.com/ollama/ollama)
- [Ollama Dockerhub Repository](https://hub.docker.com/r/ollama/ollama)
- [Ollama Library](https://ollama.com/library)
- [Ollama API](https://github.com/ollama/ollama/blob/main/docs/api.md)


---
### 💼 Connect with me 👇👇 😊

- 🔥 [**Youtube**](https://www.youtube.com/@DevOpsinAction?sub_confirmation=1)
- ✍ [**Blog**](https://ibraransari.blogspot.com/)
- 💼 [**LinkedIn**](https://www.linkedin.com/in/ansariibrar/)
- 👨‍💻 [**Github**](https://github.com/meibraransari?tab=repositories)
- 💬 [**Telegram**](https://t.me/DevOpsinActionTelegram)
- 🐳 [**Docker**](https://hub.docker.com/u/ibraransaridocker)
