<div align="center">
  <h3>🚧 Material em Construção 🚧</h3>
</div>

# Padrões de Projeto

Este repositório é dedicado ao estudo e exploração dos padrões de projeto utilizados no desenvolvimento de software. Aqui, você encontrará informações baseadas no meu entendimento pessoal sobre o tema.

No entanto, é importante ressaltar que, apesar dos meus melhores esforços, podem ocorrer equívocos ou interpretações diferentes. Se você identificar algum erro ou tiver alguma sugestão de melhoria, por favor, informe-me. Estou sempre aberta a correções e aprecio contribuições para aprimorar o conteúdo disponibilizado aqui.

Agradeço pela sua compreensão e espero que as informações fornecidas sejam úteis em seu estudo sobre os padrões de projeto.

## Principais Tópicos Abordados

- Padrões de projeto criacionais
- Padrões de projeto estruturais
- Padrões de projeto comportamentais

## Exemplos em Kotlin

Neste repositório, você encontrará exemplos práticos dos padrões de projeto implementados em Kotlin. Os exemplos foram desenvolvidos de forma a facilitar o entendimento e demonstrar a aplicação dos padrões em situações reais.

## Padrões de Projeto

A seguir, são apresentados os principais padrões de projeto abordados neste repositório:

## Padrões de Criação: Factory Method

O padrão Factory Method é um dos padrões de projeto criacionais mais utilizados. Ele fornece uma maneira de criar objetos sem especificar explicitamente a classe exata do objeto que será criado. Em vez disso, o Factory Method define uma interface para criar objetos, delegando a decisão de qual classe concreta utilizar para as subclasses.

### Contexto

Imagine que você esteja desenvolvendo um aplicativo para um jogo de RPG. No jogo, existem vários tipos de personagens, como guerreiros, magos e arqueiros. Cada personagem tem suas próprias características e habilidades específicas.

### Problema

Você precisa criar uma maneira flexível de instanciar objetos de personagens diferentes. No entanto, criar cada personagem diretamente usando o operador `new` em todo o código do jogo resultaria em um acoplamento forte entre as classes do jogo e as classes de personagens.

### Solução

Nesta solução, utilizamos o Factory Method para criar objetos de personagens em um jogo de RPG. Primeiro, definimos a interface `Personagem`, que possui os métodos `habilidades()` e `atacar()`. Em seguida, criamos a classe abstrata `PersonagemFactory`, que declara o método abstrato `criarPersonagem()`. As subclasses concretas dessa classe, como `GuerreiroFactory` e `MagoFactory`, implementam o Factory Method, retornando instâncias de `Guerreiro` e `Mago`, respectivamente.

Ao utilizar o Factory Method, o código do jogo pode criar personagens chamando `criarPersonagem()` na fábrica correspondente, sem precisar se preocupar com a classe concreta específica do personagem. Dessa forma, o Factory Method desacopla a criação de objetos da lógica principal do código, permitindo a extensibilidade e flexibilidade ao adicionar novos tipos de personagens.

### Exemplo em Kotlin

```kotlin
interface Personagem{
    fun habilidades()
    fun atacar()
}

abstract class PersonagemFactory{
    abstract fun criarPersonagem() : Personagem

}

class Guerreiro : Personagem{
    override fun habilidades() {
        println("Guerreiro possui força e resistência física elevadas.")
    }

    override fun atacar() {
        println("Guerreiro ataca com sua espada poderosa.")
    }

}

class Mago : Personagem{
    override fun habilidades() {
        println("Mago possui habilidades mágicas e pode conjurar feitiços poderosos.")
    }

    override fun atacar() {
        println("Mago ataca com feitiços arcanos devastadores.")
    }

}

class GuerreiroFactory : PersonagemFactory() {
    override fun criarPersonagem(): Personagem {
        return Guerreiro()
    }

}

class MagoFactory: PersonagemFactory(){
    override fun criarPersonagem(): Personagem {
        return Mago()
    }
}

fun main(){
    val fabricaGuerreiro: PersonagemFactory = GuerreiroFactory()
    val guerreiro: Personagem = fabricaGuerreiro.criarPersonagem()
    guerreiro.habilidades()
    guerreiro.atacar()

    val fabricaMago: PersonagemFactory = MagoFactory()
    val mago: Personagem = fabricaMago.criarPersonagem()
    mago.habilidades()
    mago.atacar()
}
```

