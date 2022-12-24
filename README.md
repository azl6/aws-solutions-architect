Este README se refere **exclusivamente** a atividades de hands-on. Para informações teóricas, refira-se aos demais arquivos do repositório.

[General info](#general-info) <br>

**IAM**

[Criando usuários IAM](#criando-usuários-iam) <br>
[Aplicação de IAM policies](#aplicação-de-iam-policies) <br>
[Estrutura de uma IAM policy](#estrutura-de-uma-iam-policy) <br>
[Utilizando o AWS Policy Generator](#utilizando-o-aws-policy-generator) <br>
[Password Policy](#password-policy) <br>
[MFA device types](#mfa-device-types) <br>
[IAM Roles](#iam-roles) <br>
[Credentials Report](#credentials-report) <br>
[Access Advisor](#access-advisor) <br>
[Permissão na página de billing para IAM users](#permissão-na-página-de-billing-para-iam-users) <br>

**Billing**

[Criação de budgets](#criação-de-budgets) <br>

**AMI**

[Criando uma AMI](#criando-uma-ami) <br>
[Criando uma EC2 com uma AMI personalizada](#criando-uma-ec2-com-uma-ami-personalizada) <br>

**EC2**

[EC2 naming convention](#ec2-naming-convention) <br>
[Creating Placement groups](#creating-placement-groups) <br>
[Elastic network interfaces for EC2](#elastic-network-interfaces-for-ec2) <br>


**EBS**

[Criando um EBS Volume e realizando um multi attach](#criando-um-ebs-volume-e-realizando-um-multi-attach) <br>
[Criando um snapshot a partir de um volume](#criando-um-snapshot-a-partir-de-um-volume) <br>
[Criando um EBS volume a partir de um snapshot](#criando-um-ebs-volume-a-partir-de-um-snapshot) <br>
[Copiando um snapshot para outra AZ](#copiando-um-snapshot-para-outra-az) <br>
[Utilização do Recycle bin para previnir deleções acidentais de snapshots](#utilização-do-recycle-bin-para-previnir-deleções-acidentais-de-snapshots) <br>
[Criando um EBS volume encriptado a partir de um não encriptado](#criando-um-ebs-volume-encriptado-a-partir-de-um-não-encriptado) <br>

**EFS**

[Criando um EFS file system](#criando-um-efs-file-system) <br>
[Attachando um EFS file system a uma EC2](#attachando-um-efs-file-system-a-uma-ec2) <br>
[Lendo arquivos de um EFS File System compartilhado entre duas EC2 em AZs diferentes](#lendo-arquivos-de-um-efs-file-system-compartilhado-entre-duas-ec2-em-azs-diferentes) <br>

**Load-Balancers**

[Criando um target group para utilizar em um Load Balancer](#criando-um-target-group-para-utilizar-em-um-load-balancer) <br>
[Criando um Application Load Balancer](#criando-um-application-load-balancer) <br>
[Criando rules de roteamento em um Application Load Balancer](#criando-rules-de-roteamento-em-um-application-load-balancer) <br>
[Criando um Network Load Balancer](#criando-um-network-load-balancer) <br>
[Adicionando cookies e stickness ao Load Balancer](#adicionando-cookies-e-stickness-ao-load-balancer) <br>
[Criando um Auto Scaling Group](#criando-um-auto-scaling-group) <br>
[Setando o automatic scaling](#setando-o-automatic-scaling) <br>

**Route 53**

[Registrando um domínio no Route 53](#registrando-um-domínio-no-route-53) <br>

**S3**

[Hosteando um website estático no S3](#hosteando-um-website-estático-no-s3) <br>
[Ativando o S3 versioning](#ativando-o-s3-versioning) <br>
[Ativando a replicação de objetos no S3](#ativando-a-replicação-de-objetos-no-s3) <br>
[Inserindo um objeto em algum storage class](#inserindo-um-objeto-em-algum-storage-class) <br>
[Ativando o Lifecycle management](#ativando-o-lifecycle-management) <br>
[Ativando encriptação em objetos no S3](#ativando-encriptação-em-objetos-no-s3) <br>
[Ativando encriptação padrão em um bucket no S3](#ativando-encriptação-padrão-em-um-bucket-no-s3) <br>
[Liberando CORS no S3](#liberando-cors-no-s3) <br>
[Ativando e desativando o S3 MFA Delete](#ativando-e-desativando-o-s3-mfa-delete) <br>
[Ativando o S3 Access Logs](#ativando-o-s3-access-logs) <br>
[Gerando pre signed urls](#gerando-pre-signed-urls) <br>

**CloudFront**

[Inserindo um bucket do S3 no cache do CloudFront](#inserindo-um-bucket-do-s3-no-cache-do-cloudfront)

**SQS**

[Criando uma fila no SQS](#criando-uma-fila-no-sqs)
[Enviando e recebendo mensagens pelo console](#enviando-e-recebendo-mensagens-pelo-console)

## General info

**Important ports**

![image](https://user-images.githubusercontent.com/80921933/206866069-3f848d15-a163-4523-9330-bc46e8af2816.png)

**EC2 Instance Connect** (browser-based connection to an EC2 instance) uses SSH behind the blankets. So you still need to allow connections to port 22.

**IAM Policy Simulator** Can be used to test your IAM policies and check whether they allow or deny an API call. Link to the tool: https://policysim.aws.amazon.com/home/index.jsp?#

## Criando usuários IAM

Podemos criar usuários normalmente, inserí-los em grupos e atribuir policies a tais grupos. Depois de criado, podemos logar com o usuário no console através da url fornecida em **IAM > Dashboard**. 

Perceba que o **Account ID** faz parte da url. Também é possível definir um **alias** para substituir o **Account ID** na url.

![image](https://user-images.githubusercontent.com/80921933/206604315-070069bc-c0ed-43a2-9b8c-f640591e847a.png)

Com o **Account ID** em mãos, podemos logar no console

![image](https://user-images.githubusercontent.com/80921933/206605353-12942d26-5c7a-4090-b965-0a4c4d9f32a3.png)

Seremos redirecionados para a página de login do IAM, bastando informar o restante das informações passadas na criação do usuário para prosseguir

![image](https://user-images.githubusercontent.com/80921933/206605622-1306cf0b-5dca-4a0c-aadc-9bc220ed7e9f.png)

### Aplicação de IAM policies

![image](https://user-images.githubusercontent.com/80921933/206606002-f1a739ca-e0d2-4cfb-862f-a88f0d4fec9d.png)


## Estrutura de uma IAM policy

![image](https://user-images.githubusercontent.com/80921933/206606247-a3bc864f-bb64-4e18-8e5f-fcf43b628533.png)

## Utilizando o AWS Policy Generator

O seguinte site pode ser usado para gerar policies de maneira intuitiva:

https://awspolicygen.s3.amazonaws.com/policygen.html

## Password Policy

Podemos configurar uma **password policy** clicando no seguinte botão:

![image](https://user-images.githubusercontent.com/80921933/206609954-b7cfd290-92d0-4a71-9024-d15a86917e05.png)

Lá, podemos customizar a estrutura das senhas dos **IAM users** criados naquela conta

![image](https://user-images.githubusercontent.com/80921933/206610296-59ffa04a-4bed-4654-8af4-ac318c5ce5ca.png)

## MFA device types

![image](https://user-images.githubusercontent.com/80921933/206609291-4649ee2a-89ef-4a8a-93bb-06833cfe0efd.png)

![image](https://user-images.githubusercontent.com/80921933/206609357-a3bd50d7-6557-4a6b-90a7-7ff65da420df.png)

## IAM Roles

Ao tentarmos rodar o comando

```
aws iam list-users
```

Teremos o seguinte erro

![image](https://user-images.githubusercontent.com/80921933/206866847-0074488b-c612-4211-bb94-fbc4223f3778.png)

Isso acontece porque o EC2 não possui permissões para executar tal ação. Para corrigir isso, temos duas opções:

1. Rodar **aws configure** no EC2 e informar o **Access Key ID** e **Secret Access Key** de uma conta com tais permissões
2. Atribuir uma role à instância com a policy **IAMReadOnlyAccess**

A **opção 1** não é boa porque, caso outras pessoas acessem a mesma EC2, poderão ver as suas credenciais (Access Key ID e Secret Access Key)

Sendo assim, seguimos com a opção 2:

![image](https://user-images.githubusercontent.com/80921933/206867084-11427019-c9d3-4b69-a33f-34cd8c5c79c7.png)

Criando uma role com a policy **IAMReadOnlyAccess**:

![image](https://user-images.githubusercontent.com/80921933/206867226-b2a911aa-4718-45f5-a382-2e52d66c2798.png)

Attachando a role na instância EC2 pelo primeiro menu aberto:

![image](https://user-images.githubusercontent.com/80921933/206867272-10a47c1e-e830-4365-863a-307c1f2473a8.png)

Agora, o comando será bem sucedido.


## Credentials Report

Podemos baixar o **Credentials Report** de uma conta, que consiste em um .xlsx informando todas as informações referentes a **segurança** dos usuários naquela conta.

É acessível por: **IAM > Menu principal > Credentials Report**

![image](https://user-images.githubusercontent.com/80921933/206616990-f5a0cd2d-cbc5-44a2-ae47-f6b611e7306c.png)


## Access Advisor

Tela que fornece informações sobre os últimos serviços acessados por um usuário. Utilizada para reforçar o **principle of the least priviledge**

É acessível por: **IAM > Menu principal > Users > Access Advisor**

![image](https://user-images.githubusercontent.com/80921933/206617368-fc7715e3-c920-4b33-9230-7cd2a255351c.png)

# Billing

Práticas para dominar:



## Permissão na página de billing para IAM users

Ao acessar a página de Billing através de um IAM user (mesmo que ele esteja com a policy **AdministratorAccess**), seremos informados de que ele não tem permissão para tal ação

![image](https://user-images.githubusercontent.com/80921933/206861706-0c0d6e15-d5aa-4d3b-b239-4758317b4296.png)

Basta ativarmos a opção **Activate IAM Access**, no menu **Account** do usuário **ROOT**

![image](https://user-images.githubusercontent.com/80921933/206862125-cd90698e-5ae1-4237-8b85-aacc43882eaf.png)

Agora, retornamos ao IAM user e teremos acesso normalmente à página de **Billing**.

## Criação de budgets

Em **Billing > Budgets > Create Budget**, podemos configurar um budget para que sejamos notificados quando um custo X seja atingido.

![image](https://user-images.githubusercontent.com/80921933/206862451-01a86fbf-b95e-4d42-9824-613fde667a43.png)

Basta seguir o template pré-definido, configurar um valor máximo e um e-mail para ser notificado.

# EC2

## EC2 naming convention

![image](https://user-images.githubusercontent.com/80921933/206863662-f370c08c-a08b-45a1-9d56-6f6b403341d1.png)

## Creating Placement groups

**Placement groups** define how your lanched EC2 instances are going to be spread.

To create a **placement group**, we can go to **EC2 > Network & Security section > Placement Groups**.

![image](https://user-images.githubusercontent.com/80921933/206882417-eafdb014-b41b-4e6f-a162-8999e69290b2.png)

After clicking on **Create placement group**, we can setup our **placement strategy**

![image](https://user-images.githubusercontent.com/80921933/206882456-32eaecf4-2f26-408a-872a-02b6bc74ca98.png)

After that, when launching an instance, we just need to select the created placement group

![image](https://user-images.githubusercontent.com/80921933/206882477-5d1943ee-76e5-4ed0-a167-36a1cc3a9852.png)

## Elastic network interfaces for EC2

We can display an instance's ENI on **EC2 > Instances > \<INSTANCE> > Networking**

![image](https://user-images.githubusercontent.com/80921933/206884742-ec16199a-2981-497c-8dd2-aa9f8080050d.png)

To create a new ENI, go to **Network & Security > Network Interfaces > Create Network Interface**

The newly create ENI will be available to attachment:

![image](https://user-images.githubusercontent.com/80921933/206884813-0f49de77-fb90-4a8b-b844-5f03feae0f62.png)

We can attach it to an EC2 instance through the **Attach** option, after clicking on it

![image](https://user-images.githubusercontent.com/80921933/206884842-fe3d5cf2-73fc-4342-974e-e4abb9423e6d.png)

We just need to choose an instance and it's done!

# Elastic Block Store (EBS)

## Criando um EBS Volume e realizando um multi attach

Ao criar uma instância EC2, podemos acessar opções mais avançadas na aba de **Storage**. Lá, definimos se queremos a flag **delete on termination** ON ou OFF para os EBS volumes. Neste exemplo, deixarei **ON**.

![image](https://user-images.githubusercontent.com/80921933/207129649-fc1588b3-94ca-4675-8f69-26b808496530.png)

Depois de termos a instância criada, podemos verificar que de fato há um volume attachado a ela, na aba de **Storage**

![image](https://user-images.githubusercontent.com/80921933/207129906-a8a44831-8948-4b28-a120-f446c7a12460.png)

Como o EBS suporta multi-attach, podemos criar um outro EBS volume em **Elastic Block Store > Volumes > Create volume**

![image](https://user-images.githubusercontent.com/80921933/207130272-80493f00-0ef2-4509-b75e-2ec3b2440778.png)

Depois, basta preencher as informações. **IMPORTANTE:** O EBS Volume deve ser lançado **na mesma AZ** do EC2 ao qual se deseja attachá-lo. Nesta etapa também seria onde ativaríamos a encriptação de dados no volume para usufruir do EC2 Hibernate.

![image](https://user-images.githubusercontent.com/80921933/207130689-f9028e40-6b7d-4cf2-8705-424821c5f86f.png)

Depois, basta attachar o volume à instância EC2 no menu que será apresentado, após clicar neste botão:

![image](https://user-images.githubusercontent.com/80921933/207130986-1ddba1ba-474d-4b2a-a85b-8e36408c6682.png)

Agora, se verificarmos a aba de storage da EC2, verificaremos que o multi-attach foi bem sucedido.

![image](https://user-images.githubusercontent.com/80921933/207131215-80207e26-6ddf-467f-b428-e00c745714f7.png)

A fim de demonstrar o comportamento do **delete on termination**, podemos dar **Terminate** na EC2.

Antes do terminate:

![image](https://user-images.githubusercontent.com/80921933/207131527-2d22e385-d747-4015-a3cd-a020b54ae318.png)

Depois do terminate:

![image](https://user-images.githubusercontent.com/80921933/207131733-d4b344f4-e72c-428f-89a6-63df2c560a98.png)

O volume root foi deletado, pois tinha a flag **delete on termination** **ON**. O outro volume criado permaneceu vivo, pois não tinha essa flag. Ele pode ser re-attachado a outras instâncias.

## Criando um snapshot a partir de um volume

No menu de um EBS volume, selecionamos **Actions > Create snapshot**

![image](https://user-images.githubusercontent.com/80921933/207141140-7c3846d1-f4bf-47f7-a72c-e7af02a3d6c3.png)

No menu de **Snapshots**, veremos o snapshot criado

![image](https://user-images.githubusercontent.com/80921933/207141456-554ae6bb-1ca2-4f2a-8741-93e3f8ab319e.png)

## Criando um EBS volume a partir de um snapshot

A partir de um snapshot, podemos re-criar um volume, por exemplo, e lançá-lo em outra AZ, através da opção **Create volume from snapshot**.

![image](https://user-images.githubusercontent.com/80921933/207141661-2620aef3-3764-4b4e-9740-ad012d80c7e0.png)

## Copiando um snapshot para outra AZ

Também é possível copiar o snapshot para uma AZ diferente com a opção **Copy snapshot** (encontrada no mesmo menu anterior), a fim de fomentar estratégias de disaster-recovery

![image](https://user-images.githubusercontent.com/80921933/207142070-a6e397e7-ec61-49eb-951d-112a0e9ccac0.png)

## Utilização do Recycle bin para previnir deleções acidentais de snapshots

Dentro do menu de snapshots, podemos clicar na opção **Recycle bin**

![snapshots](https://user-images.githubusercontent.com/80921933/207143698-2dfb592c-9f0d-4b84-9b9d-2ba600f82ea8.png)

Lá, podemos criar **retention rules**, que definem um tempo X para que um snapshot permaneça armazenado em uma "lixeira" após a sua deleção, podendo ser recuperado caso a data da requisição ainda esteja dentro dos limites do **retention rule**.

![image](https://user-images.githubusercontent.com/80921933/207143957-b5864525-23da-4f9d-86a3-b5e18258bf1b.png)

Na aba de **Retention Settings**, definimos um prazo máximo de retenção do snapshot deletado

![image](https://user-images.githubusercontent.com/80921933/207144171-41467858-6acf-440d-9441-ef33b3bbbeb1.png)

Com a **retention rule** criada, podemos consultar a aba de **Resources**, que, atualmente, não terá nenhum snapshot, já que não deletamos nenhum.

![image](https://user-images.githubusercontent.com/80921933/207144354-675d78ef-2574-4eb7-9799-8c1acfa417eb.png)

Após deletarmos o snapshot, veremos que ele foi para a Recycle bin. Podemos selecioná-lo e recuperá-lo, caso a data esteja dentro dos limites.

![image](https://user-images.githubusercontent.com/80921933/207145081-c93f428c-1538-42ea-9814-151805f70a33.png)

## Criando uma AMI

Podemos lançar uma instância EC2 e inserir um script via user data para instalar o Docker

![image](https://user-images.githubusercontent.com/80921933/207161171-69dfee5a-7d62-4456-9c45-bd19b5a5acbf.png)

Depois da instância estar up, podemos rodar **sudo docker ps** e certificar que o Docker fora instalado:

![image](https://user-images.githubusercontent.com/80921933/207161837-cbf6c900-3007-468f-8355-58d6ec66c83c.png)

Com o Docker instalado, podemos criar uma AMI para que não precisemos instalar o Docker toda vez que uma nova instância EC2 for criada. Para tal, selecionamos a opção **Create image**

![image](https://user-images.githubusercontent.com/80921933/207162119-3ca56225-99ee-4178-859b-ebf1bab1c48c.png)

Após configurarmos a AMI, podemos ver ela criada no menu de AMI.

![image](https://user-images.githubusercontent.com/80921933/207163344-c2424cef-db85-4966-a55a-be2c426ae693.png)

## Criando uma EC2 com uma AMI personalizada

Do menu de AMI, podemos selecionar a AMI e clicar em **Launch instance from AMI** (print acima).

Alternativamente, podemos selecionar a AMI no menu de criação de EC2, em **My AMI's**

![image](https://user-images.githubusercontent.com/80921933/207163898-a3b6e17f-ef8e-4c21-8a6b-90b89f060916.png)

Depois, basta seguir o procedimento padrão de criação de EC2.

## Criando um EBS volume encriptado a partir de um não encriptado

![image](https://user-images.githubusercontent.com/80921933/207668790-c5963cd4-a0b5-4196-a132-8a7c54e8d132.png)

## Criando um EFS file system

- Criar um EFS File System

No menu do EFS, clicar em **Create file system**

![image](https://user-images.githubusercontent.com/80921933/207680496-f549828b-d719-487b-aea8-7a5371a04651.png)

Na tela subsequente, clicar em **Customize** para ter mais opções de configuração

Na tela que aparecerá, poderemos configurar todas as opções descritas no arquivo **aws-saa-notes.odt**

No **Step 2**, definimos as AZ's que terão acesso ao file system

![image](https://user-images.githubusercontent.com/80921933/207681761-70f654e7-7a93-49bb-b9cd-6c1978461229.png)

Poderemos confirmar a criação do file system no menu principal

![image](https://user-images.githubusercontent.com/80921933/207682768-67c2cbc6-8ed4-4927-b846-cbd50a0e3f62.png)

## Attachando um EFS file system a uma EC2

No menu de criação de EC2, podemos selecionar a seguinte opção

![Screenshot from 2022-12-14 15-40-09](https://user-images.githubusercontent.com/80921933/207683948-2ee2c41e-cac4-4953-8e24-feb46aa1be73.png)

No menu aberto, selecionamos **Add shared file system**

![image](https://user-images.githubusercontent.com/80921933/207684579-2c35fb1c-e563-43d7-94ea-2fe07c07ac55.png)

No próximo menu, selecionamos o **file system** e o **mount point**, que será o diretório na EC2 para onde poderemos escrever/ler arquivos

![image](https://user-images.githubusercontent.com/80921933/207684950-e62225ac-6161-47f6-85d8-0ca2b239d8d9.png)

Depois, basta criar o EC2 normalmente.

## Lendo arquivos de um EFS File System compartilhado entre duas EC2 em AZs diferentes

Escrevendo da instância 1:

![image](https://user-images.githubusercontent.com/80921933/207686505-72750cc7-66c1-4ec0-ba6b-f0b0055ed8f9.png)

Lendo na instância 2:

![image](https://user-images.githubusercontent.com/80921933/207686696-98605289-348e-4cdb-9837-2388853fd30d.png)

O EFS é montado por padrão em /mnt/efs/fs1.

## Criando um target group para utilizar em um Load Balancer

- As 2 EC2 terão o seguinte user data, que sobe um server http na porta 80 expondo o IP da instância.

  ```
  #!/bin/bash

  yum update -y
  yum install -y httpd
  systemctl start httpd
  systemctl enable httpd
  echo "<h1>Hello from $(hostname -f)</h1>" > /var/www/html/index.html
  ```

Considere as duas instâncias criadas:

![image](https://user-images.githubusercontent.com/80921933/207766522-52db7948-fc38-41ad-9eff-7e7560eef8e3.png)

Ao acessar a porta 80 de cada, recebemos a seguinte tela (o acesso a cada instância dará um IP diferente):

![image](https://user-images.githubusercontent.com/80921933/207766694-e8e4f197-aa3f-4119-9e12-5eb9ab9fc716.png)

Para criar um **target group** com as instâncias, acessamos o menu de **Target Groups**

![image](https://user-images.githubusercontent.com/80921933/207766768-e5dd40a6-cf77-46c7-9e44-a907bfaf3e1a.png)

Depois de clicar em **Create target group**. selecionamos a opção **Instances**

![image](https://user-images.githubusercontent.com/80921933/207766898-f016e6fe-0c9e-4d2e-abca-8fbb8a3aa278.png)

Deixamos as demais opções como padrão e vamos para a próxima tela.

Já na tela de **Register targets**, selecionamos as instâncias e clicamos em **Include as pending below**

![image](https://user-images.githubusercontent.com/80921933/207767123-8ea7c8cc-3c33-4b5b-adba-69178732eb66.png)

Depois, clicamos em **Create target group**, e poderemos vê-lo criado no menu de **target groups**

## Criando um Application Load Balancer

Para criar um **Applcation Load Balancer** para um target group, visitamos o menu de **Load Balancer** e selecionamos a opção **Create Load Balancer**

![image](https://user-images.githubusercontent.com/80921933/207767373-ac19a293-984d-4b17-b5cf-50a9e9e1adc6.png)

Selecionamos a opção **Application Load Balancer**, e configuramos tudo. **Importante:** Deve-se criar um security group exclusivo para o ALB, que permite tráfego HTTP de 0.0.0.0/0. Além disso, é **sempre** uma boa prática permitir tráfego para as instâncias EC2 **somente** do security-group do Load Balancer. Isso significa que as instâncias serão acessíveis através do DNS do Load Balancer, mas não por seus próprios IPs públicos.

Na aba de **Listeners and routing**, selecionamos o **target group** criado

![image](https://user-images.githubusercontent.com/80921933/207767660-7b282fc0-d929-4d0b-bfce-587d5bd32375.png)

Finalizamos a criação do ALB.

Como nosso **target group** dispõe de duas instâncias EC2 com IP diferente, podemos dar refresh no DNS do ALB, e receberemos duas saídas de IP diferentes, fato que prova que o load-balancer está funcionando

Saída 1:

![image](https://user-images.githubusercontent.com/80921933/207769996-a8551d9d-d527-486c-a5e1-0b3dcc59ab4c.png)

Saída 2:

![image](https://user-images.githubusercontent.com/80921933/207770013-f5f5f6fc-5f07-465a-b7af-e5851b209b0a.png)

## Criando rules de roteamento em um Application Load Balancer

No menu do ALB selecionado, clicamos em **View/edit rules**

![Screenshot from 2022-12-15 01-20-11](https://user-images.githubusercontent.com/80921933/207771821-952487fd-e842-4ba2-ab21-c44ad0744392.png)

Podemos clicar no símbolo de **+** e em **Insert rule** para editar regras de roteamento

![Screenshot from 2022-12-15 01-25-41](https://user-images.githubusercontent.com/80921933/207772407-838dcf31-a13b-4346-91ca-94a1d4d1840d.png)

Adicionando uma regra onde, caso o path seja /error, retornar uma mensagem personalizada

![image](https://user-images.githubusercontent.com/80921933/207772155-31b282c0-f304-4e2a-9e2a-7426f8c75b67.png)

Testando a regra

![image](https://user-images.githubusercontent.com/80921933/207772225-94329260-15bb-4fe0-bf88-d6d3f7b23d89.png)

## Criando um Network Load Balancer

Seguir aula 76. 
Passo a passo muito similar a criação do ALB. A única diferença é que o NLB não necessita de um security group.

## Adicionando cookies e stickness ao Load Balancer

Essa opção significa que um usuário, em seu primeiro acesso, fica "vinculado" à instância a qual o ALB o direciona pela primeira vez, por um período de tempo estabelecido.

No menu dos **target groups**, selecionamos a opção **Edit atributes**

![image](https://user-images.githubusercontent.com/80921933/207777078-f7e842ea-5d2f-47d3-af0e-650556fca97b.png)

Na tela que se apresenta, basta configurar o stickiness

![image](https://user-images.githubusercontent.com/80921933/207777249-3e60233b-f43f-4403-9100-a13605b88300.png)

## Criando um Auto Scaling Group

Primeiro, definimos um **target group**

![image](https://user-images.githubusercontent.com/80921933/208152968-1dde3b52-799c-4910-9288-c32650d10275.png)

No menu de **Auto-Scaling Groups**, selecionamos a opção **Create Auto-Scaling Group**

![image](https://user-images.githubusercontent.com/80921933/208153149-8e6ec874-6274-4c03-a9f1-d3a6ccd6898c.png)

No próximo menu, selecionamos a opção **Create launch template**

![Screenshot from 2022-12-16 14-20-12](https://user-images.githubusercontent.com/80921933/208153570-ffa3c647-e97a-42a3-8d93-757cf7cd28c0.png)

Configuramos tudo normalmente, como se fosse o menu de launch de EC2

Depois da criação do **launch template**, selecionamos-o na tela anterior de criação de um **auto-scaling group**

![image](https://user-images.githubusercontent.com/80921933/208154419-8622b5f6-af1e-4dbe-911b-df083c5eccea.png)

Damos sequência na configuração até o menu de configuração de Load-Balancer. Podemos adicionar um Load-Balancer apontando para o ASG, porém, um ALB **já deve estar associado ao target-group escolhido para que isso funcione adequadamente**

![image](https://user-images.githubusercontent.com/80921933/208155266-626c1da8-fca2-4dc6-8e56-a80f439dc006.png)

Na etapa de health-checks, podemos delegar a responsabilidade de health-checking para o ALB, para que este possa remover unhealthy instances

![image](https://user-images.githubusercontent.com/80921933/208155417-588f36a7-9dcc-40d7-8670-a012b1fb4203.png)

Na configuração inicial do group-size, deixarei da seguinte forma:

![image](https://user-images.githubusercontent.com/80921933/208155622-c5630088-3447-4d1f-8771-70156f2aaf22.png)

Com tudo criado, podemos checar as atividades do ASG pelo **Activity history**, na aba **Activity**

Neste caso, setamos o **desired number of instances para 1**, portanto, o ASG automaticamente criou uma instância e deixou-a ativa.

![image](https://user-images.githubusercontent.com/80921933/208156458-4f353ad4-59c9-4456-9915-225aedab6b1a.png)

Caso alteremos o **desired number of instances** para 2, veremos uma alteração na aba de **Activity history**, que representa a criação de uma nova instância de acordo com a nossa alteração.

![image](https://user-images.githubusercontent.com/80921933/208156875-aa4903ae-a134-482c-ba73-320b29ed96c3.png)

Com 2 instâncias, veremos dois IPs diferentes a cada vez que acessarmos o DNS do Load-Balancer

![image](https://user-images.githubusercontent.com/80921933/208157787-fae22dbd-13d4-41d7-b66f-4b6297ccb9ca.png)

![image](https://user-images.githubusercontent.com/80921933/208157844-4b17c30a-fcfb-43f4-b63e-a9c5c91e9e95.png)

As alterações no **Activity history** também acontecem em caso de diminuição da variável **desired number of instances**

## Setando o automatic scaling

Nas configurações de um ASG, podemos configurar a aba de **Automatic scaling** com as seguintes opções:

- **Scheduled actions** - Aumenta o número de instâncias na data informada, ex: 10/10/2023, às 13:00, quero 10 instâncias. 
- **Predictive scaling policies** - Utiliza ML para analisar métricas do passado e escalar baseado nelas. "Forecast".
- **Dynamic scaling policy** - Podemos usar 3 configurações para esse caso: <br>

    Simple scaling: Executa uma ação (adiciona/remove instâncias) baseado em um **CloudWatch Alarm**
        
    ![image](https://user-images.githubusercontent.com/80921933/208170120-2a47833b-5dc2-4fc0-b037-d1b0edd00036.png)
    
     Step scaling: Se baseia no valor de um **CloudWatch Alarm**, e faz um "if", dependendo do valor dele, ex: Se o alarme está MUITO alto, adicione 5 instâncias, mas se está alto, mas não tão alto, adicione 2
     
     Target-tracking scaling: Cria "automaticamente" um **CloudWatch Alarm** e escala baseado nas definições informadas
     
     ![image](https://user-images.githubusercontent.com/80921933/208172198-46d251bc-3aa9-4dff-a8de-0ebd71e96f0a.png)
     
## Registrando um domínio no Route 53

Clicamos em **Register Domain**

![image](https://user-images.githubusercontent.com/80921933/208768808-26883769-8cd5-4899-97d5-6f9b2e7f931c.png)

Ao registrar um domínio, teremos um **Hosted Zone** criado, que é a sua URL-base escolhida.

A partir dele, podemos criar os nossos **DNS records**, que são variações da URL do **Hosted Zone**

A partir do **DNS record**, definimos para qual IP aquele **DNS record** irá nos direcionar

![image](https://user-images.githubusercontent.com/80921933/208770473-bd6bca29-ea86-436b-9452-2682edf67764.png)

## Hosteando um website estático no S3

Acessamos a opção **Properties**, nas configurações de um bucket

![image](https://user-images.githubusercontent.com/80921933/209164249-ff47e3b1-f788-4d09-a6a8-27aea754aba2.png)

Ao final da aba, selecionamos a opção **Static website hosting**

![image](https://user-images.githubusercontent.com/80921933/209164474-18d7c75f-a908-4862-986d-3e01002c7988.png)

Basta clicarmos em **Edit** e configurar as opções. Nomearei de **index.html** o arquivo do website, podendo ser alterado.

![image](https://user-images.githubusercontent.com/80921933/209164720-8678cbdf-b3cc-4979-b967-e2f20d87e71e.png)

Depois, basta anexar o arquivo ao bucket, e acessar a url pública disponibilizada.

## Ativando o S3 versioning

Nas properties de um bucket, selecionamos **Bucket versioning**

![image](https://user-images.githubusercontent.com/80921933/209165807-9a3eb3c2-45ba-4bc9-810d-b7f8402d51ff.png)

Após ativarmos a opção, podemos realizar o re-upload para o S3. Todas as versões do arquivo serão visíveis

![image](https://user-images.githubusercontent.com/80921933/209166216-97c60d7e-bc30-47ce-b2b1-5f7a2bdc9eb0.png)

Importante ressaltar que objetos uploaded antes de ativar o versionamento terão o seu **Version Id** = null

Ao deletar versões, o S3 restaurará a última versão disponível.

Ao deletar um objeto inteiro, inserimos um **Delete Marker** no objeto, que é uma flag para não expor aquele objeto.

## Ativando a replicação de objetos no S3

Para que a replicação funcione, **o bucket-versioning deve estar ativo em ambos!**

Supondo que temos os dois buckets criados em regiões diferentes

![image](https://user-images.githubusercontent.com/80921933/209173836-5ba9af2f-c422-4ccb-b57c-9bbe58414539.png)

Nas configurações do bucket de origem, vamos para **Management** > **Replication rules** > **Create replication rule**

![image](https://user-images.githubusercontent.com/80921933/209174377-a77f8a64-c0e0-4230-a17f-933c666f8202.png)

Após selecionar o bucket de destino e configurar as demais opções, a replicação estará funcional.

**Importante:** Por padrão, **Delete Markers** não são replicados, mas podemos alterar esse comportamento pela seguinte opção:

![image](https://user-images.githubusercontent.com/80921933/209174632-2f3afef4-87a2-4693-8b60-9b64c103e4fb.png)

Por outro lado, deletes permanentes **não são replicados.**

## Inserindo um objeto em algum storage class

Ao inserir um objeto em um bucket, podemos acessar a aba de **Properties** e definir para qual storage class aquele objeto irá

![image](https://user-images.githubusercontent.com/80921933/209182147-906244f7-1dcb-43ed-8ce9-57f85d791b71.png)

No menu do bucket, poderemos ver o storage class escolhido, que também pode ser posteriormente alterado clicando-se no objeto

## Ativando o Lifecycle management

Nas opções de um bucket, clicamos em **Management** e acessamos a aba **Lifecycle rules**

Clicamos em **Create lifecycle rule**

![image](https://user-images.githubusercontent.com/80921933/209185600-88b6e5a7-82a7-4a19-a96f-558b6b72ccc5.png)

Em **Lifecycle rule actions**, podemos escolher os tipos de regras desejadas

![image](https://user-images.githubusercontent.com/80921933/209185274-e6c8c688-9865-4946-93cc-fae976027363.png)

Depois, basta criar as regras de transição de dados desejada

![image](https://user-images.githubusercontent.com/80921933/209185541-7a954502-6714-43c8-a8e4-1f84075bcb3e.png)

# Ativando encriptação em objetos no S3

Ao realizar o upload de um objeto, podemos acessar a opção **Server-side encryption**, no final da página, e escolher a opção desejada

![Screenshot from 2022-12-23 19-41-44](https://user-images.githubusercontent.com/80921933/209411222-e01f9e3a-2c66-45f5-bfd7-11a0a956a0dd.png)

# Ativando encriptação padrão em um bucket no S3

Nas configurações de um bucket, na aba **Properties**, acessamos a opção **Edit default encryption**

![image](https://user-images.githubusercontent.com/80921933/209411348-d806ba68-0656-4f7c-82c1-751dcdacb21f.png)

Daí, basta escolher o recurso para encriptação.

Também é possível sobreescrever o mecanismo de encriptação do bucket no momento do upload de um objeto:

![image](https://user-images.githubusercontent.com/80921933/209411552-88ec1e8c-10f3-44b3-8408-43250229c465.png)


## Liberando CORS no S3

Na sessão **Permissions** de um bucket, no final da página, temos as configurações de CORS

![image](https://user-images.githubusercontent.com/80921933/209410980-9ad74c64-bb7e-448c-a082-631f31551d2e.png)

Essas configurações são escritas em JSON, como nesse caso:

![image](https://user-images.githubusercontent.com/80921933/209411002-25101ae9-8a49-4698-90d9-ca11538b7273.png)

Basta escrevermos o JSON, permitindo as origins desejadas.

## Ativando e desativando o S3 MFA Delete

Feature que só permite que deletemos objetos de um bucket com um código fornecido pelo MFA

Para ativar esta feature, basta rodar os comandos abaixo (tendo o Access Key ID e Secret Access Key configurados com o **aws configure**):

![image](https://user-images.githubusercontent.com/80921933/209412020-299170e4-293d-461d-8e1c-e08b6aec601b.png)

## Ativando o S3 Access Logs

Em um bucket, vamos para a aba **Properties** e selecionamos a opção **Server Access Logging**

Configuramos o bucket de destino

![image](https://user-images.githubusercontent.com/80921933/209415187-4a1bf98f-c4e0-4672-affe-b547d2535df8.png)

Após ativarmos essa feature, o bucket de destino armazenará todas as ações realizadas dentro do bucket configurado.

## Gerando pre signed urls

As pre-signed URLs são usadas para fornecer accesso temporário a objetos armazenados no S3.

Selecionamos algum objeto de um bucket, e selecionamos o drop-down **Actions**, para selecionar a opção **Share with a pre-signed url**

![Screenshot from 2022-12-23 21-39-36](https://user-images.githubusercontent.com/80921933/209415604-498ac572-1295-4225-b9c8-02fa881edb1a.png)

Depois, basta configuramos o tempo desejado de expiração da URL

![image](https://user-images.githubusercontent.com/80921933/209415625-a4b71810-bb43-4fe3-9aef-365ac49333bd.png)

Agora, basta compartilhar a URL.

![image](https://user-images.githubusercontent.com/80921933/209415639-a886042a-bb8e-4944-b5ba-c8633cea59c0.png)

## Inserindo um bucket do S3 no cache do CloudFront

**Importante:** Para este exemplo, utilizamos um bucket não-público. Ou seja, na opção **Origin Access**, selecionamos a utilização de um OAC

Com um bucket já criado (inseri uma imagem nele), clicamos em **Create a CloudFront distribution**

![image](https://user-images.githubusercontent.com/80921933/209419344-2ea54c92-6f8c-438e-9c91-ee6c2c73b810.png)

Selecionamos nosso bucket como **Origin**

![image](https://user-images.githubusercontent.com/80921933/209419431-a6ec8da3-189e-47c6-99a6-358fddd02463.png)

Em **Origin Access**, criamos um **Control setting** com os valores padrões

![image](https://user-images.githubusercontent.com/80921933/209419511-882c6496-1b1d-411c-b2c5-f42fb0a003d3.png)

Finalizamos por aqui. Só dar um **Create**

No topo da próxima página, veremos a seguinte mensagem:

![image](https://user-images.githubusercontent.com/80921933/209419572-07441d22-02eb-4473-b8fc-c4c5ba133c61.png)

Basta copiar a policy gerada, inserí-la no bucket, e acessar o DNS fornecido pelo CloudFront. Os dados já estarão com o cache sendo realizado.

## Criando uma fila no SQS

Na tela inicial do serviço, clicamos em **Create Queue**

![image](https://user-images.githubusercontent.com/80921933/209453186-c578002c-2f4c-4052-a7c1-7b71e8d7adc0.png)

Na sessão de configurações, definimos uma série de aspectos, como: encriptação, quem pode mandar e receber mensagens da fila (somente o dono e/ou IAM users), tipo da fila (Standard ou FIFO), etc.

Após finalizar as configurações, basta clicar em **Create Queue** no final da página.

## Enviando e recebendo mensagens pelo console

Com a fila criada, clicamos em **Send and receive messages**

![image](https://user-images.githubusercontent.com/80921933/209453222-e39a8cdb-f3f2-423b-bb6d-1da0f187f380.png)

Basta escrevermos uma mensagem e clicar em **Send message**

![image](https://user-images.githubusercontent.com/80921933/209453232-c56cf8ac-a002-4d39-8723-40625c1a6288.png)

A aba de **Receive messages**, localizada logo abaixo, nos informará acerca da mensagem recebida

![image](https://user-images.githubusercontent.com/80921933/209453239-c9beb539-2d9d-44fb-87fb-e1038dc597d0.png)

Podemos clicar no botão **Poll for messages** para que a mensagem seja mostrada

![image](https://user-images.githubusercontent.com/80921933/209453248-1ef16d18-e1ab-48d7-9b99-13e42972f381.png)

Ao clicar na mensagem, poderemos acessar suas informações

![image](https://user-images.githubusercontent.com/80921933/209453255-a4384c79-5d53-4205-a12b-9e410fcb35a0.png)

Após a leitura da mensagem, deve-se apagá-la.





