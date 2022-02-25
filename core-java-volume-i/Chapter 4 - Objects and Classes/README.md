### 4.1 Introdução a OOP

Em OOP, é importante identificar três características chaves de objetos:

- O **comportamento** do objeto: o que ele pode fazer e quais seus métodos.
- O **estado** do objeto: como ele reage quando são invocados os métodos
- A **identidade** do objeto: como ele se diferencia de outros que tem o mesmo comportamento e estado
  Objetos que são instâncias de uma mesma classe compartilham uma semelhança já que suportam os mesmos comportamentos, sendo ele definido pelo métodos desse objeto.
  O estado de um objeto muda ao longo do tempo, o que é feito por meio de seus métodos. Caso seu estado mude sem o uso deles, temos que o **encapsulamento** foi quebrado.

Apesar disso, o estado de um objeto não o define completamente, já que dois objetos do tipo **Pedido** podem ter o mesmo estado, porém tem **identidades diferentes**. Ou seja, eles **sempre** diferem em sua identidade mas **usualmente** em seu estado. O estado de um objeto pode também influenciar seu comportamento, como por exemplo se o estado dele é **encaminhado** ou **pago** não é possível utilizar os métodos **remover** ou **adicionar**.
Para identificar classes, é necessário olhar para seus substantivos e adjetivos. Substantivos normalmente são utilizados para descrever seu estado, enquanto adjetivos, seu comportamento.

Existem alguns tipos de relacionamentos possíveis entre classes:

- Dependência ("usa um")
  - Uma classe depende de outra se em seus métodos são manipulados objetos dessa classe, por exemplo, uma classe **Pedido** depende de Conta já que é necessário verificar se a pessoa tem limite disponível, mas o mesmo não acontece com **Item**.
  - É comum que a dependência seja diminuída em projetos, já que, caso a classe A não saiba da existência de B -- ou seja, não acompanha nenhum tipo de mudança em seu estado -- bugs são evitados em A.
    - Em terminologia de engenharia de software, você quer **minimizar** o _coupling_ entre classes.
- Agregação ("tem um")
  - Significa que um objeto **Ordem** contém **Item**, significando que objetos da classe A contenha objetos da classe B.
- Herança ("é um") - É uma relação especial, em que uma classe tem acesso ao comportamento de outra, permitindo que a classe herdada tenha também métodos específicos. **RushOrder** é uma classe que herda de **Order**, no sentido que ambas tem métodos de _adicionar_ um pedido, mas **RushOrder** pode ter métodos que lidam de forma diferente em relação ao envio de pedidos de acordo com o nível de prioridade.
  É comum programadores usarem diagramas UML para representar as relações entre classes. Um exemplo abaixo mostra isso:

<img width="600" height="400" src="https://i.imgur.com/PneKLxa.png" />

Cada flecha representa uma relação específica:

<img width="500" height="300" src="https://i.imgur.com/DwyUS6v.png" />

### 4.2 Usando classes predefinidas

Em Java, temos diversas classes disponíveis de forma padrão, como por exemplo _Math_ e _Date_. Classes precisam ser construídas e terem seu estado inicial especificado e isso é feito por meio de métodos contrutores.

Existem linguagens de programação como o Visual Basic que tem alguns desses tipos de forma _built-in_. Apesar de parecer uma melhor escolha na estrutura da linguagem, essa abordagem pode sofrer problemas, já que existem lugares em que as datas são representadas de outra forma. Com classes, caso isso acontecesse, os programadores podem se sentir livres para inserir comportamentos para surprir a falta de alguma funcionalidade.

Podemos instanciar uma classe utilizando a palavra chave **new**

<code id="first-code-block">Date date = new Date();</code>