No exemplo em Kotlin, utilizamos as classes `Guerreiro` e `Mago` como subclasses concretas de `Personagem`, cada uma implementando os métodos `habilidades()` e `atacar()` de acordo com suas características. As classes `GuerreiroFactory` e `MagoFactory` estendem `PersonagemFactory` e implementam o método `criarPersonagem()`, retornando as instâncias correspondentes de `Guerreiro` e `Mago`.

No código de exemplo, criamos uma instância de `Guerreiro` utilizando a fábrica `GuerreiroFactory`, chamamos seus métodos e, em seguida, repetimos o processo para `Mago` utilizando a fábrica `MagoFactory`. Dessa forma, podemos criar personagens sem nos preocupar com a implementação concreta, apenas utilizando a interface `Personagem` e a fábrica correspondente.

**Benefícios do Factory Method:**
- Desacopla o código que cria objetos do código que os utiliza.
- Permite a adição de novos tipos de objetos sem modificar o código existente.
- Promove a consistência na criação de objetos em todo o sistema.
- Facilita a aplicação do princípio da inversão de dependência.

Observação: Essa é uma explicação básica do padrão Factory Method. É importante estudar mais sobre o assunto e considerar outros aspectos e possibilidades ao aplicar o padrão em diferentes contextos.

## Padrões de Criação: Abstract Factory

O padrão Abstract Factory é um padrão de projeto criacionais que fornece uma interface para criar famílias de objetos relacionados sem especificar suas classes concretas. Ele permite que você crie objetos de várias classes relacionadas sem acoplar o código cliente às classes específicas desses objetos.

### Contexto

Imagine que estamos lidando com a criação de carros e seus componentes. Existem diferentes tipos de carros, como carros esportivos, carros familiares e carros de luxo. Cada tipo de carro possui um conjunto específico de componentes, como motor, roda e assento.

### Problema

O problema é que precisamos criar diferentes famílias de objetos de carros sem acoplar o código cliente às classes concretas desses objetos. Além disso, desejamos garantir que os componentes de um determinado carro sejam compatíveis e pertençam à mesma família.

### Solução

O padrão Abstract Factory aborda esse problema fornecendo uma interface chamada `CarFactory`, que declara métodos para criar cada componente do carro, como `createEngine()`, `createWheel()` e `createSeat()`. Essa interface é implementada por diferentes classes concretas, como `SportsCarFactory`, `FamilyCarFactory` e `LuxuryCarFactory`, que são responsáveis por criar componentes de carros específicos.

Cada classe concreta de fábrica, como `SportsCarFactory`, implementa os métodos da `CarFactory` para criar componentes específicos de carros esportivos, como `SportsEngine`, `SportsWheel` e `SportsSeat`. Da mesma forma, as classes `FamilyCarFactory` e `LuxuryCarFactory` criam componentes de carros familiares e de luxo, respectivamente.

Ao utilizar o padrão Abstract Factory, podemos criar diferentes famílias de objetos de carros chamando os métodos apropriados da fábrica correspondente. Isso garante que os componentes criados pertençam à mesma família e sejam compatíveis entre si.

### Exemplo em Kotlin

