# Infraestrutura - Wordpress

## Descrição do Projeto

Este projeto contém os arquivos Kubernetes que utilizo na minha infraestrutura para subir a aplicação Wordpress.

## Requisitos

Para executar este projeto, é necessário ter os seguintes componentes instalados:

- [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)
- [minikube](https://kubernetes.io/docs/tasks/tools/#minikube)

## Como executar

Para subir esta aplicação, siga os seguintes passos:

### 1. Crie os arquivos de variável de ambiente

Crie o arquivo ```wordpress.env``` através da cópia do arquivo ```wordpress.env.sample```.

E faça o mesmo com o arquivo ```mysql.env``` com a cópia do arquivo ```mysql.env.sample```.

### 2. Altere os valores das variáveis de ambiente

No arquivo ```wordpress.env```, defina o valor da variável ```WORDPRESS_DB_PASSWORD```.

E copie esse valor para a variável ```MYSQL_PASSWORD``` do arquivo ```mysql.env```.

### 3. Inicie o cluster Kubernetes

Para iniciar o cluster Kubernetes, em um Terminal, Prompt de Comando ou PowerShell, execute o seguinte comando:

```shell
minikube start
```

### 4. Suba a aplicação

Para subir a aplicação, em um Terminal, PowerShell ou Prompt de Comando, execute o seguinte comando:

```shell
kubectl apply -k .
```

E a aplicação rodará.

### 5. Descubra o endereço IP e a Porta

#### Endereço IP

Para descobrir o endereço IP onde está rodando a aplicação, em um Terminal, Prompt de Comando ou PowerShell, execute o seguinte comando:

```shell
kubectl get nodes -o wide
```

E será mostrada uma tabela listando os nós Kubernetes.

Exemplo:

```
NAME       STATUS   ROLES           AGE     VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE                         KERNEL-VERSION          CONTAINER-RUNTIME
minikube   Ready    control-plane   6h48m   v1.35.1   192.168.49.2   <none>        Debian GNU/Linux 12 (bookworm)   7.1.5-200.fc44.x86_64   docker://29.2.1
```

Copie o endereço IP mostrado na coluna ```INTERNAL-IP``` da primeira linha. No exemplo mostrado, o endereço IP é ```192.168.49.2```.

#### Porta

Para descobrir a porta sendo utilizada, em um Terminal, Prompt de Comando ou PowerShell, execute o seguinte comando:

```shell
kubectl get service
```

E será mostrada uma tabela listando os serviços Kubernetes.

Exemplo:

```
NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes                   ClusterIP      10.96.0.1        <none>        443/TCP        6h53m
svc-wordpress-loadbalancer   LoadBalancer   10.111.188.214   <pending>     80:31351/TCP   6h53m
wordpress-svc-db             ClusterIP      None             <none>        3306/TCP       6h50m
```

Copie a segunda porta mostrada na coluna ```PORT(S)``` da linha cujo nome é ```svc-wordpress-loadbalancer```. No exemplo mostrado, a porta é ```31351```.

### 6. Abra o Wordpress no navegador web

Em um navegador web, na barra de endereço, digite: ```http://<ENDEREÇO-IP>:<PORTA>``` substitunido ```<ENDEREÇO-IP>``` pelo valor do endereço IP e ```<PORTA>``` pela porta onde está rodando a aplicação. No exemplo mostrado, esse valor seria: ```http://192.168.49.2:31351```.

E será exibida a página de configuração do Wordpress.