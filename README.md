# Druid Local Standalone Setup on Ubuntu

This README provides step-by-step instructions for setting up Druid in a local standalone mode on an Ubuntu machine. Please ensure you meet the prerequisites before starting.

## Prerequisites

- A machine with a minimum of 5 GB RAM. If using AWS, consider the `t2.large` instance type and allow incoming traffic on port 8888 in the security group.
- Java Development Kit (JDK) is a prerequisite. Install it with the following command:
    
    ```bash
    sudo apt install default-jre

## Setup Instructions

1. Download and extract Druid:

   ```bash
   cd /home/ubuntu/downloads
   wget https://dlcdn.apache.org/druid/27.0.0/apache-druid-27.0.0-bin.tar.gz
   tar -xzf apache-druid-27.0.0-bin.tar.gz

2. Create a systemd service (use ROOT user for this):
   - Create a service file:

     ```bash
     vi /etc/systemd/system/druid.service

   - Paste the text from the [`druid.service`](https://github.com/PavanKumarYarramsetti/druid/blob/main/druid.service) file available in this repository.

   - Reload the systemd manager configuration:

     ```bash
     systemctl daemon-reload

   - Enable the Druid service to start on boot:

     ```bash
     systemctl enable druid

   - Start the Druid service:

     ```bash
     systemctl start druid

3. Check the service status:

   ```bash
   systemctl status druid

The service should be in the active state. Wait for 2-3 minutes.

4. Access the Druid web console @{public-ip}:8888

## Troubleshooting

- If you're getting a connection refused, check the status of the service. There might be some configuration or Druid start-up issues.
- If you're getting a connection timed out, check the security group. You might have missed enabling the 8888 port in the security group.
