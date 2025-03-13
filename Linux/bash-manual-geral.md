# Documentação Pessoal da Linha de Comando do Linux - Bash

## 1. Informações Básicas

### Comandos

* Um **Full Command** consiste em:  
`Command + Option(s) + Argument(s)`

* A parte mais importante de um Full Command é o **Command** em si. Options e Arguments o complementam.  
`ls` → Full Command gerado por um Command.  
`ls -l -a` → Full Command gerado por um Command + Options.

* A seguir, estes três são equivalentes, e nos casos 2 e 3 a ordem não importa:  
`ls -l -a` = `ls -la` = `ls -al`

De agora em diante, vamos nos referir a um 'Full Command' simplesmente como 'Command', pois não há risco de confusão.

### Terminal

* **Home directory**: Como abrimos o Terminal e o `~` é exibido na tela, estamos no diretório home.

## 2. Escrevendo comandos no shell a partir do prompt

`ls`

`ls -l`

`ls -al`

`clear` -> limpar terminal

## 3. Encontrando ajuda para comandos

**`man [command]`** -> `man ls`  
Se pressionarmos `/` e digitarmos o comportamento desejado, o comando tentará buscar na lista de opções.  
Exemplo:  
`man ls` [Enter]  
`/comma separed` [Enter]  
Deve encontrar se o termo pesquisado corresponder a alguma descrição de opção.

**`[command] --help`** -> `ls --help`

**`apropos [supposed command]`** -> `apropos list`  
**`apropos "[what the command suppose to do]"`** -> usando aspas duplas podemos obter uma correspondência exata

## 3. Autocompletar com a tecla TAB

1. Completa o nome de um arquivo ou pasta  
2. Faz sugestões

`ls -l De` seguido pela tecla Tab

`ls -l Do` seguido pela tecla Tab duas vezes

`ls -l Doc` seguido pela tecla Tab

`a` seguido pela tecla Tab

## 4. Atalhos de teclado úteis

| Combinação de teclas      | Resultado                                |
|---------------------------|------------------------------------------|
| CRTL + A                  | Mover para o início da linha             |
| CRTL + E                  | Mover para o final da linha              |
| setas                     | Mover letra por letra                    |
| CRTL + ->                | Mover uma palavra para a esquerda        |
| CRTL + <-                | Mover uma palavra para a direita         |
| CRTL + U                  | Deletar do cursor até o início da linha   |
| CRTL + K                  | Deletar do cursor até o final da linha    |
| CRTL + SHIFT + C          | Copy                                     |
| CRTL + SHIFT + V          | Paste                                    |
| (seta para cima/baixo)    | Exibe comandos anteriores                |
| CRTL + R                  | Pesquisar no histórico de comandos       |
| CRTL + C                  | Cancelar comando                         |
| CRTL + L                  | Limpar terminal                       |

## 5. Sistema de Arquivos

1. Caminho absoluto: começa com `/` para o diretório raiz do sistema de arquivos.  
2. Caminho relativo: não começa com `/`.

**`file [document]`** -> Determina o tipo de arquivo

**`stat [document]`** -> Exibe o status do arquivo ou do sistema de arquivos

## 6. Navegação pelo sistema de arquivos

**`cd`** -> Change Directory  
**`pwd`** -> Print Working Directory

Ir para a pasta Documents e imprimir o diretório de trabalho atual:
`cd Documents/` 
`pwd`

Usando `cd` com diretórios que possuem espaços:  
1. Comando inválido  
   `cd Exercise Files`  
2. Possibilidades de comandos válidos:  
   2.1: Usando aspas duplas  
       `cd "Exercise Files"`  
   2.2: Usando escape (uso comum)  
       `cd Exercise\ Files`

Listar arquivos recursivamente:  
`ls -R departments/`

Ponto único:  
`.` -> representa o diretório atual

Navegação entre diretórios:  
1. `cd departments/hr/policies` -> vai para o diretório `departments/hr/policies`  
2. `cd ..` -> sobe um nível = `departments/hr`  
3. `cd ..` -> sobe mais um nível = `departments`  
4. `cd hr/policies` -> desce dois níveis seguidos = `departments/hr/policies`  
5. `cd ../../finance/documents` -> sobe dois níveis e entra em `departments/finance/documents`  
6. `cd -` -> alterna entre o diretório anterior e o atual  
7. `cd` -> volta para o diretório home

## 7. Comando ls, um dos comandos mais úteis

`ls`

`ls --color=always` -> útil para representar diferentes aspectos dos arquivos

`ls -l` -> utiliza um formato de listagem longa (ver metadata)

`ls -lh` -> exibe metadata de forma legível, útil para verificar tamanhos de arquivos

## 8. Criar e remover diretórios

Suponha que exista previamente uma pasta `departments`...

1. **Criar**

- `mkdir newfolder` -> cria uma nova pasta `newfolder`

- `mkdir departments/customerservice` -> dentro de `departments` cria a pasta `customerservice`

