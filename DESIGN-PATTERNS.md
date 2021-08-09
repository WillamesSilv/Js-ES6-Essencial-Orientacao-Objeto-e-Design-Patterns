# Objetivo da Aula
 - Definição
 - Tipos
 - Patterns mais utilizados
 ---------------------------------------------------------
 ## _Definição_

 Design Patterns ou padrões de projetos são soluções generalistas para problemas recorrentes durante o desenvolvimento de um software. Não se trata de um framework ou um código pronto, mas de uma definição de alto nível de como um problema comum pode ser solucionado.

### ___A Pattern Language___

- Surgiu em 1978
- Christopher Alexander, Sara  Ishikawa e Murray Silverstein
- 253 tipos de problemas/desafios de projetos

![Capa do livro A Pattern Language](./img.jpg)

### ___Formato de um Pattern___
 - Nome
 - Exemplo ( de sua utlização )
 - Contexto ( que pode ser aplicado )
 - Problema ( que o pattern resolve )
 - Solução ( a forma que ele resolve )

 ### ___Using Pattern Languages for Object-Oriented Programs___

  - 1987
  - Kent Beck e Ward Cunningham
  - 5 Padões de projetos
### ___Design Patterns: Elements of Reusable Object-Oriented Software___

 - 1994
 - Gang of four (GoF)
 - Erich Gamma, Richard Helm, Ralph Johnson e John Vlissides 

 ![Capa do livro Elements of Reusable Object-Oriented Software](./elements.jpg) 

 -------------------------------------------------------

## _Tipos_

 - Criação
 - Estruturais
 - Comportamentais

 ### ___Padrões de Criação___

 Os padrões de criação são aqueles que abstraem e/ou adiam o processo de criação dos objetos. Eles ajudam a tornar um sistema independente de como seus objetos são criados, compostos e representados.

- Abstract Factory
- Builder
- Factory method
- Prototype
- Singleton

### ___Padrões Estruturais___

Os padrões estruturais se preocupam com a forma de como classes e objetos são compostos para formar estruturas maiores.

 - Adapter
 - Bridge
 - Composite
 - Decorator
 - Facade
 - Business Delegate
 - Flyweight
 - Proxy

 ### ___Padrões Comportamentais___

 Os padrões de comportamentos se concentram nos algoritmos e atribuições de responsabilidades entre os objetos. Eles não descrevem apenas padrões de objetos ou de classes, mas também padrões de comunicações entre objetos.

 - Chain of Responsibility
 - Command
 - Interpreter
 - Iterator
 - Mediator 
 - Observer 
 - State
 - Strategy
 - Template method
 - Visitor

 ---------------------------------------------------------

## _Patterns mais utilizados_

 - Factory
 - Singleton
 - Decorator
 - Observer
 - Module

 ### ___Factory___

 Todas as funções que retornam um objeto, sem a necessidade de chama-las com o `new`, são consideradas funções ___Factory___ (fábrica).

Exemplo do que ___não___ é uma função Factory:
 ~~~javascript
 function FakeUser() {
     this.name: 'Willames'
     this.lastName: 'Santos'
 }

 // não é Factory
 const user = new FakeUser()
 ~~~

Exemplo de Factory:
 ~~~javascript
 function FakeUser() {
     return {
        name: 'Willames'
        lastName: 'Santos'
     }
     
 }

 // Factory
 const user = FakeUser()
 ~~~

### ___Singleton___

O objetivo desse pattern é criar uma única instância de uma função construtora e retorná-la toda vez em que for necessário utilizá-la.

O [___jQuery___](https://jquery.com/) use o padrão de Singleton.

Exemplos de Singleton:

- Pode ser uma variável global
~~~javascript
var SETTINGS ={
    api: 'http://localhost',
    trackJsToken: '12345'
}
~~~

- Em função, caso a variável não esteja definida ele instância

~~~javascript
function MyApp() {
    if(!MyApp.instance) {
        MyApp.instance = this
    }
    return MyApp.instance
}
~~~
### ___Decorator___