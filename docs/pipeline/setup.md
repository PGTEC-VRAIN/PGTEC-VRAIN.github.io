# Set up 

This [repository](https://github.com/PGTEC-VRAIN/Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap) provides a complete environment for orchestration and management of IoT data, integrating a set of FIWARE-based components and workflow automation tools.
## Repository Contents

- **docker-compose.yml**: Defines and configures all services and containers within the stack.

- **dags/**: Directory containing Airflow DAGs for automated workflows.

- **Scripts:**
    - **AEMET.py:** Fetches meteorological data from the AEMET API.
    - **Copernicus.py:** Retrieves Copernicus climate datasets for the province of Valencia using Python’s cdsapi library.
    - **Flujo_Copernicus_orion.py:** DAG that collects Copernicus data, registers it in the IoT Agent, and stores it in Orion-LD.
    - **Flujo_copernicus_orion_quantumleap.py:** Enhanced DAG that extends the previous workflow by integrating QuantumLeap for historical data persistence in CrateDB. (Recommended DAG for production use.)

##  **Install the software**
The following commands can be used to install some of the necessary software:
### **Docker**
```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```
### **Docker Compose**
```
sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
### **Clone the repository**
```
git clone https://github.com/PGTEC-VRAIN/Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap.git
cd Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap
```
### **Python (Environment from anaconda / miniconda)**
```
# Download Miniconda installer (Linux x86_64)
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh

# Run the installer
bash ~/miniconda.sh

# Follow the prompts (accept license, choose install path, initialize conda)

# Initialize conda for bash
source ~/.bashrc

# Create a project environment (Python 3.12.3)
conda create -n pgtec_env python=3.12.3 -y
conda activate pgtec_env
```
##  **Setup instructions**

### **Clone the repository**
```
git clone https://github.com/PGTEC-VRAIN/Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap.git
cd Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap
```
### **Start the containers**
```
docker-compose up -d --build
```

- Use --build only if changes were made to the docker-compose.yml.

- The -d option runs services in the background (detached mode).
### **Verify running services**
```
docker ps
```
### **Shut down the environment**

- From a new terminal:
```
docker-compose down
```
- Or interrupt the current process with CTRL + C.