```kotlin
// Interfaces de componentes de carro
interface Engine {
    override fun toString(): String
}

interface Wheel {
    override fun toString(): String
}

interface Seat {
    override fun toString(): String
}

// Interface da fábrica de carros
interface CarFactory {
    fun createEngine(): Engine
    fun createWheel(): Wheel
    fun createSeat(): Seat
}

// Implementações de componentes para carros esportivos
class SportsEngine : Engine {
    override fun toString(): String {
        return "Sports Engine"
    }
}

class SportsWheel : Wheel {
    override fun toString(): String {
        return "Sports Wheel"
    }
}

class SportsSeat : Seat {
    override fun toString(): String {
        return "Sports Seat"
    }
}

// Implementações de componentes para carros familiares
class FamilyEngine : Engine {
    override fun toString(): String {
        return "Family Engine"
    }
}

class FamilyWheel : Wheel {
    override fun toString(): String {
        return "Family Wheel"
    }
}

class FamilySeat : Seat {
    override fun toString(): String {
        return "Family Seat"
    }
}

// Implementações de componentes para carros de luxo
class LuxuryEngine : Engine {
    override fun toString(): String {
        return "Luxury Engine"
    }
}

class LuxuryWheel : Wheel {
    override fun toString(): String {
        return "Luxury Wheel"
    }
}

class LuxurySeat : Seat {
    override fun toString(): String {
        return "Luxury Seat"
    }
}

// Fábrica de carros esportivos
class SportsCarFactory : CarFactory {
    override fun createEngine(): Engine {
        return SportsEngine()
    }

    override fun createWheel(): Wheel {
        return SportsWheel()
    }

    override fun createSeat(): Seat {
        return SportsSeat()
    }
}

// Fábrica de carros familiares
class FamilyCarFactory : CarFactory {
    override fun createEngine(): Engine {
        return FamilyEngine()
    }

    override fun createWheel(): Wheel {
        return FamilyWheel()
    }

    override fun createSeat(): Seat {
        return FamilySeat()
    }
}

// Fábrica de carros de luxo
class LuxuryCarFactory : CarFactory {
    override fun createEngine(): Engine {
        return LuxuryEngine()
    }

    override fun createWheel(): Wheel {
        return LuxuryWheel()
    }

    override fun createSeat(): Seat {
        return LuxurySeat()
    }
}

// Função para criar um carro usando a fábrica
fun createCar(carFactory: CarFactory) {
    val engine = carFactory.createEngine()
    val wheel = carFactory.createWheel()
    val seat = carFactory.createSeat()

    println("Engine: $engine")
    println("Wheel: $wheel")
    println("Seat: $seat")
}

fun main() {
    val sportsFactory: CarFactory = SportsCarFactory()
    createCar(sportsFactory)

    val familyFactory: CarFactory = FamilyCarFactory()
    createCar(familyFactory)

    val luxuryFactory: CarFactory = LuxuryCarFactory()
    createCar(luxuryFactory)
}
```

No exemplo acima, temos as seguintes características do padrão Abstract Factory:

- Interfaces `Engine`, `Wheel` e `Seat` representam diferentes componentes de carros.
- A interface `CarFactory` declara os métodos para criar cada componente.
- As classes concretas, como `SportsEngine`, `SportsWheel` e `SportsSeat`, implementam as interfaces correspondentes para carros esportivos, assim como temos implementações para carros familiares e de luxo.
- As classes concretas de fábrica, como `SportsCarFactory`, `FamilyCarFactory` e `LuxuryCarFactory`, implementam a interface `CarFactory` e fornecem implementações para criar componentes de carros específicos.
- A função `createCar` recebe uma instância de `CarFactory` e usa essa fábrica para criar um conjunto de componentes de carro, imprimindo seus detalhes.
- No método `main`, são criadas instâncias de `SportsCarFactory`, `FamilyCarFactory` e `LuxuryCarFactory`, chamando a função `createCar` para cada uma delas, permitindo criar carros esportivos, carros familiares e carros de luxo com seus respectivos componentes.

**Benefícios do Abstract Factory**

- Desacopla o código cliente das classes concretas dos objetos criados.
- Permite a criação de famílias de objetos relacionados sem especificar suas classes concretas.
- Garante a compatibilidade dos objetos criados dentro de uma família.
- Facilita a adição de novas famílias de objetos sem modificar o código existente.

Observação: Essa é uma explicação básica do padrão Abstract Factory. É importante estudar mais sobre o assunto e considerar outros aspectos e possibilidades ao aplicar o padrão em diferentes contextos.

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
