# CapRover

## Variáveis de Ambiente

1. **Tipos de comportamento que apps podem ter se não tiverem variáveis de ambiente (.env):**  
   - **Comportamento de Quebra:** Algumas variáveis são essenciais, como as de conexão com o banco de dados.  
   - **Comportamento de Indeterminação:** O app pode até funcionar sem estas variáveis, mas, quando requisitadas, será atribuído o valor `undefined`.

2. **Deploy no CapRover:**  
   - O CapRover possui um local para alocar as variáveis de ambiente do projeto, chamado de **repositório de env vars**.  
   - O CapRover permite que o projeto funcione com ou sem o arquivo `.env` na imagem Docker. Vamos chamar este `.env` de **`.env docker`**.  

      **Cenários possíveis:**
      1. **`.env fora da imagem Docker`:**  
         Utilização das variáveis definidas no **repositório de env vars**.  
         - Se alguma variável estiver faltando, ocorre o **Comportamento de Indeterminação**.

      2. **`.env dentro da imagem Docker`:**  
         Ocorre uma **mescla** entre o **repositório de env vars** e o **`.env docker`**, onde o **repositório de env vars** tem prioridade:  
         - **a)** As variáveis do **repositório de env vars** sobrescrevem as do **`.env docker`**.  
         - **b)** Se o **repositório de env vars** não tiver alguma variável definida no **`.env docker`**, será utilizada a variável do **`.env docker`**.  
         - **c)** Se uma variável não estiver definida nem no **repositório de env vars** nem no **`.env docker`**, ocorre o **Comportamento de Indeterminação**.

     

## Acessibilidade Interna

1. **Acessibilidade Interna de Apps:**  
   - Requisições usando URLs públicas não são mais permitidas para comunicação interna entre apps.  
   - O CapRover utiliza a resolução interna de nomes via rede do Docker para comunicação entre serviços.  
   - A comunicação é restrita à **rede interna do Docker**, o que evita tráfego desnecessário fora da rede do servidor.  
   - Cada app web possui um identificador interno no formato:  
     `http://srv-captain--{nome-do-app}:{porta-mapeada}`  
   - Nas variáveis de ambiente, utilize o formato:  
     `http://srv-captain--{nome-do-app}:{porta-mapeada}` para referenciar outros apps.  
   - Se a `porta-mapeada=80`, é suficiente escrever:  
     `http://srv-captain--{nome-do-app}`.  

2. **Gerenciamento de Portas de Apps:**  
   - No Docker (e, por consequência, no CapRover), cada contêiner é um ambiente isolado.  
   - Dentro de cada contêiner, é possível usar a mesma porta interna para diferentes apps devido ao isolamento.  
   - O CapRover gerencia automaticamente o mapeamento de portas externas.  
   - Sem esse gerenciamento, ocorreria erro se dois apps tentassem expor diretamente a mesma porta externa.  

