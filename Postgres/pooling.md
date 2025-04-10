# Pooling de Conexões com PostgreSQL

## Contexto

- **Motivação**: aplicações que utilizam Jobs ou múltiplas conexões ao banco de forma concorrente.

- **Problema**: Criar e fechar conexões a cada execução de query é custoso em termos de performance.

- **Solução**: Pool de conexão.


## Pooling de Conexões

Manter um conjunto de conexões abertas com o banco de dados, prontas para serem reutilizadas, evitando o custo de abrir/fechar conexões a cada operação.

### Benefícios:
- Evita abrir/fechar conexão a cada operação, mantendo conexões ativas e reutilizáveis.
- Melhor performance e escalabilidade em ambientes com múltiplos acessos simultâneos.
- Permite configurar limites de conexões e timeouts de inatividade.

### Funcionamento:
- Quando o app faz a primeira query, o pool abre uma nova conexão.
- As conexões vão sendo adicionadas ao pool conforme a demanda, até o limite definido.
  - Se passar desse limite, há espera por uma conexão ou falha por timeout.
- Quando uma requisição termina, a conexão é devolvida ao pool.
- Conexões inativas por muito tempo são fechadas, via timeout.
- Quando o app encerra, é preciso encerrar a pool para fechar todas as conexões.

### Estratégias para manter uma conexão aberta (diminuição de latência):
- Executar uma query simples [[[await pool.query('SELECT 1');]]] a cada intervalo de tempo.
- Se o driver suportar (ORMs como o Lucid ou Sequelize), é possível setar um mínimo de conexões ativas:

```bash
pool: { min: 1, max: 10 }
```


## Conexão com mais de um banco

- Instanciar as pools em um único arquivo de configuração, como `/database/connection`.
- No mesmo arquivo de configuração pode criar funções `openAllPools` e `closeAllPools`.

### `openAllPools`:
- Dependendo do contexto, é opcional.
- Interessante para aquecer o banco e diminuir a latência.
- Bom para API que roda por meio de Jobs, evita retries desnecessários.

### No arquivo de entrada:
- `openAllPools`: deve disparar antes do processamento da lógica.
- `closeAllPools`: deve disparar no shutdown da aplicação:   
   - **SIGTERM**: ideal para uso com DOCKER
   - **SIGINT**: ideal para uso com SERVIDOR DE DESENVOLVIMENTO
   - **beforeExit**
   - **uncaughtException**


### Utilização da Pool:
- Fácil.
- Quando for rodar a lógica, pega uma conexão por meio da instância do Pool do DB que desejar.
- A partir daí roda a query e depois libera a conexão.
