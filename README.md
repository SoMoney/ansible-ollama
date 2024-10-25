# Ansible-Ollama: An Ansible deployed AI Stack: Ollama, OpenWebUI, and NGINX in Docker

This Ansible role automates the installation and configuration of Docker, NVIDIA container toolkit, Ollama LLM WebUI, Open-WebUI with CUDA support, and Nginx reverse proxy. It includes GPU detection, Docker container management, and SSL configuration for the Nginx reverse proxy to expose the WebUIs securely.

When complete, you should be able to reach the OpenWebUI interface with `https://IP.ADDRESS.HERE`.

## Requirements

- Ubuntu (or a compatible distribution)
- NVIDIA GPU
- Ansible with `community.docker` collection

## Installation

To install a basic Ansible distribution with the `community.docker` module from which to install the project:

```bash
cd ~
apt install pipx
pipx install --include-deps ansible
ansible-galaxy collection install community.docker
```

## Configuration

The Ansible `./inventory` file assumes the server is called "docker-server". If you want to continue using that alias, you will need to edit your Ansible server's `/etc/hosts` file so it's reachable.

Example:

```bash
sudo vi /etc/hosts
# IP to openWebUI alias on Ansible server
192.168.x.x ai docker-server
```

## Models

Popular models can be configured in `vars/main.yml`. Uncomment the models you want to run or add new ones:

Example:
```yaml
ollama_models:
  - ollama run llama3.1
  - ollama run dolphin-llama3
  # Add more models as needed
```

## Run the Playbook

To deploy the setup, run the following command:

```bash
ansible-playbook -i inventory playbook.yml
```

## Handlers

The role includes handlers to restart Docker and Nginx containers:

- `Restart_Docker`: Restarts the Docker service.
- `Restart Nginx container`: Restarts the Nginx container.

## Task Summary

The main tasks performed by this role include:

1. Adding Docker GPG key and repository.
2. Installing required Ubuntu packages.
3. Setting up NVIDIA GPU support if detected.
4. Downloading and verifying Docker Compose.
5. Ensuring required directories exist.
6. Generating self-signed SSL certificates for Nginx.
7. Copying Nginx and Docker Compose configuration files.
8. Deploying the Docker Compose stack.
9. Waiting for services to start.
10. Installing LLMs into the Ollama container if specified (no models loaded by default)

## License

This project is licensed under the MIT License.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss any changes.

## Acknowledgments

Special thanks to the contributors and the open-source community for their support.

---
