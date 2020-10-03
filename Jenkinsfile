node{
   stage('SCM Checkout'){
       git credentialsId: 'git-creds', url: 'https://github.com/devendra-suntechno/vedikaservice.git'
   }
   

     stage('gradle Package'){
   def gradleHome = tool name: 'gradle', type: 'gradle'
     def gradleCMD = "${gradleHome}/bin/gradle"
     sh "${gradleCMD} clean build -x test" 
   } 
   
   stage('connecting to anspip server'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo chmod 777 /opt
    ssh ubuntu@172.31.41.54 sudo chmod 777 /opt
    ssh ubuntu@172.31.41.54 sudo mkdir -p $HOME/.kube'''
}
   
    stage('connecting to anspip server'){
    sh label: '', script: '''scp /var/lib/jenkins/workspace/vedikapipeline/build/libs/functionhall-service-0.0.1-SNAPSHOT.war ubuntu@172.31.13.69:/opt'''
}

    stage('connecting to anspip server'){
    sh label: '', script: '''sudo chmod 777 /opt
    sudo echo "echo Installing software-properties-common packages, then add the java OpenJDK PPA repository.
   sudo apt install software-properties-common apt-transport-https -y
   sudo add-apt-repository ppa:openjdk-r/ppa -y
   Now installing the Java 8 using apt command.
   sudo apt install openjdk-8-jdk -y
   echo java version installed on the system.
   java -version
   echo updating and upgrading the version
   sudo apt-get update -y
   sudo apt-get upgrade -y
   echo Ansible PPA to your server
   sudo apt-add-repository ppa:ansible/ansible \' \'
   echo update the repository and install Ansible
   sudo apt-get update -y
   sudo apt-get install ansible -y
   echo Ansible version
   sudo ansible --version" > /opt/ansibleinstallation.sh'''
}

stage('copying ansibleinstallation.sh'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo chmod 777 /opt
    scp /opt/ansibleinstallation.sh ubuntu@172.31.13.69:/opt'''
}
stage('executing ansibleinstallation script'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sh /opt/ansibleinstallation.sh'''
  }

stage('executing ansibleinstallation script'){
sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo rm -Rf /etc/ansible/hosts
sudo echo "172.31.1.232" > /opt/hosts
sudo echo "172.31.41.54" >> /opt/hosts
sudo echo "172.31.44.159" >> /opt/hosts
sudo chmod 777 /etc/ansible
scp /opt/hosts ssh ubuntu@172.31.13.69:/etc/ansible'''
}

stage('docker installation'){
    sh label: '', script: '''sudo echo "sudo chmod 777 /opt
   #!/bin/bash
sudo apt update -y
sudo apt upgrade -y
sudo apt-get install curl apt-transport-https ca-certificates software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update -y
apt-cache policy docker-ce
sudo apt install docker-ce
sudo sudo mkdir /opt/Mydockerfile
sudo chmod 777 /opt/Mydockerfile
cd /opt/Mydockerfile
sudo mv /opt/functionhall-service-0.0.1-SNAPSHOT.war /opt/Mydockerfile" > /opt/dockerinstallation.sh'''
}

stage('copying dockerinstallation.sh.sh'){
    sh label: '', script: '''scp /opt/dockerinstallation.sh ubuntu@172.31.13.69:/opt'''
}

stage('service Dokerfile'){
    sh label: '', script: '''sudo echo "FROM java:8-jdk-alpine
COPY ./functionhall-service-0.0.1-SNAPSHOT.war /usr/app/
WORKDIR /usr/app
EXPOSE 8057
ENTRYPOINT ["java", "-jar", "functionhall-service-0.0.1-SNAPSHOT.war"]" > /opt/Dockerfile'''
}

stage('copying Dockerfile'){
    sh label: '', script: '''scp /opt/Dockerfile ubuntu@172.31.13.69:/opt'''
  }

stage('docker hub pushing'){
    sh label: '', script: '''sudo echo "sudo mv /opt/Dockerfile /opt/Mydockerfile
cd /opt/Mydockerfile
sudo docker build -t vedikaservicecicd .
sudo chmod 666 /var/run/docker.sock
sudo docker tag vedikaservicecicd deva9017/vedikaservicecicd
sudo docker push deva9017/vedikaservicecicd" > /opt/dockerservicepush.sh'''
}

stage('copying dockerservicepush.sh'){
    sh label: '', script: '''scp /opt/dockerservicepush.sh ubuntu@172.31.13.69:/opt'''
}

stage('angular docker code'){
    sh label: '', script: '''sudo echo "FROM ubuntu
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install git -y
RUN apt-get install sudo -y
RUN sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
RUN sudo curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
RUN sudo apt -y install nodejs
RUN sudo apt -y  install gcc g++ make
RUN sudo npm install -g @angular/cli
RUN cd /opt
RUN sudo git init
RUN sudo git clone https://github.com/shivastunts0327/vedikauipipeline.git
RUN cd vedikauipipeline
RUN npm install
WORKDIR /opt/vedikauipipeline
ENTRYPOINT ["ng", "serve", "--host", "0.0.0.0"]" > /opt/ang'''
}

stage('angulardockerfile'){
    sh label: '', script: '''scp /opt/ang ubuntu@172.31.13.69:/opt'''
}


stage('angular docker push'){
    sh label: '', script: '''sudo echo "cd /opt/angulardocker/Mydockerfile
    sudo docker build -t vedikauipipelinecicd .
sudo docker tag vedikauipipelinecicd deva9017/vedikauipipelinecicd
sudo docker push deva9017/vedikauipipelinecicd" > /opt/dockeruipush.sh'''
}

stage('dockeruipush.sh'){
    sh label: '', script: '''scp /opt/dockeruipush.sh ubuntu@172.31.13.69:/opt'''
}
stage('kubernetes installating'){
    sh label: '', script: '''sudo echo "sudo apt update
sudo apt upgrade
sudo apt-get install curl apt-transport-https ca-certificates software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update -y
apt-cache policy docker-ce
sudo apt install docker-ce
systemctl start docker
systemctl enable docker
echo Download the latest release with the command:
sudo curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
echo To install k8 version v1.18.0 on Linux, type:
sudo curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl
echo Make the kubectl binary executable.
sudo chmod +x ./kubectl
echo Move the binary in to your PATH.
sudo mv ./kubectl /usr/local/bin/kubectl
echo Test to ensure the version you installed is up-to-date:
sudo kubectl version --client
echo Install using native package management
sudo apt-get update && sudo apt-get install -y apt-transport-https gnupg2
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
echo Add Kubernetes Signing Key
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
echo If you get an error that curl is not installed, install it with:
sudo apt-get install curl
echo Then repeat the previous command to install the signing keys. Repeat for each server node.
echo Add Software Repositories
echo Kubernetes is not included in the default repositories. To add them, enter the following
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
echo Kubernetes Installation Tools
echo Install Kubernetes tools with the command
sudo apt-get install kubeadm kubelet kubectl kubernetes-cni -y
sudo apt-mark hold kubeadm kubelet kubectl
echo Verify the installation with
sudo kubeadm version
sudo apt upgrade -y
sudo apt update -y" > /opt/kubernetesinstallation.sh'''
}

stage('copying kubernetesinstallation.sh'){
    sh label: '', script: '''scp /opt/kubernetesinstallation.sh ubuntu@172.31.13.69:/opt'''
}

stage('vedika yaml'){
    sh label: '', script: '''sudo echo "apiVersion: apps/v1
kind: Deployment
metadata:
  name: vedika-deployment
spec:
  selector:
    matchLabels:
      app: vedika-deployment
  replicas: 2
  template:
    metadata:
      labels:
        app: vedika-deployment
    spec:
     containers:
     - name: vedikaservice-java
       image: deva9017/vedikaservicecicd
       ports:
       - containerPort: 8057
     - name: vedikauipipeline-angular
       image: deva9017/vedikauipipelinecicd
       ports:
       - containerPort: 4200" > /opt/vedika.yaml'''
}

stage('copying vedika.yaml'){
    sh label: '', script: '''scp /opt/vedika.yaml ubuntu@172.31.13.69:/opt'''
}


    stage('dockernode yaml'){
    sh label: '', script: '''sudo echo "---
-
  hosts: 172.31.1.232
  tasks:
    vars:
    ansible_python_interpreter: /usr/bin/python3
  tasks:  
    - debug: var=ansible_host
   
    -
       shell: sudo chmod 777 /opt
    -
      copy:
        src:  /opt/functionhall-service-0.0.1-SNAPSHOT.war
        dest: /opt
    -
      copy:
        src:  /opt/dockerinstallation.sh
        dest: /opt
    -
       shell: sh /opt/dockerinstallation.sh 
    -
      copy:
        src:  /opt/Dockerfile
        dest: /opt/Mydockerfile
    -
       shell: sudo docker login -u deva9017 -p 9700939598dD@
    -
      copy:
        src:  /opt/dockerservicepush.sh
        dest: /opt
    -
       shell: sh /opt/dockerservicepush.sh
    -
       shell: sudo mkdir /opt/angulardocker
    -
       shell: sudo chmod 777 /opt/angulardocker
    -
       shell: sudo mkdir /opt/angulardocker/Mydockerfile
    -
       shell: sudo chmod 777 /opt/angulardocker/Mydockerfile
    -
       shell: sudo swapoff -a
    -
       shell: sed -i '/ swap / s/^/#/' /etc/fstab
    -
       shell: sudo echo 1 > /proc/sys/net/ipv4/ip_forward
    -
      copy:
        src:  /opt/ang
        dest: /opt
    -
       shell: mv /opt/ang /opt/angulardocker/Mydockerfile
    -
       shell: mv /opt/angulardocker/Mydockerfile/ang /opt/angulardocker/Mydockerfile/Dockerfile
    -
      copy:
        src:  /opt/dockeruipush.sh
        dest: /opt
    -
       shell: sh /opt/dockeruipush.sh" > /opt/dockernode.yaml'''
}

stage('kubernetes node yaml'){
    sh label: '', script: '''cd /opt
cat >kubernetesnode.yaml <<'EOF'
---
-
  hosts: 172.31.41.54
  tasks:
    vars:
    ansible_python_interpreter: /usr/bin/python3
  tasks:  
    - debug: var=ansible_host
   
    -
       shell: sudo chmod 777 /opt
    -
      copy:
        src:  /opt/kubernetesinstallation.sh
        dest: /opt
    -
       shell: sudo sh /opt/kubernetesinstallation.sh
    -
       shell: sudo kubeadm init --pod-network-cidr=10.244.0.0/16 > /opt/kubeadmtoken.sh
    -
      copy:
        src:  /opt/kubeconfig.sh
        dest: /opt
    -
       shell: sh /opt/kubeconfig.sh
    -
       shell: sudo awk 'NR>=66 && NR<=67' /opt/kubeadmtoken.sh > /opt/kubeadmtokenedit.sh
    -
       shell: sudo sed -i '1s/^/sudo /' /opt/kubeadmtokenedit.sh
    -
       shell: sudo swapoff -a
    -
       shell: sed -i '/ swap / s/^/#/' /etc/fstab
    -
       shell: sudo echo 1 > /proc/sys/net/ipv4/ip_forward
    -
      copy:
        src:  /opt/vedika.yaml
        dest: /opt'''
       }

stage('kubernetes node yaml'){
    sh label: '', script: '''sudo echo "---
-
  hosts: 172.31.44.159
  tasks:
    vars:
    ansible_python_interpreter: /usr/bin/python3
  tasks:  
    - debug: var=ansible_host
    -
       shell: sudo chmod 777 /opt
    -
      copy:
        src:  /opt/kubernetesinstallation.sh
        dest: /opt
    -
       shell: sudo sh /opt/kubernetesinstallation.sh
    -
      copy:
        src:  /opt/kubeadmtokenedit.sh
        dest: /opt
    -
       shell: sudo sh /opt/kubeadmtokenedit.sh" > /opt/kubenodepipe.yaml'''
       }
       
       
       stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''cd /opt
    cat >kubefannels.sh <<'EOF'
   #!/bin/bash
    sudo kubectl apply -f https://docs.projectcalico.org/v2.6/getting-started/kubernetes/installation/hosted/kubeadm/1.6/calico.yaml
    sudo kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
    sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
    sudo kubectl create -f /opt/vedika.yaml'''
    }
    
    stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''cd /opt
    cat >kubeconfig.sh <<'EOF'
   #!/bin/bash
  mkdir -p $HOME/.kube   
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config   
sudo chown $(id -u):$(id -g) $HOME/.kube/config'''
 }
 
 stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''scp /opt/kubeconfig.sh ubuntu@172.31.13.69:/opt'''
    }
 
    stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''scp /opt/kubefannels.sh ubuntu@172.31.13.69:/opt'''
    }
       
       stage('kubernetes node yaml'){
    sh label: '', script: '''sudo echo "---
-
  hosts: 172.31.41.54
  tasks:
    vars:
    ansible_python_interpreter: /usr/bin/python3
  tasks:  
    - debug: var=ansible_host

    -
      copy:
        src:  /opt/kubefannels.sh
        dest: /opt
    -
       shell: sh /opt/kubefannels.sh" > /opt/fannels.yaml'''
   }
    
    
    stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''scp /opt/fannels.yaml ubuntu@172.31.13.69:/opt'''
  }
       
    stage('copying dockernode.yaml'){
    sh label: '', script: '''scp /opt/dockernode.yaml ubuntu@172.31.13.69:/opt'''
}

stage('connecting to anspip server'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo ansible-playbook /opt/dockernode.yaml'''
}

stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''scp /opt/kubernetesnode.yaml ubuntu@172.31.13.69:/opt'''
  }
  
  stage('copying kubernetesnode.yaml'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo ansible-playbook /opt/kubernetesnode.yaml'''
  }


  stage('connecting to anspip server'){
    sh label: '', script: '''scp -r ubuntu@172.31.1.232:/opt/kubeadmtokenedit.sh /opt'''
    }    
    
  stage('connecting to anspip server'){
    sh label: '', script: '''scp /opt/kubeadmtokenedit.sh ubuntu@172.31.13.69:/opt'''
}

    stage('connecting to anspip server'){
    sh label: '', script: '''scp /opt/kubenodepipe.yaml ubuntu@172.31.13.69:/opt'''
}

stage('connecting to anspip server'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo ansible-playbook /opt/kubenodepipe.yaml'''
try {
  sh "..."
} catch (err) {
  echo "something failed"
}

}

stage('connecting to anspip server'){
    sh label: '', script: '''ssh ubuntu@172.31.13.69 sudo ansible-playbook /opt/fannels.yaml'''
try {
  sh "..."
} catch (err) {
  echo "something failed"
}
}

stage('webhooks testing'){
    sh label: '', script: '''sudo apt-get update'''
}

}
