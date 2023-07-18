<div align="center">
  <h3>🚧 Material em Construção 🚧</h3>
</div>

# Padrões de Projeto

Este repositório é dedicado ao estudo e exploração dos padrões de projeto utilizados no desenvolvimento de software. Aqui, você encontrará informações baseadas no meu entendimento pessoal sobre o tema.

No entanto, é importante ressaltar que, apesar dos meus melhores esforços, podem ocorrer equívocos ou interpretações diferentes. Se você identificar algum erro ou tiver alguma sugestão de melhoria, por favor, informe-me. Estou sempre aberta a correções e aprecio contribuições para aprimorar o conteúdo disponibilizado aqui.

Agradeço pela sua compreensão e espero que as informações fornecidas sejam úteis em seu estudo sobre os padrões de projeto.

## Principais Tópicos Abordados

- Padrões de projeto creacionais
- Padrões de projeto estruturais
- Padrões de projeto comportamentais

## Exemplos em Kotlin

Neste repositório, você encontrará exemplos práticos dos padrões de projeto implementados em Kotlin. Os exemplos foram desenvolvidos de forma a facilitar o entendimento e demonstrar a aplicação dos padrões em situações reais.

## Padrões de Projeto

A seguir, são apresentados os principais padrões de projeto abordados neste repositório:

## Padrões de Criação: Factory Method

O padrão Factory Method é um dos padrões de projeto creacionais mais utilizados. Ele fornece uma maneira de criar objetos sem especificar explicitamente a classe exata do objeto que será criado. Em vez disso, o Factory Method define uma interface para criar objetos, delegando a decisão de qual classe concreta utilizar para as subclasses.

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


## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
