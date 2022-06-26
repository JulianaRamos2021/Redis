![image](https://user-images.githubusercontent.com/78691172/174131694-2befa329-c6ba-4f7a-829b-4ad453781097.png)


#Criando e configurando banco de dados Redis

Redis é um servidor de estruturas de dados chave-valor que fornece suporte a diferentes tipos de valores. Indicado para aplicações com alta exigência de resposta rápida e processamento dinâmico. Aceita estruturas mais complexas como string, listas, sets, sets ordenados, streams, hyperloglogs e hash.
É indicado o uso de chaves simples com no máximo 1 MB. É indicado instanciar as chaves e evitar abreviações, exemplo de chave adequada: "object-type:id".



## Exercícios -SETS

1. Deletar a chave “pesquisa:produto”
Comando: del pesquisa:produto
![image](https://user-images.githubusercontent.com/78691172/175814955-90453912-4cab-43b2-b830-60d20e9d87d0.png)

*O zero significa que a chave não existe, se o resultado for 1 então a chave foi deletada.




2. Criar a chave "pesquisa:produto" do tipo set com os seguintes valores: monitor, mouse e teclado
Comando: sadd pesquisa:produto monitor mouse teclado

![image](https://user-images.githubusercontent.com/78691172/175815037-4d848ade-2010-433c-9e2d-8a260b3b09e0.png)


3. Visualizar a quantidade de valores da chave
Comando: scard pesquisa:produto
![image](https://user-images.githubusercontent.com/78691172/175815068-0541baa3-4d32-4155-94df-424cbeae2404.png)

4. Retornar todos os elementos da chave
Comando: smembers pesquisa:produto
![image](https://user-images.githubusercontent.com/78691172/175815210-c46e1b30-dff5-4e35-bd23-2f7e2a35ec6c.png)

5. Verificar se existe o valor monitor
Comando: sismember pesquisa:produto monitor
![image](https://user-images.githubusercontent.com/78691172/175815280-3c8415a2-def1-4588-a835-cac5701fbc68.png)

*O retorno 1 significa que o valor existe, retorno 0 significa que não existe.

6. Remover o valor monitor
Comando: srem pesquisa:produto monitor
![image](https://user-images.githubusercontent.com/78691172/175815350-fcf5e656-b273-487c-b449-1731c26c27b6.png)

*Retorno 1 significa que o valor foi excluído.

7. Recuperar um elemento e remove-lo do set
Comando: spop pesquisa:produto
![image](https://user-images.githubusercontent.com/78691172/175815545-6e0daccc-69c1-4891-917d-8fc74174137f.png)


8. Criar a chave "pesquisa:desconto“ do tipo set com os seguintes valores: memória RAM, monitor, teclado, HD
Comando: sadd pesquisa:desconto 'memoria RAM' monitor teclado HD

![image](https://user-images.githubusercontent.com/78691172/175815616-808fb3d1-59f4-4ab0-a68a-2050deae244e.png)

9. Próximas questões fazem uso dos sets pesquisa:produto e pesquisa:desconto

Visualizar a interseção entre os 2 sets
Comando: sinter pesquisa:produto pesquisa:desconto
![image](https://user-images.githubusercontent.com/78691172/175815745-d813a691-7643-4a17-9f94-6cad356b1385.png)

*No meu resultado não foi gerada interseção pois não existem valores iguais dentro das chaves.


Visualizar a diferença entre os 2 sets
Comando:sdiff pesquisa:produto pesquisa:desconto
![image](https://user-images.githubusercontent.com/78691172/175815832-97f41c6a-594f-462b-b79d-f3f6e448d5ba.png)


Criar o set "pesquisa:produto_desconto" com a união entre os 2 sets
Comando: sunionstore pesquisa:produto_desconto pesquisa:produto pesquisa:desconto

![image](https://user-images.githubusercontent.com/78691172/175816022-b8a57d9b-aefd-4cba-be88-bb04eab73d3d.png)







##SETS ORDENADOS
###Primeiro vamos limpar a chave que já existe

1. Deletar a chave "pesquisa:produto"
Comando:del pesquisa:produto
![image](https://user-images.githubusercontent.com/78691172/175817088-cf376aae-699c-489b-a1a8-7fc35ffb5f60.png)

*O retorno 1 significa que foi deletado.

2. Criar a chave "pesquisa:produto" do tipo set ordenado com os seguintes valores:

Valor: monitor, Score: 100
Valor: HD, Score: 20
Valor: mouse, Score: 10
Valor: teclado, Score: 50
O score representa a quantidade de pesquisas feitas para aquele produto na aplicação

Comando: zadd pesquisa:produto 100 monitor 200 HD 10 mouse 50 teclado
![image](https://user-images.githubusercontent.com/78691172/175817287-07bc3496-0e5a-4676-aa63-5271851b9ad7.png)


1. Visualizar a quantidade de produtos

2. Visualizar todos os produtos do mais pesquisado ao menos pesquisado

3. Visualizar o rank do produto teclado

4. Visualizar o score do produto teclado

5. Remover o valor HD da chave

6. Recuperar e remover do set o produto mais pesquisado

7. Recuperar e remover do set o produto menos pesquisado

8. Visualizar todos os produtos


