
```sh
#!/bin/bash

# Update packages and install necessary dependencies
sudo yum update -y
sudo yum install -y wget tar

# Fetch the latest K9s version
K9S_VERSION=$(curl -s https://api.github.com/repos/derailed/k9s/releases/latest | grep tag_name | cut -d '"' -f 4)

# Download the latest K9s release
wget https://github.com/derailed/k9s/releases/download/${K9S_VERSION}/k9s_Linux_amd64.tar.gz

# Check if the download was successful
if [ $? -ne 0 ]; then
  echo "Failed to download K9s. Please check the version number and URL."
  exit 1
fi

# Extract the tarball and move the binary to /usr/local/bin
tar -xzf k9s_Linux_amd64.tar.gz
sudo mv k9s /usr/local/bin/

# Clean up
rm k9s_Linux_amd64.tar.gz

# Verify installation
k9s version
```

### Usage

1. Save the script to a file, e.g., `install_k9s.sh`.
2. Make the script executable:
   ```sh
   chmod +x install_k9s.sh
   ```
3. Run the script:
   ```sh
   sh install_k9s.sh
   ```

This script includes error handling for the download step to ensure that the script exits gracefully if the download fails.
