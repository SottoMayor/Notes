# Variáveis de Ambiente

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
