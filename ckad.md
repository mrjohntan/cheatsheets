# Setup Bash

source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc # add autocomplete to bash shell

echo "alias k=kubectl" >> ~/.bashrc
echo "complete -F __start_kubectl k" >> ~/.bashrc