# tuna-network

Hyperledger Composer network for Tuna tracking

### Environment setup - OS Ubuntu 18.04 LTS
Step 1 - Install Docker, Docker Composer, Hyperledger Composer pre-requisites

    sudo apt update;
    sudo apt install python-dev -y;
    sudo apt install apt-transport-https ca-certificates curl software-properties-common -y;
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -;
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable";
    sudo apt update;
    sudo apt install docker-ce -y;
    sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose;
    sudo chmod +x /usr/local/bin/docker-compose;
    docker-compose --version;
    curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh;
    chmod u+x prereqs-ubuntu.sh;
    ./prereqs-ubuntu.sh;
    
###### All in 1:

    sudo apt update; sudo apt install python-dev -y; sudo apt install apt-transport-https ca-certificates curl software-properties-common -y; curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -; sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"; sudo apt update; sudo apt install docker-ce -y; sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose; sudo chmod +x /usr/local/bin/docker-compose; docker-compose --version; curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh; chmod u+x prereqs-ubuntu.sh; ./prereqs-ubuntu.sh;
    
Step 2 - Install Hyperledger Composer

    npm install -g grpc;
    npm install -g composer-cli;
    npm install -g composer-rest-server;
    npm install -g composer-playground;
    npm install -g yo;
    npm install -g generator-hyperledger-composer;
    mkdir ~/fabric-tools;
    cd ~/fabric-tools;
    curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.zip;
    unzip fabric-dev-servers.zip;
    ./downloadFabric.sh ;
    ./startFabric.sh;
    ./createPeerAdminCard.sh;
    
###### All in 1

    npm install -g grpc; npm install -g composer-cli; npm install -g composer-rest-server; npm install -g composer-playground; npm install -g yo; npm install -g generator-hyperledger-composer; mkdir ~/fabric-tools; cd ~/fabric-tools; curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.zip; unzip fabric-dev-servers.zip; ./downloadFabric.sh ; ./startFabric.sh; ./createPeerAdminCard.sh;
   
Step 3 - Deploy
    
    cd ~/fabric-tools;
    ./teardownFabric.sh;
    ./startFabric.sh;
    ./createPeerAdminCard.sh;
    cd ~/; rm -rf social-feedback;
    git clone -b deploy --single-branch https://github.com/trampn-lifull-tech/social-feedback.git
    cd ~/social-feedback;
    composer archive create -t dir -n .;
    composer network install --card PeerAdmin@hlfv1 --archiveFile tuna-network@0.0.1.bna;
    composer network start --card PeerAdmin@hlfv1 --networkAdmin admin --networkAdminEnrollSecret adminpw --networkName tuna-network --networkVersion 0.0.1;
    composer card import --file admin@tuna-network.card;
    composer network ping --card admin@tuna-network;
    
###### All in 1
     
    cd ~/fabric-tools; ./teardownFabric.sh; ./startFabric.sh; ./createPeerAdminCard.sh; cd ~/; rm -rf social-feedback; git clone -b deploy --single-branch https://github.com/trampn-lifull-tech/social-feedback.git; cd ~/social-feedback; composer archive create -t dir -n .; composer network install --card PeerAdmin@hlfv1 --archiveFile tuna-network@0.0.1.bna; composer network start --card PeerAdmin@hlfv1 --networkAdmin admin --networkAdminEnrollSecret adminpw --networkName tuna-network --networkVersion 0.0.1; composer card import --file admin@tuna-network.card; composer network ping --card admin@tuna-network;
    
START SERVICE
			
    composer-playground;  
    composer-rest-server -c admin@tuna-network -n never -w true;    