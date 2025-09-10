# Guide: Running Sentient AGI ROMA on a VPS
This guide provides step-by-step instructions on how to set up and run the Sentient AGI ROMA meta-agent framework on a VPS, such as one from Contabo.

# Step 1: Install Dependencies
First, you need to install the essential tools to run ROMA on your VPS. ROMA uses Docker containers, so you must have Docker and Git installed.

'''Bash

# For Ubuntu/Debian Guide: Running Sentient AGI ROMA on a VPS
sudo apt update
sudo apt install git docker.io -y
'''

# Start the Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add your user to the docker group (optional but recommended)
sudo usermod -aG docker $USER
If you used the usermod command, close your current SSH session and reconnect for the changes to take effect.

Step 2: Clone the ROMA Repository and Run the Setup
Next, clone the ROMA source code from GitHub and run the setup script.

Bash

# Clone the repository
git clone https://github.com/sentient-agi/ROMA.git
cd ROMA

# Run the setup script
./setup.sh
The setup script will ask you to choose between Docker Installation and Native Installation. For stability and ease of use, select Docker Installation.

Step 3: Start Docker Services
Once the setup is complete, you need to start ROMA's Docker containers. The docker-compose.yml file is not in the main directory, but in the docker subdirectory.

Bash

# Navigate to the docker directory
cd docker

# Start the Docker containers in the background
docker-compose up -d
If this command gives you an address already in use error, it means another application is using a port that ROMA needs. See the Port Troubleshooting section for a solution.

Step 4: Configure the Firewall
Your VPS's default firewall (e.g., UFW) may block external access to ROMA's web interface. By default, ROMA uses port 3000, so you must open this port.

Bash

# Allow incoming connections on  port 3000
sudo ufw allow 3000/tcp

# Enable the firewall (if it's not already enabled)
sudo ufw enable
Step 5: Access and Experience ROMA
Everything should be ready now! Open a web browser and navigate to the following address:

http://<Your_VPS_IP_Address>:3000

The first time you access the page, you'll be prompted to enter your OpenAI API key. Once you've entered the key, the ROMA dashboard will load, and you can start experimenting with the "New Goal" section.

Troubleshooting
Port Troubleshooting
If you get a port error when running docker-compose up -d, you can change the port number by editing the docker-compose.yml file.

Bash

# Make sure you are in the docker directory
nano docker-compose.yml
Find the sentient-frontend section and change the ports line to use a different port (e.g., 3001).

YAML

sentient-frontend:
    # ...
    ports:
      - "3001:3000"  # We changed the port here
    # ...
Save the file (Ctrl+O, then Enter) and exit (Ctrl+X). Then, restart the Docker services. You can now access ROMA at your new port: http://<VPS_IP>:3001.
