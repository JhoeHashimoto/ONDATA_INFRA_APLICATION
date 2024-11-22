# ONDATA_INFRA_APLICATION
Repositório de Infra da ONDATA

# 🌐 Infraestrutura da aplicação ONDATA

Bem-vindo à infraestrutura da aplicação ONDATA! Este guia fornece instruções para criar recursos no Azure, configurar uma máquina virtual e instalar o Docker e Docker Compose. 🚀

## 📦 Criação de Recursos no Azure

### 🛠️ 1. Criar o Resource Group


```bash
az group create --name ondata-prd --location eastus
```


### 🖥️ 2. Criar a VM 


```bash
az vm create \
  --resource-group rg-sufradev-prd \
  --name vm-sufradev-linux-back-prd \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --admin-username admsufra \
  --admin-password sufra123@2024 \
  --authentication-type password \
  --storage-sku Standard_LRS \
  --os-disk-size-gb 30 \
  --custom-data cloud-init.txt \
  --public-ip-sku Standard \
  --tags Environment=Production
```

```bash
az vm create \
  --resource-group rg-sufradev-prd \
  --name vm-sufradev-windowsserver-front-prd \
  --image MicrosoftWindowsServer:windows-server:2022-datacenter-azure-edition:latest \
  --size Standard_D2s_v5 \
  --admin-username adm-sufra \
  --admin-password sufra123@2024 \
  --public-ip-sku Standard \
  --os-disk-size-gb 128 \
  --authentication-type password

```

```bash
ssh admsufra@191.233.254.131
sufra123@2024
```





```bash
az vm open-port --port 80-100 --resource-group rg-sufradev-prd --name vm-sufradev-windowsserver-front-prd
az vm open-port --port 8080 --resource-group rg-sufradev-prd --name vm-sufradev-linux-back-prd
az vm open-port --port 22 --resource-group rg-sufradev-prd --name vm-sufradev-linux-back-prd
az vm open-port --port 443 --resource-group rg-sufradev-prd --name vm-sufradev-linux-back-prd

```




```bash
sudo apt update && sudo apt install openjdk-17-jdk -y
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64 export PATH=$JAVA_HOME/bin:$PATH
java -version
```



```bash
sudo apt install gradle
gradle wrapper
chmod +x ./gradlew
./gradlew wrapper --gradle-version 8.0
./gradlew clean build

```



```bash
cd /home/admsufra
git clone https://github.com/eduardofuncao/suffra-backend.git
cd suffra-backend
```



```bash
cd /home/admsufra/sufrajava/suffra-backend
 ./gradlew clean build
./gradlew bootRun

cd /home/admsufra/sufrajava/suffra-backend/build/libs
java -jar build/libs/suffra-0.0.1-SNAPSHOT.jar
```



### 🔐 Acesso à VM

```bash
ssh jhanalytics@191.232.243.129
# Senha: Jhanalytics123
```



## 🐳 Instalação do Docker e Docker Compose

### 📥 Baixando e Instalando Docker

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt install docker-ce
sudo systemctl status docker
```

### 📋 Baixando e Instalando Docker Compose

```bash
sudo apt update
sudo apt install -y curl jq
VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)
curl -L "https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

### ✅ Verificando as versões instaladas

```bash
docker --version
docker-compose --version
```

# 📂 Estrutura do Projeto

```bash
/ondata-prd
├── docker-compose.yml
├── java-app-ondata
│   ├── Dockerfile
│   └── my-app.jar  
└── react-native-app-ondata
    ├── Dockerfile
    ├── package.json
    ├── package-lock.json
    └── src
```

### 📁 Criando diretórios e arquivos de configuração

```bash
mkdir ondata-prd
cd ondata-prd

mkdir java-app-ondata
mkdir react-native-app-ondata

touch docker-compose.yml
cd java-app-ondata && touch Dockerfile
cd ../react-native-app-ondata && touch Dockerfile
```

## 🛠️ Buildando os containers

```bash
docker-compose up --build -d
```


## 🗑️ Deletando o Resource Group ❗ 

```bash
az group delete --name ondata-prd --yes --no-wait
```


Desenvolvido por:
Artur Lopes 👨‍💻
Eduardo Função 👨‍💻
Jhoe Hashimoto 👨‍💻

[DEPLOY INFRAESTRUTURA DO PROJETO](https://www.youtube.com/watch?v=q3IbmCpXN0s)
