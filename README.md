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

## Sumário

- [Padrões de Criação: Factory Method](#padrões-de-criação-factory-method)
- [Padrões de Criação: Abstract Factory](#padrões-de-criação-abstract-factory)
- [Padrões de Criação: Builder](#padrões-de-criação-builder)
- [Padrões de Criação: Singleton](#padrões-de-criação-singleton)
- [Padrões de Criação: Prototype](#padrões-de-criação-prototype)
- [Padrões de Estrutura: Adapter](#padrões-de-estrutura-adapter)
- [Padrões de Estrutura: Bridge](#padrões-de-estrutura-bridge)

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

## Padrões de Criação: Builder
O padrão Builder é um padrão de projeto criacional que permite a construção de objetos complexos passo a passo. Ele separa o processo de construção do objeto final da sua representação, permitindo que o mesmo processo de construção possa criar diferentes representações do objeto.

### Contexto
Imagine que você esteja desenvolvendo um sistema para construir casas com diferentes estilos arquitetônicos, como casas modernas e casas rústicas. Cada tipo de casa tem características específicas, como área, número de quartos, número de banheiros e presença ou ausência de garagem.

### Problema
Você precisa criar objetos de casas com diferentes estilos e especificações de forma flexível. No entanto, a criação direta dos objetos de casa em todo o código resultaria em um código complexo e pouco legível.

### Solução
Nesta solução, utilizamos o padrão Builder para construir objetos de casas com diferentes estilos arquitetônicos. Primeiro, definimos a interface `Builder`, que possui métodos para definir as características da casa, como `setArea()`, `setNumeroQuartos()`, `setNumeroBanheiros()` e `setGaragem()`. As classes `CasaModernaBuilder` e `CasaRusticaBuilder` implementam a interface `Builder`, permitindo a criação de casas modernas e casas rústicas, respectivamente.

A classe `Diretor` é responsável por dirigir o processo de construção de casas, utilizando um determinado tipo de builder. Ele define métodos como `construirCasaModerna()` e `construirCasaRustica()`, que utilizam os métodos do builder para definir as características da casa e retornar o objeto final.

Ao utilizar o padrão Builder, o código principal pode criar casas chamando os métodos do builder apropriado, sem se preocupar com a lógica detalhada de construção da casa. Dessa forma, o padrão Builder permite a construção passo a passo de objetos complexos, com diferentes combinações de características, mantendo o código limpo e legível.


### Exemplo em Kotlin
```kotlin
class CasaModerna(
    var area: Int = 0,
    var numeroQuartos: Int = 0,
    var numeroBanheiros: Int = 0,
    var garagem: Boolean = false
){
    fun result(): String{
        return "Casa moderna: área = $area m², número de quartos = $numeroQuartos, número de banheiros = $numeroBanheiros, garagem = $garagem"
    }
}

class CasaRustica(
    var area: Int = 0,
    var numeroQuartos: Int = 0,
    var numeroBanheiros: Int = 0,
    var garagem: Boolean = false
){
    fun result(): String{
        return "Casa rústica: área = $area m², número de quartos = $numeroQuartos, número de banheiros = $numeroBanheiros, garagem = $garagem"
    }
}

interface Builder{
    fun setArea(area: Int): Builder
    fun setNumeroQuartos(numeroQuartos: Int): Builder
    fun setNumeroBanheiros(numeroBanheiros: Int): Builder
    fun setGaragem(garagem: Boolean): Builder
    fun build(): Any
}

class CasaModernaBuilder() : Builder{

    private var casa: CasaModerna = CasaModerna()
    override fun setArea(area: Int): Builder {
        casa.area = area
        return this
    }

    override fun setNumeroQuartos(numeroQuartos: Int): Builder {
        casa.numeroQuartos = numeroQuartos
        return this
    }

    override fun setNumeroBanheiros(numeroBanheiros: Int): Builder {
        casa.numeroBanheiros = numeroBanheiros
        return this
    }

    override fun setGaragem(garagem: Boolean): Builder {
        casa.garagem = garagem
        return this
    }

    override fun build(): CasaModerna {
        return casa
    }

}

class CasaRusticaBuilder() : Builder{

    private var casa: CasaRustica = CasaRustica()
    override fun setArea(area: Int): Builder {
        casa.area = area
        return this
    }

    override fun setNumeroQuartos(numeroQuartos: Int): Builder {
        casa.numeroQuartos = numeroQuartos
        return this
    }

    override fun setNumeroBanheiros(numeroBanheiros: Int): Builder {
        casa.numeroBanheiros = numeroBanheiros
        return this
    }

    override fun setGaragem(garagem: Boolean): Builder {
        casa.garagem = garagem
        return this
    }

    override fun build(): CasaRustica {
        return casa
    }

}

class Diretor{
    fun construirCasaModerna(builder: Builder): Any {
        return builder.setArea(200)
            .setNumeroQuartos(3)
            .setNumeroBanheiros(2)
            .setGaragem(true)
            .build()
    }

    fun construirCasaRustica(builder: Builder): Any{
        return builder.setArea(150)
            .setNumeroQuartos(2)
            .setNumeroBanheiros(1)
            .build()
    }
}

fun main() {
    val diretor = Diretor()

    val casaModernaBuilder: Builder = CasaModernaBuilder()
    val casaModerna: CasaModerna = diretor.construirCasaModerna(casaModernaBuilder) as CasaModerna
    println(casaModerna.result())

    val casaRusticaBuilder: Builder = CasaRusticaBuilder()
    val casaRustica: CasaRustica = diretor.construirCasaRustica(casaRusticaBuilder) as CasaRustica
    println(casaRustica.result())
}
```

No exemplo em Kotlin, utilizamos as classes `CasaModerna` e `CasaRustica` para representar os diferentes estilos de casas. As classes `CasaModernaBuilder` e `CasaRusticaBuilder` implementam a interface `Builder`, permitindo a construção de casas modernas e casas rústicas, respectivamente.

A classe `Diretor` possui métodos `construirCasaModerna()` e `construirCasaRustica()` que utilizam os métodos do builder para definir as características da casa e retornar o objeto final.

No código de exemplo, criamos instâncias de `CasaModerna` e `CasaRustica` utilizando os builders apropriados. Chamamos o método `result()` em cada uma das casas para exibir as características específicas de cada estilo de casa.

**Benefícios do padrão Builder:**
- Permite construir objetos complexos passo a passo, separando a lógica de construção da representação do objeto.
- Facilita a criação de diferentes representações do mesmo objeto, usando os mesmos passos de construção.
- Melhora a legibilidade e manutenção do código, evitando construtores com muitos parâmetros.
- Facilita a adição de novas características ou estilos de objetos sem modificar a lógica do construtor.

Observação: Essa é uma explicação básica do padrão Builder. É importante estudar mais sobre o assunto e considerar outros aspectos e possibilidades ao aplicar o padrão em diferentes contextos.

## Padrões de Criação: Singleton

O padrão de projeto Singleton é um padrão de criação que garante que uma classe tenha apenas uma instância e forneça um ponto de acesso global para essa instância. Esse padrão é útil em situações em que é necessário restringir a criação de objetos de uma determinada classe para uma única instância, compartilhada por todo o sistema.

### Contexto

Imagine que você esteja desenvolvendo um aplicativo para configurar e gerenciar a aplicação como um todo. Nesse contexto, existem certas configurações que precisam ser acessadas e modificadas de várias partes do código, mas você quer garantir que essas configurações permaneçam consistentes em todo o aplicativo.

### Problema

O problema aqui é que você precisa de uma única instância da classe de configuração para evitar duplicação de dados e inconsistências no sistema. Além disso, é importante que todas as partes do aplicativo acessem a mesma instância para manter a consistência das configurações.

### Solução em Kotlin

Em Kotlin, o padrão Singleton pode ser implementado de maneira simples e eficaz usando um objeto (object). A palavra-chave `object` define uma classe e cria uma única instância desse objeto durante toda a execução do programa.

```kotlin
object AppConfig {
    private var appName: String = "Singleton"
    private var appVersion: String = "1.0.0"

    fun getAppName(): String {
        return appName
    }

    fun getAppVersion(): String {
        return appVersion
    }
}

fun main() {
    val config1 = AppConfig
    val config2 = AppConfig

    println(config1.getAppName())
    println(config2.getAppVersion())

    println(config1 === config2)
}
```
Neste exemplo, criamos o objeto `AppConfig`, que representa a configuração do aplicativo. A classe é declarada como `object`, o que significa que só haverá uma única instância dela durante toda a execução do programa.

O objeto `AppConfig` possui duas propriedades privadas: `appName` e `appVersion`, bem como dois métodos públicos `getAppName()` e `getAppVersion()`, que permitem acessar as configurações do aplicativo.

No `main()`, criamos duas variáveis `config1` e `config2` que recebem a instância do objeto `AppConfig`. Como o objeto é um singleton, ambas as variáveis apontam para a mesma instância, como podemos verificar usando o operador `===` de igualdade de referência.

**Benefícios do padrão Singleton:**

- Garantia de uma única instância: O padrão Singleton garante que uma classe tenha apenas uma instância durante a execução do programa, evitando a criação de múltiplas instâncias desnecessárias e reduzindo o consumo de recursos do sistema.

- Acesso global: A instância única criada pelo Singleton pode ser acessada de qualquer lugar do código, tornando-o um ponto de acesso global para compartilhar informações e funcionalidades importantes em todo o sistema.

- Evita inconsistências: Ao garantir que apenas uma instância exista, o padrão Singleton ajuda a manter a consistência dos dados e configurações em todo o aplicativo, já que todos os componentes acessam a mesma instância.

**Observação:** O padrão Singleton deve ser usado com cuidado, pois o acesso global à instância única pode tornar o código mais difícil de testar e aumentar o acoplamento entre os componentes. É essencial considerar as necessidades específicas do projeto antes de optar por usar esse padrão.

Lembre-se de que o exemplo apresentado é uma implementação simples do padrão Singleton em Kotlin, destinado apenas para fins ilustrativos. Em projetos mais complexos, podem ser aplicadas técnicas adicionais, como garantir a thread safety em ambientes concorrentes ou aplicar padrões de injeção de dependência, para garantir uma utilização mais robusta do padrão Singleton.


## Padrões de Criação: Prototype

O padrão de projeto Prototype é um padrão de criação que permite a clonagem de objetos, evitando a necessidade de criar novas instâncias através de construtores. Esse padrão é útil quando precisamos criar cópias de objetos complexos de forma eficiente, sem a necessidade de recriar a estrutura completa do objeto.

### Contexto

Imagine que você esteja desenvolvendo um jogo de RPG, onde existem vários tipos de monstros, cada um com atributos específicos, como nome e nível. Ao longo do jogo, você precisa criar múltiplas instâncias de monstros para representar as diferentes criaturas que os jogadores encontrarão.

### Problema

Você precisa criar cópias de monstros existentes para evitar a sobrecarga de construtores e permitir que os jogadores encontrem monstros com características variadas sem criar novas instâncias a partir do zero.

### Solução

O padrão Prototype resolve esse problema ao permitir que cada tipo de monstro implemente uma interface de clonagem (normalmente chamada de `Cloneable`), que define um método de clonagem. Cada monstro concreto deve implementar esse método de clonagem para retornar uma cópia de si mesmo.

### Exemplo em Kotlin

```kotlin
open class Monster(
    var name: String,
    var level: Int
): Cloneable {
    public override fun clone(): Monster {
        return Monster(name, level)
    }
}

class OrcMonster(
    name: String,
    level: Int
): Monster(name, level)

class GoblinMonster(
    name: String,
    level: Int
): Monster(name, level)

class MonsterPrototype {
    private val monsterPrototypes = mutableMapOf<String, Monster>()

    fun registerMonster(name: String, monster: Monster) {
        monsterPrototypes[name] = monster
    }

    fun cloneMonster(type: String): Monster? {
        val prototype = monsterPrototypes[type]
        return prototype?.clone()
    }
}

fun main() {
    val monsterPrototype = MonsterPrototype()
    monsterPrototype.registerMonster("orc", OrcMonster("Orc", 1))
    monsterPrototype.registerMonster("goblin", GoblinMonster("Goblin", 4))

    val orc = monsterPrototype.cloneMonster("orc")
    val goblin = monsterPrototype.cloneMonster("goblin")

    orc?.name = "Orcus"
    goblin?.level = 5

    println("Monstro Orc Original: ${monsterPrototype.cloneMonster("orc")?.name} (Nível ${monsterPrototype.cloneMonster("orc")?.level})")
    println("Monstro Orc Clonado: ${orc?.name} (Nível ${orc?.level})")
    println("Monstro Goblin Original: ${monsterPrototype.cloneMonster("goblin")?.name} (Nível ${monsterPrototype.cloneMonster("goblin")?.level})")
    println("Monstro Goblin Clonado: ${goblin?.name} (Nível ${goblin?.level})")
}
```
Neste exemplo, temos uma classe abstrata `Monster`, que representa o protótipo dos monstros do jogo, com atributos como `name` e `level`. As classes `OrcMonster` e `GoblinMonster` são classes concretas que herdam de `Monster`.

A classe `MonsterPrototype` é a responsável por manter um registro dos diferentes tipos de monstros (protótipos) que podem ser clonados. Ela oferece um método `registerMonster` para adicionar monstros ao registro e um método `cloneMonster` para clonar o monstro desejado.

Ao executar o programa, podemos ver que a clonagem é efetiva, pois ao modificar as instâncias clonadas (`orc` e `goblin`), os monstros originais permanecem inalterados. Isso demonstra como o padrão Prototype permite criar cópias independentes de objetos complexos com facilidade, economizando tempo e recursos.

**Benefícios do padrão Prototype:**
- Permite a clonagem de objetos complexos sem a necessidade de recriar a estrutura completa.
- Evita a sobrecarga de construtores ao criar múltiplas instâncias de objetos similares.
- Facilita a criação de objetos com configurações variadas.
- Reduz o acoplamento entre classes ao permitir a clonagem através de interfaces.

Observação: Lembre-se de que este é um exemplo simples do padrão Prototype e pode ser mais complexo dependendo do contexto e dos requisitos do jogo.


## Padrões de Estrutura: Adapter

O padrão Adapter é um dos padrões de projeto estruturais mais utilizados. Ele permite que classes com interfaces incompatíveis trabalhem juntas, facilitando a reutilização de código existente e evitando a necessidade de modificar o código fonte original.

### Contexto

Imagine que você esteja trabalhando em um sistema de pagamento online. Nesse sistema, você possui duas classes que lidam com diferentes provedores de pagamento: `Paypal` e `Payonner`. Cada provedor de pagamento possui sua própria interface de pagamento específica.

### Problema

Você deseja utilizar ambas as classes `Paypal` e `Payonner` para processar pagamentos no seu sistema. No entanto, para isso, seria necessário adaptar a interface de pelo menos uma das classes, para que ambas pudessem ser usadas de forma intercambiável.

### Solução

Nesta solução, utilizamos o padrão Adapter para permitir que as classes `Paypal` e `Payonner` sejam usadas de forma transparente no sistema de pagamento. Criamos uma nova classe chamada `AdapterPayoneer`, que implementa a interface `PaypalPayment` (que já existia no código original). Essa nova classe atua como um adaptador e possui uma referência para a classe `Payonner`, que não implementa a interface `PaypalPayment`.

A classe `AdapterPayoneer` implementa os métodos da interface `PaypalPayment` e, dentro desses métodos, chama os métodos equivalentes da classe `Payonner`. Dessa forma, a classe `Paypal` e a classe `Payonner` podem ser usadas de forma intercambiável, mesmo tendo interfaces diferentes.

### Exemplo em Kotlin

```kotlin
interface PaypalPayment {
    fun payWithPayPal()
}

interface PayonnerPayment {
    fun payWithPayonner()
}

class Paypal : PaypalPayment {
    override fun payWithPayPal() {
        println("Pagamento feito com PayPal.")
    }
}

class Payonner : PayonnerPayment {
    override fun payWithPayonner() {
        println("Pagamento feito com Payonner.")
    }
}

class AdapterPayoneer(private val payonner: Payonner) : PaypalPayment {
    override fun payWithPayPal() {
        payonner.payWithPayonner()
    }
}

fun main() {
    val paypalPayment: PaypalPayment = Paypal()
    paypalPayment.payWithPayPal()

    val adapterPayoneer: PaypalPayment = AdapterPayoneer(Payonner())
    adapterPayoneer.payWithPayPal()
}

```
No exemplo em Kotlin, temos as interfaces `PaypalPayment` e `PayonnerPayment`, bem como as classes concretas `Paypal` e `Payonner`. Criamos a classe `AdapterPayoneer`, que implementa `PaypalPayment` e atua como um adaptador para `Payonner`.

No `main()`, podemos ver que a classe `Paypal` é usada diretamente, chamando seu método `payWithPayPal()`. Em seguida, utilizamos o `AdapterPayoneer` para adaptar a classe `Payonner` e permitir que ela seja usada através da interface `PaypalPayment`, chamando também o método `payWithPayPal()`.

**Benefícios do padrão Adapter:**
- Permite a reutilização de código existente mesmo em classes com interfaces incompatíveis.
- Ajuda a evitar a modificação de código fonte original ao adicionar novas funcionalidades.
- Facilita a integração de classes de terceiros em sistemas existentes.
- Promove a interoperabilidade entre diferentes classes e componentes.

Observação: Essa é uma explicação básica do padrão Adapter. Para aplicar corretamente o padrão em situações mais complexas, é importante estudar mais sobre o assunto e considerar outros aspectos e possibilidades ao adaptar interfaces de classes.

## Padrões de Estrutura: Bridge

O padrão de projeto Bridge é um padrão estrutural que tem como objetivo separar a abstração (interface) da implementação, permitindo que ambas possam variar independentemente. Essa separação é útil quando existem múltiplas dimensões de variação em um sistema.

### Contexto

Imagine que você esteja desenvolvendo uma aplicação de transmissão ao vivo. Nessa aplicação, você tem várias plataformas de streaming, como YouTube, TwitchTV e Facebook.

### Problema

Você precisa implementar a capacidade de fazer transmissões ao vivo em diferentes plataformas, mas não quer que a lógica de streaming específica de cada plataforma fique diretamente acoplada à lógica de negócio da aplicação.

### Solução

O padrão Bridge resolve esse problema dividindo a hierarquia de classes em duas partes: a parte abstrata (abstraction) e a parte implementadora (implementor). A parte abstrata define a interface que será utilizada pela aplicação, enquanto a parte implementadora define a interface que será usada pelas classes concretas de implementação.

### Exemplo em Kotlin

```kotlin
// Parte Abstrata
interface LiveStreaming {
    fun start()
    fun stop()
}

// Parte Implementadora
interface Platform {
    fun startLiveStream()
    fun endLiveStream()
}

// Implementações da Parte Implementadora
class YoutubePlatform : Platform {
    override fun startLiveStream() {
        println("Iniciando a transmissão no Youtube")
    }

    override fun endLiveStream() {
        println("Encerrando a transmissão no Youtube")
    }
}

class TwitchTVPlatform : Platform {
    override fun startLiveStream() {
        println("Iniciando a transmissão na TwitchTV")
    }

    override fun endLiveStream() {
        println("Encerrando a transmissão na TwitchTV")
    }
}

class FacebookPlatform : Platform {
    override fun startLiveStream() {
        println("Iniciando a transmissão no Facebook")
    }

    override fun endLiveStream() {
        println("Encerrando a transmissão no Facebook")
    }
}

// Implementações da Parte Abstrata
class LiveStream(private val platform: Platform) : LiveStreaming {
    override fun start() {
        platform.startLiveStream()
    }

    override fun stop() {
        platform.endLiveStream()
    }
}

fun main() {
    val youtubeLive: LiveStreaming = LiveStream(YoutubePlatform())
    val twitchLive: LiveStreaming = LiveStream(TwitchTVPlatform())
    val facebookLive: LiveStreaming = LiveStream(FacebookPlatform())

    youtubeLive.start()
    twitchLive.start()
    facebookLive.start()

    youtubeLive.stop()
    twitchLive.stop()
    facebookLive.stop()
}
```

Neste exemplo, definimos a parte abstrata `LiveStreaming`, que representa a interface para iniciar e encerrar a transmissão. Em seguida, temos a parte implementadora `Platform`, que define a interface para as diferentes plataformas de streaming. As classes concretas de implementação, como `YoutubePlatform`, `TwitchTVPlatform` e `FacebookPlatform`, implementam a interface `Platform` de acordo com suas respectivas plataformas.

A classe `LiveStream` é a implementação concreta da parte abstrata `LiveStreaming`, que recebe uma instância da plataforma de streaming específica e do tipo de transmissão em seu construtor e delega as chamadas de `start()` e `stop()` para as respectivas plataformas e tipos de transmissão.

Dessa forma, o padrão Bridge desacopla a lógica de negócio da transmissão ao vivo da lógica específica de cada plataforma de streaming e tipo de transmissão, permitindo que ambas variem independentemente. Se uma nova plataforma for adicionada, basta criar novas classes concretas que implementem a interface `Platform`, sem precisar alterar as classes existentes.

**Benefícios do padrão Bridge:**
- Desacopla abstração de implementação.
- Permite a extensão independente das duas partes.
- Facilita a adição de novas funcionalidades sem modificar o código existente.
- Melhora a legibilidade e manutenção do código.

Observação: Lembre-se de que este é um exemplo simples do padrão Bridge e pode ser mais complexo dependendo do contexto e dos requisitos do sistema.



## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
