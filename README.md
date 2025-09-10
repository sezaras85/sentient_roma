# Guide: Running Sentient AGI ROMA on a VPS
This guide provides step-by-step instructions on how to set up and run the Sentient AGI ROMA meta-agent framework on a VPS, such as one from Contabo.

# Step 1: Install Dependencies
First, you need to install the essential tools to run ROMA on your VPS. ROMA uses Docker containers, so you must have Docker and Git installed.

# For Ubuntu/Debian Guide: Running Sentient AGI ROMA on a VPS

```Bash
sudo apt update
sudo apt install git docker.io -y
```

# Start the Docker service

```Bash
sudo systemctl start docker
sudo systemctl enable docker
```

# Step 2: Clone the ROMA Repository and Run the Setup
Next, clone the ROMA source code from GitHub and run the setup script.

```Bash

# Clone the repository
git clone https://github.com/sentient-agi/ROMA.git
cd ROMA
```


# Run the setup script

```Bash
./setup.sh
```
The setup script will ask you to choose between Docker Installation and Native Installation. For stability and ease of use, select Docker Installation.

# Step 3: Start Docker Services
Once the setup is complete, you need to start ROMA's Docker containers. The docker-compose.yml file is not in the main directory, but in the docker subdirectory.


# Navigate to the docker directory

```Bash
cd docker
```

# Start the Docker containers in the background

```Bash
docker-compose up -d
```
If this command gives you an address already in use error, it means another application is using a port that ROMA needs. See the Port Troubleshooting section for a solution.

# Step 4: Configure the Firewall
Your VPS's default firewall (e.g., UFW) may block external access to ROMA's web interface. By default, ROMA uses port 3000, so you must open this port.


# Allow incoming connections on  port 3000

```Bash
sudo ufw allow 3000/tcp
```

# Enable the firewall (if it's not already enabled)

```Bash
sudo ufw enable
```

# Step 5: Access and Experience ROMA
Everything should be ready now. Open a web browser and navigate to the following address:

http://<Your_VPS_IP_Address>:3000

If you are installing with your own local PC, just type http://localhost:3000

<img width="915" height="397" alt="roma 3" src="https://github.com/user-attachments/assets/e57441eb-bb83-4822-b9db-654fcacd4967" />



