# Acessibilidade Interna

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