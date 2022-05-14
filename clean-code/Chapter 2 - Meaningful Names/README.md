## Chapter 2 - Meaningful Names



#### Usar nomes com intenções reveladas

Nomes tem que revelar intenções sobre o o que aquilo deve fazer. Eles devem responder todas as grandes perguntas sobre seu propósito: **por que existe**, **o que faz**, **e como é usado**. Se um **nome** precisa de um comentário para ser explicado, então ele não explica sua funcionalidade. Um exemplo abaixo:

```java
int d; // elapsed time in days
```

O nome *d* não revela name sobre sua intenção. Deveríamos escolher um nome que enfatiza o que é medido e a medida de tempo que é usada:

```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

#### Evitar desinformação

Outra preocupação que deve ser considerada quando escrevendo código é **evitar desinformação**. Um exemplo seria uma variável de nome *accountsList* que não é do tipo *List*. (Mais tarde será mostrado que mesmo se o container for um *List*, é melhor não dizê-lo no nome da variável). 

Outro problema são nomes que se diferenciam por poucos detalhes, como `XYZControllerForEfficientHandlingOfStrings` e `XYZControllerForEfficientStorageOfStrings`. Se ambos estivessem em partes distantes do código, o tempo para encontrar a diferença seria grande.



#### Fazer distinções significantes

Criar nomes de variáveis de forma que seja para evitar problemas com o compilador é comum - por exemplo, usar `klass` , já que `class` pode ser uma palavra reservada - se os nomes são diferentes, então eles devem significar coisas diferentes.

 No exemplo abaixo, podemos ver que usar os nomes origem e destino no lugar de `a1` e `a2` respectivamente, melhora a legibilidade do código.

```java
public static void copyChars(char a1[], char a2[]) {
    for (int i = 0; i < a1.length; i++) {
        a2[i] = a1[i]
    }
}
```

Palavras "barulhentas" são outro ponto importante a se tocar. Uma variável de nome `NameString` não é melhor do que somente `Name`. Como poderia um nome ser algo que não uma string?

#### Use nomes pronunciáveis

Se não é possível pronunciar uma variável, então discutir sobre seu funcionamento ou funcionalidade dificulta a comunicação com outros colegas, já que **programar é uma atividade social**. Discutir sobre o objeto `acnmb` que chama o método `fpdr` não faz sentido nenhum, mesmo que `acnmb` signifique "**A**luno **C**om **N**ota **M**uito **B**aixa" e `fpdr` seja "**F**azer **P**rova **D**e **R**ecuperação".

#### Nomes pesquisáveis

Nomes com uma letra ou constantes numéricas são problemáticas de se localizar dentro de um código. Podem ocorrer inúmeras repetições daquele caracter ao longo do arquivo. A preferência do Uncle Bob é utilizar nomes pequenos apenas em variáveis locais de métodos pequenos, ainda considerando que **o tamanho de um nome deve ser proporcional do seu escopo**.

#### Interfaces e Implementações

Suponha que você esteja escrevendo um *abstract factory* para a criação de formas. Ela é uma interface e é implementada por alguma classe. Seu nome deve ser `IShapeFactory` ou `ShapeFactory`?  Uncle Bob diz que prefere esconder o I e se for para mostrar ao usuário algo, que seja mostrar a classe como uma implementação, usando algo como `ShapeFactoryImpl`.

#### Evitar mapas mentais

Usar letras como nome de variáveis pode ser útil em loops, já que há uma conveção em usar `k` ou `j` como nome de contadores. Porém, lembrar que `r` significa uma url sem o host é um problema.

#### Nomes de Métodos e Classes

Classes devem ter em seus nomes apenas substantivos, enquanto métodos devem ter um verbo ou uma frase com verbo, como `postPayment` ou `deletePage`. Considerando o padrão javabean, devemos usar acessors, mutators e predicates com `get`, `set` e `is`, respectivamente.



#### Escolha uma palavra por conceito

Usar palavras diferentes para o mesmo significado pode ser problemático, como `retrive`, `get` ou `fetch` para métodos que tem a mesma ideia em classes diferentes.

Usando essa dica, é possível que muitos métodos tenham um mesmo nome. Isso é razoável para casos em que a assinatura do método é parecida assim como semanticamente iguais, porém, a consistência pode acabar resultando em um problema caso o método faça algo de diferente em uma outra classe. Por exemplo, se `add` adiciona ou concatena dois valores. Agora, criamos uma classe em que seu método `add` adiciona um novo valor à uma coleção. A semântica diferente entre esse método e os outros mostra que talvez ele deva ter um nome diferente, como `insert`.



#### Nomes de acordo com o domínio

Usar nomes considerando termos de ciência da computação pode ajudar no entendimento do código. `JobQueue` tem um grande significado para um programador, por exemplo. Quando não for possível usar um nome com algo desse tipo, a melhor abordagem é utilizar o nome de acordo com o porlbema que ele tenta resolver.