É importante definir a diferença entre _objetos_ e _variáveis objetos_. Enquanto o primeiro é um objeto que foi instanciado utilizando **new**, como em [(1)](#first-code-block). O segundo é uma variável que tem apenas um tipo especifico e que pode ser atribuido a um outro objeto já instanciado:

```java
Date deadline;
s = deadline.toString() // erro
```

```java
Date deadline;
deadline = date;
s = deadline.toString(); // correto
```

O segundo bloco de código acima permite que deadline tenha acesso ao método _toString_ já que ele foi atribuido a um objeto com classe _Date_.

Pode-se pensar em variáveis objetos como o funcionamento de ponteiros de objetos em C++, em que, ao serem atribuidos à algum objeto, ele é feito por referência, tendo suas propriedades copiadas, mas, caso uma mudança ocorra em `date`, ela também ocorrerá em `deadline`. Para realizar uma cópia sem referências, deve-se utilizar o método _clone_.

A classe _Date_ do Java registra datas como um ponto específico no tempo, sendo em milissegundos que passaram desde 1 de janeiro de 1970 00:00:00 UTC. Apesar disso, não é dessa forma que humanos registram datas no dia a dia, e ele pode variar ao longo do mundo. Para isso, existe a classe _LocalDate_.

Objetos dessa classe não são instanciados, mas sim usados _factory methods_ para chamar seus construtores. Podemos criar utilizando seus métodos diretamente

```java
LocalDate.now(); // retorna uma data com a data em que o objeto foi criado
LocalDate local = LocalDate.of(1999, 12, 31);
// retorna data específica que foi fornecida em seus parâmetros
```

Se chamarmos o método _plusDays_ em `local`, o Java irá criar um novo objeto _LocalDate_, e deixar o antigo valor de local intocado. Isso é conhecido como um método que **não altera** o estado do objeto, mas cria outro em seu lugar para que a alteração ocorra.

```java
local.plusDays(1000); // não é alterado
LocalDate someDay = local.plusDays(1000) // novo valor é salvo na variável someDay
```

Existem métodos que podem alterar o estado do objeto ao serem chamados, como os da antiga classe GregorianCalendar, em que o método _add_ substitui o valor antigo do objeto.

```java
GregorianCalendar newDay = new GregorianCalendar(1999, 12, 31);
newDay.add(Calendar.DAY_OF_MONTH, 1000);
int year = newDay.get(Calendar.YEAR) // 2002
int month = newDay.get(Calendar.MONTH) + 1; // 09
int day = newDay.get(Calendar.DAY_OF_MONTH); // 26
```

### 4.4 Campos Estáticos e Métodos

Podemos usar métodos e atributos estáticos quando desejamos que uma característica da classe seja compartilhado com todas as suas instâncias. Por exemplo, usando a classe Empregado:

```java
public class Employee {
  private int id;
  private static int nextId = 1;

  public Employee() {
    this.id = this.nextId;
    this.nextId++;
  }

  public getNextId() {
    return nextId;
  }
}

Employee employee1 = new Employee(); // id = 1
Employee employee2 = new Employee(); // id = 2
```

Atributos estáticos também podem ser acessados sem a necessidade da classe ser instanciada:

```java
public class Math {
  public static final double PI = 3.14159265358979323846;
}

System.out.println(Math.PI); // 3.14159265358979323846;
```

Apesar de não ser uma boa prática utilizar atributos com visibildade pública, esse caso não há nenhum problema por que PI é uma constante.
Assim como os atributos estáticos não podem ser usados por objetos, mas somente pelas suas classes, e não podem acessar atributos de objetos (ou seja, aqueles que são chamados usando o `this` dentro do objeto. Ainda assim, é possível usar métodos estáticos em instâncias de classes. Um exemplo de um método estático é o método pow da classe Math:

```java
Math.pow(2, 2) // retorna 4
```

As situações mais favoráveis para se utilizar métodos estáticos são:

- Não é necessário que haja parâmetros implicitos na chamada dele
  - `Math.pow(x, y)`
- O método só precisa de acesso à atributos estáticos
  - `Employee.getNextId()`

_Factory methods_ são métodos estáticos que instanciam um objeto sem a necessidade do uso de um construtor.

```java
NumberFormat currentFormat = NumberFormat.getCurrencyInstance();
NumberFormat percentFormat = NumberFormat.getPercentInstance();

double x = 0.1;
currentFormat.format(x); // $0.10
percentFormat.format(x); // 10%
```

A vantagem de se usar um _factory method_ é que podemos dar nomes aos construtores e inclusive utilizar outros tipos na hora de instanciar uma classe. Quando `getCurrencyInstance` e `getPercentInstance` são usados, eles retornam objetos da classe `DecimalFormat`, que herda de `NumberFormat`.

Métodos estáticos são utilizados antes mesmo de um programa em Java começar a ser executado. O método `main` é estático e permite que o programa seja iniciado mesmo sem ter um objeto para executá-lo, e a partir dele que o programa constrói todos os objetos necessários para seu funcionamento.

É possível que qualquer classe tenha um método estático `main` e ele seja executado, o que permite que testes unitários sejam feitos sem utilizar ferramentas como o JUnit (não que seja o recomendado, apenas que é possível). Adicionando esse método à classe Employee vista anteriormente, temos:

```java

class Employee {
  // implementação feita antes
  public static void main(String[] args) { // teste unitário
    var e = new Employee("Romeo", 50000, 2003, 3, 31);
    e.raiseSalary(10);
    System.out.println(e.getName() + " " + e.getSalary());
  }
}
```

Para aplicarmos esse teste unitário, podemos iniciar o programa pela classe `Employee`.

### 4.5 Parâmetros de Métodos

Em Java, só podemos passar por valor em parâmetros de métodos, diferente de C++ aonde é possível utilizar a passagem por referência.

```java
public static void tripleValue(double x) {
  x = 3 * x;
}
double x = 10;
tripleValue(x);
```

Ao chamar o método `tripleValue`, o valor de x fora da função continua sendo 10, e é apenas durante a execução desse método que seu valor é triplicado.
No caso de valores primitivos, temos que eles nunca são alterados quando passados por meio do parâmetros. Porém, isso muda quando são usados objetos:

```java
public static void tripleSalary(Employee x) {
  x.raiseSalary(200);
}

Employee harry = new Employee(...);
tripleSalary(harry);
```

Agora, após o termino do método, o salário de harry é aumentado, já que `x` ainda continua fazendo referência ao objeto `harry`, mesmo que ele tenha sido passado como um parâmetro do método `tripleSalary`.
Ainda assim, temos que o Java nunca passa valores por refêrencia. O exemplo abaixo mostra isso:

```java
public static void swap(Employee x, Employee y) {
  Employee temp = x;
  x = y;
  y = temp;
}

var a = new Employee("Alice", ...);
var b = new Employee("Bob", ...);
swap(a, b);
```

Apesar de serem passados os objetos, quando o método termina, a continua sendo _Alice_ e b _Bob_. Quando esses objetos são passados para o método `swap`, é feito uma cópia das referências deles.

Durante o funcionamento do método, eles são trocados entre x e y, porém essas variáveis são abandonadas. Ou seja, o Java não usa passagem por referência, mas sim, é passado uma cópia da referência desse objeto.

<img src="https://i.imgur.com/CAlGoZX.png">

### 4.6 Construção de Objetos