- `mkdir departments/customerservice/documents departments/customerservice/cases departments/customerservice/awards` -> cria mais de uma pasta de uma vez

- `mkdir -p departments/legal/contracts` -> Com a opção `-p`, cria a pasta e as pastas pai de uma vez

2. **Remover**

- `rmdir departments/legal/contracts/` -> Remove pastas. Essa remoção só é permitida se a pasta estiver vazia.

- `rmdir departments/legal/` -> remove a pasta `legal`

## 9. Copiar, mover e excluir arquivos e diretórios

1. **Copiar**: `cp [file] [diretório para copiar e novo nome (opcional)]`  
   - `cp poems.txt poems2.txt` -> copia o arquivo `poems.txt` para o mesmo diretório, nomeando a cópia como `poems2.txt`  
   - `cp simple_data.txt departments/hr/employee\ info/` -> copia o arquivo `simple_data.txt` para o diretório `departments/hr/employee\ info/`  
   - `cp simple_data.txt departments/new.txt` -> copia o arquivo `simple_data.txt` para o diretório `departments`, nomeando a cópia como `new.txt`

2. **Mover**: 
   1. **Mover um arquivo**: `mv [file] [diretório]`  
      `mv poems2.txt departments/marketing`  
   2. **Renomear um arquivo**: `mv [file] [mesmo diretório do arquivo + novo nome]`  
      `mv departments/marketing/poems2.txt departments/marketing/literature.txt`
      
      Suponha que você esteja no diretório `documents` e exista o subdiretório `departments/marketing/literature.txt`:
      
      `mv departments/marketing/literature.txt .` -> move o arquivo `literature.txt` para o diretório atual (`documents`, neste caso).

      `mv *.txt departments/marketing/` -> move todos os arquivos com extensão .txt para o diretório `departments/marketing/`  
      `mv departments/marketing/* .` -> move todos os arquivos do diretório `departments/marketing/` para o diretório atual.

3. **Remover**: `rm [file]` -> Atenção: não há como desfazer!  
   `rm literature.txt`

Removendo recursivamente:  
`rm -r departments/customerservice/`

## 10. Comando find, uso básico

_consulte o manual (man) para mais informações sobre este comando_

1. Caminho relativo:  
   `find . -name "poe*"` -> encontra, no diretório atual, por nome, todos os arquivos que começam com "poe".
   
2. Caminho absoluto:  
   `find ~/Documents -name "*d*"` -> encontra, no diretório Documents, por nome, todos os arquivos que contêm o caractere "d".

`find / -name "filename"` -> pesquisa recursivamente por arquivos chamados 'filename', iniciando a partir do diretório raiz.

## O sudo

_sudo significa Super User DO_

Uso -> `sudo [Full Command]`

Um usuário comum não pode acessar:  
`ls /root`

O sudo pode acessar:  
`sudo ls /root`

Removendo os privilégios sudo do usuário:  
`sudo -k`

Inicia um shell interativo como root:  
`sudo -s`

## 11. Links

`ln -s(optional) [target file] [link name]`

- soft (symbolic) link: aponta para outro arquivo, caminho relativo  
- Hard link: aponta para um dado específico no disco, caminho absoluto

_OBS_: Ambos quebram se o arquivo original for movido.

Arquivo aponta para outro arquivo, usando a opção -s (ver informações com `ls -l`):  
`ln -s poems.txt writing.txt` -> cria o soft link writing.txt para o arquivo poems.txt

`cat writing.txt` -> imprime o conteúdo do arquivo

Arquivo aponta para os dados do disco, omitindo a opção -s (ver informações com `ls -l`):  
`ln poems.txt words.txt`

## 12. Pipes

Pipe: `|` -> pega a saída de um comando e a envia para outro. A ordem importa!

- echo: imprime o argumento.  
  `echo "Hello"`

- wc: imprime a contagem de linhas, palavras e bytes para cada arquivo.

- Combinando echo + wc de uma vez com o auxílio do pipe:  
  1. `echo "Hello" | wc`  
  2. `echo "Hello world from the command line" | wc`

## 13. Variáveis de ambiente e PATH

`env` -> Lista as variáveis de ambiente, incluindo o PATH.

`echo $PATH` -> exibe o valor da variável de ambiente PATH.

## 14. Informações sobre a distribuição Linux

Exibe informações de forma resumida:  
`cat /etc/lsb-release`

Exibe informações de forma mais detalhada:  
`cat /etc/os-release`

Exibe informações de ambas as maneiras de uma vez:  
`cat /etc/*release`

Exibe informações do Kernel do Linux:  
`uname -a` -> Exibe todas as informações  
`uname -r` -> Exibe apenas a versão do Kernel.

## 15. Instalar e atualizar software com um gerenciador de pacotes

Verifica se tudo está atualizado (interessante executar antes de instalar qualquer pacote):  
`sudo apt update`

Instala um pacote:  
`sudo apt install tree`

Instala novas versões dos pacotes:  
`sudo apt upgrade`
