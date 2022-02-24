
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

Em Java, temos diversas classes disponíveis de forma padrão, como por exemplo *Math* e *Date*. Classes precisam ser construídas e terem seu estado inicial especificado e isso é feito por meio de métodos contrutores.

Existem linguagens de programação como o Visual Basic que tem alguns desses tipos de forma *built-in*. Apesar de parecer uma melhor escolha na estrutura da linguagem, essa abordagem pode sofrer problemas, já que existem lugares em que as datas são representadas de outra forma. Com classes, caso isso acontecesse, os programadores podem se sentir livres para inserir comportamentos para surprir a falta de alguma funcionalidade.

Podemos instanciar uma classe utilizando a palavra chave **new**

<code id="first-code-block">Date date = new Date();</code> 

É importante definir a diferença entre *objetos* e *variáveis objetos*. Enquanto o primeiro é um objeto que foi instanciado utilizando **new**, como em [(1)](#first-code-block). O segundo é uma variável que tem apenas um tipo especifico e que pode ser atribuido a um outro objeto já instanciado:

```java
Date deadline;
s = deadline.toString() // erro
```

```java
Date deadline;
deadline = date;
s = deadline.toString(); // correto
```

O segundo bloco de código acima permite que deadline tenha acesso ao método *toString* já que ele foi atribuido a um objeto com classe *Date*.

Pode-se pensar em variáveis objetos como o funcionamento de ponteiros de objetos em C++, em que, ao serem atribuidos à algum objeto, ele é feito por referência, tendo suas propriedades copiadas, mas, caso uma mudança ocorra em `date`, ela também ocorrerá em `deadline`. Para realizar uma cópia sem referências, deve-se utilizar o método *clone*.

A classe *Date* do Java registra datas como um ponto específico no tempo, sendo em milissegundos que passaram desde 1 de janeiro de 1970 00:00:00 UTC. Apesar disso, não é dessa forma que humanos registram datas no dia a dia, e ele pode variar ao longo do mundo. Para isso, existe a classe *LocalDate*.

Objetos dessa classe não são instanciados, mas sim usados *factory methods* para chamar seus construtores. Podemos criar utilizando seus métodos diretamente

```java
LocalDate.now(); // retorna uma data com a data em que o objeto foi criado
LocalDate local = LocalDate.of(1999, 12, 31); 
// retorna data específica que foi fornecida em seus parâmetros
```


