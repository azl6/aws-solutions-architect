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

**TODO:** PENDENTE DE INSERÇÃO!


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










