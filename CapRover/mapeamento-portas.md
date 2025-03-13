# Mapeamento de portas

O mapeamento de portas é o processo de associar uma porta externa do servidor (por exemplo, porta 80) a uma porta interna do container (como a porta 3333 do AdonisJS). Isso permite que o tráfego externo seja direcionado para a aplicação dentro do container, tornando-a acessível ao público.

__Passos__:

1. Acesse a seção "HTTP Settings" do seu aplicativo no CapRover.   
2. Em "Container HTTP Port", insira o valor da porta do seu aplicativo (geralmente, a porta definida no arquivo .env). No caso de AdonisJS, por exemplo, o valor padrão é 3333.   
3. Clique em Salvar para aplicar as mudanças.   

   
__Obs__: É interessante que as variáveis de ambiente PORT e HOST estejam no arquivo `.env`. Caso essas variáveis não estejam presentes, é possível contornar isso, mas não é a abordagem recomendada. Para isso:
1. Descubra a porta padrão do framework (ex: AdonisJS => 3333).
2. Realize o mapeamento dessa porta padrão no CapRover.