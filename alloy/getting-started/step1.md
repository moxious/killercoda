# Installing Alloy

You can install Grafana Alloy as a systemd service on Linux.

## Before you begin

Some Debian-based cloud Virtual Machines don't have GPG installed by default.
To install GPG in your Linux Virtual Machine, run the following command in a terminal window.

```bash
sudo apt install gpg
```{{exec}}

We also need to spin up our local Grafana stack so alloy can write data to it. 

```bash
docker-compose -f /setup/docker-compose.yml up -d
```{{exec}}

## Install

To install Grafana Alloy on Linux, run the following commands in a terminal window.

1. Import the GPG key and add the Grafana package repository.

   ```bash
   sudo mkdir -p /etc/apt/keyrings/ && wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null &&
   echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
   ```{{exec}}

2. Update the repositories.

   ```bash
   sudo apt-get update
   ```{{exec}}

3. Install Grafana Alloy.

   ```bash
   sudo apt-get install alloy
   ```{{exec}}


4. Lastly we need to add a optional flag to `/etc/default/alloy` to run the Alloy UI.

   ```bash
   sed -i -e 's/CUSTOM_ARGS=""/CUSTOM_ARGS="--server.http.listen-addr=0.0.0.0:12345"/' /etc/default/alloy
   ```{{exec}}

5. Start the Grafana Alloy service.

   ```bash
   sudo systemctl start alloy
   ```{{exec}}

6. After starting the Alloy service, we can see the the Alloy UI:
   [http://localhost:12345]({{TRAFFIC_HOST1_12345}})





