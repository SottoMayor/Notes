
# CI/CD usando Webhooks do GitHub

## Funcionamento
- **Push** no GitHub para a branch X.
- O app **CapRover**, apontando para a branch X, faz o build automático.

## Diagrama de Funcionamento

Push no GitHub -> Notificação para o CapRover -> build automático.


## Passos no CapRover
### Passos
1. Abrir o app.
2. Ir à aba **Deployment**.
3. Copiar a **Webhook URL** para os deploys do GitHub.

### Observações
- O CapRover só faz deploy na branch configurada para o app.
- O CapRover só gera a **Webhook URL** quando a integração com o GitHub está configurada.

## Passos no GitHub
### Passos
1. No GitHub, acesse **Settings** → **Webhooks** → **Add webhook**.
2. Cole a **Webhook URL** em **Payload URL**.
3. Configure o **Content-Type** para `application/json`.
4. No campo **Secret**, deixe em branco (a menos que tenha configurado um no CapRover).
5. Configure o disparo do webhook para ocorrer somente quando houver push ("Just the push event").
6. Adicione o webhook.

### Observações
- É possível consultar cada disparo do webhook.
- O campo **Secret** pode ir em branco, o CapRover não valida a assinatura do webhook.

## Interação Teórica vs. Prática
### Teoricamente
- Um único token e webhook poderiam servir para múltiplas branches e apps, já que ambos são únicos para o repositório.

### Na Prática
- Quando um repositório possui vários apps CapRover apontando para branches diferentes, é necessário configurar um webhook para cada app.
- Isso garante que cada branch seja monitorada e que o deploy automático ocorra corretamente para cada app.

## Problemas que Podem Afetar o Deploy
- Expiração do Auth Token do GitHub ou erros de sintaxe no TypeScript.
- Não há notificação quando isso ocorre:
  - A resposta de sucesso do GitHub refere-se apenas ao disparo do webhook.
- Se ocorrer, o sistema mantém a versão funcional anterior.

### Subterfúgios
- **Rodar o build localmente:**  
   - Faça o build do framework na própria máquina antes do push para o repositório.
   - Ex. de build de framework: transpilação de TS para JS, como o NestJS. 