### 4.1 Introdução a OOP

Em OOP, é importante identificar três características chaves de objetos:
- O **comportamento** do objeto: o que ele pode fazer e quais seus métodos.
- O **estado** do objeto, como ele reage quando são invocados os métodos
- A **identidade** do objeto, como ele se diferencia de outros que tem o mesmo comportamento e estado
Objetos que são instâncias de uma mesma classe compartilham uma semelhança já que suportam os mesmos comportamentos, sendo ele definido pelo métodos desse objeto.
O estado de um objeto muda ao longo do tempo, o que é feito por meio de seus métodos. Caso seu estado mude sem o uso deles, temos que o **encapsulamento** foi quebrado.

Apesar disso, o estado de um objeto não o define completamente, já que dois objetos do tipo **Pedido** podem ter o mesmo estado, porém tem **identidades diferentes**.  Ou seja, eles **sempre** diferem em sua identidade mas **usualmente** em seu estado. O estado de um objeto pode também influenciar seu comportamento, como por exemplo se o estado dele é **encaminhado** ou **pago** não é possível utilizar os métodos **remover** ou **adicionar**.
 Para identificar classes, é necessário olhar para seus substantivos e adjetivos. Substantivos normalmente são utilizados para descrever seu estado, enquanto adjetivos, seu comportamento.

Existem alguns tipos de relacionamentos possíveis entre classes:
- Dependência ("usa um")
	- Uma classe depende de outra se em seus métodos são manipulados objetos dessa classe, por exemplo, uma classe **Pedido** depende de Conta já que é necessário verificar se a pessoa tem limite disponível, mas o mesmo não acontece com **Item**.
	- É comum que a dependência seja diminuída em projetos, já que, caso a classe A não saiba da existência de B -- ou seja, não acompanha nenhum tipo de mudança em seu estado -- bugs são evitados em A.
		- Em terminologia de engenharia de software, você quer **minimizar** o *coupling* entre classes. 
- Agregação ("tem um")
	- Significa que um objeto **Ordem** contém **Item**, significando que objetos da classe A contenha objetos da classe B.
- Herança ("é um")
	- É uma relação especial, em que uma classe tem acesso ao comportamento de outra, permitindo que a classe herdada tenha também métodos específicos. **RushOrder** é uma classe que herda de **Order**, no sentido que ambas tem métodos de *adicionar* um pedido, mas **RushOrder** pode ter métodos que lidam de forma diferente em relação ao envio de pedidos de acordo com o nível de prioridade.
É comum programadores usarem diagramas UML para representar as relações entre classes. Um exemplo abaixo mostra isso:

<img width="600" height="400" src="https://i.imgur.com/PneKLxa.png" />

Cada flecha representa uma relação específica:

<img width="500" height="300" src="https://i.imgur.com/DwyUS6v.png" />

### 4.2 Usando classes predefinidas
