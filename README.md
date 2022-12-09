# IAM

Práticas para dominar:

- Criação de usuários
- Login com um usuário IAM
- Utilização de alias no Account ID
- Inserção de usuários em grupos
- Estrutura das IAM policies
- Password Policies
- Implementação do MFA

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






