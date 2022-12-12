# General information

**Important ports**

![image](https://user-images.githubusercontent.com/80921933/206866069-3f848d15-a163-4523-9330-bc46e8af2816.png)

**EC2 Instance Connect (browser-based connection to an EC2 instance) uses SSH behind the blankets. So you still need to allow connections to port 22.**

# IAM

Práticas para dominar:

- Criação de usuários
- Login com um usuário IAM
- Utilização de alias no Account ID
- Inserção de usuários em grupos
- Estrutura das IAM policies
- Password Policies
- Implementação do MFA
- Uso do Access Key ID e Secret Access Key
- Utilização das IAM Roles
- Credentials Report e Access Advisor

## Criando usuários

Podemos criar usuários normalmente, inserí-los em grupos e atribuir policies a tais grupos. Depois de criado, podemos logar com o usuário no console através da url fornecida em **IAM > Dashboard**. 

Perceba que o **Account ID** faz parte da url. Também é possível definir um **alias** para substituir o **Account ID** na url.

![image](https://user-images.githubusercontent.com/80921933/206604315-070069bc-c0ed-43a2-9b8c-f640591e847a.png)

Com o **Account ID** em mãos, podemos logar no console

![image](https://user-images.githubusercontent.com/80921933/206605353-12942d26-5c7a-4090-b965-0a4c4d9f32a3.png)

Seremos redirecionados para a página de login do IAM, bastando informar o restante das informações passadas na criação do usuário para prosseguir

![image](https://user-images.githubusercontent.com/80921933/206605622-1306cf0b-5dca-4a0c-aadc-9bc220ed7e9f.png)


## IAM Policies

### Aplicação de IAM policies

![image](https://user-images.githubusercontent.com/80921933/206606002-f1a739ca-e0d2-4cfb-862f-a88f0d4fec9d.png)


### Estrutura de uma IAM policy

![image](https://user-images.githubusercontent.com/80921933/206606247-a3bc864f-bb64-4e18-8e5f-fcf43b628533.png)


## Password Policy

Podemos configurar uma **password policy** clicando no seguinte botão:

![image](https://user-images.githubusercontent.com/80921933/206609954-b7cfd290-92d0-4a71-9024-d15a86917e05.png)

Lá, podemos customizar a estrutura das senhas dos **IAM users** criados naquela conta

![image](https://user-images.githubusercontent.com/80921933/206610296-59ffa04a-4bed-4654-8af4-ac318c5ce5ca.png)


## Multi-factor authentication (MFA)

### MFA device types

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

## Criando um EBS Volume (com ou sem delete on termination) e realizando um multi-attach

Ao criar uma instância EC2, podemos acessar opções mais avançadas na aba de **Storage**. Lá, definimos se queremos a flag **delete on termination** ON ou OFF. Neste exemplo, deixarei **ON**.

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














