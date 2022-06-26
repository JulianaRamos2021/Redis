![image](https://user-images.githubusercontent.com/78691172/174131694-2befa329-c6ba-4f7a-829b-4ad453781097.png)


# Criando e configurando banco de dados Redis

Redis é um servidor de estruturas de dados chave-valor que fornece suporte a diferentes tipos de valores. Indicado para aplicações com alta exigência de resposta rápida e processamento dinâmico. Aceita estruturas mais complexas como string, listas, sets, sets ordenados, streams, hyperloglogs e hash.
É indicado o uso de chaves simples com no máximo 1 MB. É indicado instanciar as chaves e evitar abreviações, exemplo de chave adequada: "object-type:id".



## Exercícios -SETS

#### 1. Deletar a chave “pesquisa:produto”  
Comando: del pesquisa:produto


![image](https://user-images.githubusercontent.com/78691172/175814955-90453912-4cab-43b2-b830-60d20e9d87d0.png)

*O zero significa que a chave não existe, se o resultado for 1 então a chave foi deletada.




#### 2. Criar a chave "pesquisa:produto" do tipo set com os seguintes valores: monitor, mouse e teclado

Comando: sadd pesquisa:produto monitor mouse teclado

![image](https://user-images.githubusercontent.com/78691172/175815037-4d848ade-2010-433c-9e2d-8a260b3b09e0.png)  


#### 3. Visualizar a quantidade de valores da chave

Comando: scard pesquisa:produto

![image](https://user-images.githubusercontent.com/78691172/175815068-0541baa3-4d32-4155-94df-424cbeae2404.png)  

#### 4. Retornar todos os elementos da chave

Comando: smembers pesquisa:produto

![image](https://user-images.githubusercontent.com/78691172/175815210-c46e1b30-dff5-4e35-bd23-2f7e2a35ec6c.png)  

#### 5. Verificar se existe o valor monitor

Comando: sismember pesquisa:produto monitor

![image](https://user-images.githubusercontent.com/78691172/175815280-3c8415a2-def1-4588-a835-cac5701fbc68.png)

*O retorno 1 significa que o valor existe, retorno 0 significa que não existe.  

#### 6. Remover o valor monitor

Comando: srem pesquisa:produto monitor

![image](https://user-images.githubusercontent.com/78691172/175815350-fcf5e656-b273-487c-b449-1731c26c27b6.png)

*Retorno 1 significa que o valor foi excluído.  

#### 7. Recuperar um elemento e remove-lo do set

Comando: spop pesquisa:produto

![image](https://user-images.githubusercontent.com/78691172/175815545-6e0daccc-69c1-4891-917d-8fc74174137f.png)  


#### 8. Criar a chave "pesquisa:desconto“ do tipo set com os seguintes valores: memória RAM, monitor, teclado, HD

Comando: sadd pesquisa:desconto 'memoria RAM' monitor teclado HD

![image](https://user-images.githubusercontent.com/78691172/175815616-808fb3d1-59f4-4ab0-a68a-2050deae244e.png)  

#### 9. Próximas questões fazem uso dos sets pesquisa:produto e pesquisa:desconto

#####Visualizar a interseção entre os 2 sets

Comando: sinter pesquisa:produto pesquisa:desconto

![image](https://user-images.githubusercontent.com/78691172/175815745-d813a691-7643-4a17-9f94-6cad356b1385.png)

*No meu resultado não foi gerada interseção pois não existem valores iguais dentro das chaves.  


#####Visualizar a diferença entre os 2 sets

Comando:sdiff pesquisa:produto pesquisa:desconto

![image](https://user-images.githubusercontent.com/78691172/175815832-97f41c6a-594f-462b-b79d-f3f6e448d5ba.png)  


#####Criar o set "pesquisa:produto_desconto" com a união entre os 2 sets

Comando: sunionstore pesquisa:produto_desconto pesquisa:produto pesquisa:desconto

![image](https://user-images.githubusercontent.com/78691172/175816022-b8a57d9b-aefd-4cba-be88-bb04eab73d3d.png)    







## Exercícios SETS ORDENADOS

### Primeiro vamos limpar a chave que já existe e criar uma nova

#### 1. Deletar a chave "pesquisa:produto"

Comando:del pesquisa:produto

![image](https://user-images.githubusercontent.com/78691172/175817088-cf376aae-699c-489b-a1a8-7fc35ffb5f60.png)

*O retorno 1 significa que foi deletado.  

#### 2. Criar a chave "pesquisa:produto" do tipo set ordenado com os seguintes valores:

Valor: monitor, Score: 100
Valor: HD, Score: 20
Valor: mouse, Score: 10
Valor: teclado, Score: 50
O score representa a quantidade de pesquisas feitas para aquele produto na aplicação

#### Comando: zadd pesquisa:produto 100 monitor 200 HD 10 mouse 50 teclado

![image](https://user-images.githubusercontent.com/78691172/175817287-07bc3496-0e5a-4676-aa63-5271851b9ad7.png)    


### Agora podemos iniciar
1. Visualizar a quantidade de produtos

Comando: zcard pesquisa:produto

![image](https://user-images.githubusercontent.com/78691172/175817530-141cbe9c-e89e-410d-a7c5-bc272ee864a6.png)  

#### 2. Visualizar todos os produtos do mais pesquisado ao menos pesquisado

Comando: zrevrange pesquisa:produto 0 -1

![image](https://user-images.githubusercontent.com/78691172/175817631-0bcc4af1-6da8-4abb-8ac9-523c548a8302.png)  


#### 3. Visualizar o rank do produto teclado

Comando: zrevrank pesquisa:produto teclado

![image](https://user-images.githubusercontent.com/78691172/175817690-81efc296-cbe7-460b-a77e-db45a0aaeac7.png)  

#### 4. Visualizar o score do produto teclado

Comando: zscore pesquisa:produto teclado

![image](https://user-images.githubusercontent.com/78691172/175817756-88949cc3-a979-4699-99eb-3bda52ccf0b2.png)  

#### 5. Remover o valor HD da chave

Comando:  zrem pesquisa:produto HD

![image](https://user-images.githubusercontent.com/78691172/175817796-df8f4924-548d-4fc9-948e-e3c62cc1e72f.png)

*O resultado 1 significa que foi removido.  

#### 6. Recuperar e remover do set o produto mais pesquisado

Comando:  zpopmax pesquisa:produto  

![image](https://user-images.githubusercontent.com/78691172/175817869-3a983813-a5be-4a93-928f-d96620fcfb3c.png)  

#### 7. Recuperar e remover do set o produto menos pesquisado

Comando: zpopmin pesquisa:produto

![image](https://user-images.githubusercontent.com/78691172/175817925-c6ddc700-1fd2-40f3-b543-2c3ed75ff648.png)  

#### 8. Visualizar todos os produtos

Comando: zrange pesquisa:produto -1 0

![image](https://user-images.githubusercontent.com/78691172/175817997-9cae67dd-eef0-42d8-89e0-99ca76e7c115.png)    





## Exercícios Hashes

#### 1. Deletar a chave “usuario:100”

Comando: del usuario:100

![image](https://user-images.githubusercontent.com/78691172/175825776-ba69e419-0341-4d93-a76c-ca88e9a149a4.png)  


* O resultado zero significa que a chave não foi deletada, isso ocorreu devido ela não existir.

#### 2. Criar uma chave “usuario:100” do tipo hash com a seguinte estrutura

nome – Augusto
estado – SP
views – 10

Comando: hmset usuario:100 nome Augusto estado SP views 10

![image](https://user-images.githubusercontent.com/78691172/175825838-dd6eb6fe-0213-4e3a-9d4a-c015181cf924.png)  

#### 3. Visualizar todas as chaves e valores

Comando: hgetall usuario:100

![image](https://user-images.githubusercontent.com/78691172/175825900-d7818225-610a-43aa-9a8a-7a17dfa43e5d.png)  

#### 4. Contar a quantidade de campos

Comando: hlen usuario:100

![image](https://user-images.githubusercontent.com/78691172/175825964-1ee97e4f-93c6-428d-9d98-e16efd885278.png)  

#### 5. Visualizar apenas o nome e views

Comando:  hmget usuario:100 nome views

![image](https://user-images.githubusercontent.com/78691172/175826047-ee02f2fa-1658-4a98-95ec-7469de2629fc.png)  

#### 6. Contar o tamanho do valor do campo nome

Comando: hstrlen usuario:100 nome

![image](https://user-images.githubusercontent.com/78691172/175826120-49d56305-4a14-42b7-949a-f77e4b50068e.png)  


#### 7. Incrementar em 2 o valor do campo views

Comando:  hincrby usuario:100 views 2

![image](https://user-images.githubusercontent.com/78691172/175826840-24ab42a5-6628-4b70-8a31-a7584fb11be7.png)

#### 8. Visualizar apenas os campos

Comando: hkeys usuario:100

![image](https://user-images.githubusercontent.com/78691172/175826917-0dedb9ad-b151-46f1-a9dc-aa1a1e60a63e.png)


#### 9. Visualizar apenas os valores

Comando: hvals usuario:100

![image](https://user-images.githubusercontent.com/78691172/175827012-af661ab4-f6a1-454a-bd8d-1536b1b15f1e.png)

#### 10. Deletar o campo estado

Comando: hdel usuario:100 estado

![image](https://user-images.githubusercontent.com/78691172/175827068-d669442a-1d42-402a-bb8b-3cba747276e2.png)




## Exercícios Publish e Subscribe

#### 1. Criar um assinante para receber as mensagens do canal noticias:sp

Comando: subscribe noticias:sp

![image](https://user-images.githubusercontent.com/78691172/175828847-a775f6ae-7080-4c27-b849-acac7d310849.png)


#### 2. Criar um editor para enviar as seguintes mensagens no canal noticias:sp

Msg 1  
Msg 2  
Msg 3  

Comando: publish noticias:sp 'Msg 1'  
publish noticias:sp 'Msg 2'  
publish noticias:sp 'Msg 3'  

![image](https://user-images.githubusercontent.com/78691172/175829025-3984b477-1b0b-4d4d-b72f-f5dbcfa9e4a5.png)


#### 3. Cancelar o assinante do canal noticias:sp
CTRL + C

#### 4. Criar um assinante para receber as mensagens dos canais com o padrão noticias:*

Comando:psubscribe noticias:*

![image](https://user-images.githubusercontent.com/78691172/175829330-bff07a18-a2ae-42b2-9e7e-030df941a7fa.png)

#### 5. Criar um editor para enviar as seguintes mensagens no canal noticias:rj

Msg 4  
Msg 5  
Msg 6  

Comando: publish noticias:rj 'Msg 4'
publish noticias:rj 'Msg 5'
publish noticias:rj 'Msg 6'


![image](https://user-images.githubusercontent.com/78691172/175829448-2597f7be-ea80-4615-804d-6b8c24469a68.png)

