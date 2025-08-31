# Self-Hosted GitHub Actions Runner

This repository contains the setup and configuration for a self-hosted GitHub Actions runner.

## Overview

A self-hosted runner is a system that you deploy and manage to execute jobs from GitHub Actions on your own infrastructure. This gives you more control over the hardware, operating system, software, and security tools used in your CI/CD workflows.

## Setup Process

### Prerequisites
- A GitHub repository or organization where you want to add the runner
- Administrative access to the repository/organization
- A machine (physical, virtual, or cloud instance) to host the runner

### Installation Steps

1. **Download the Runner Application**
   ```bash
   # Create a folder for the runner
   mkdir actions-runner && cd actions-runner
   
   # Download the latest runner package
   curl -o actions-runner-linux-x64-2.311.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.311.0/actions-runner-linux-x64-2.311.0.tar.gz
   
   # Extract the installer
   tar xzf ./actions-runner-linux-x64-2.311.0.tar.gz
   ```

2. **Configure the Runner**
   ```bash
   # Create the runner and start the configuration experience
   ./config.sh --url https://github.com/[OWNER]/[REPO] --token [REGISTRATION_TOKEN]
   ```

3. **Start the Runner**
   ```bash
   # Start the runner
   ./run.sh
   ```

### Configuration Options

During the configuration process, you'll be prompted to:
- Provide the repository/organization URL
- Enter the registration token (obtained from GitHub Settings)
- Set a runner name (optional)
- Choose runner labels (optional)
- Set the work folder (default: _work)

### Running as a Service

To run the runner as a background service:

```bash
# Install the service
sudo ./svc.sh install

# Start the service
sudo ./svc.sh start

# Check service status
sudo ./svc.sh status
```

## Security Considerations

- Self-hosted runners should only be used with private repositories
- Ensure the runner machine is properly secured and maintained
- Regularly update the runner software
- Monitor runner activity and logs

## Usage in Workflows

Once configured, you can use your self-hosted runner in workflows by specifying:

```yaml
runs-on: self-hosted
# or
runs-on: [self-hosted, linux, x64]  # with specific labels
```

## Maintenance

- **Updates**: Regularly update the runner application
- **Monitoring**: Monitor system resources and runner logs
- **Cleanup**: Clean up old workflow artifacts and temporary files

## Troubleshooting

- Check runner logs in the `_diag` folder
- Verify network connectivity to GitHub
- Ensure proper permissions for the runner user
- Check system resources (CPU, memory, disk space)