# Introdução a orientação a objetos

## Objetivo da aula

 - Herança
 - Classes 
 - Modificadores de Acesso
 - Encapsulamento
 - Static

### ___Herança___

- Baseada em prototipos
- Prototype
- __ proto__
- constructor

**Prototype**  : É uma variavel que armazena as definições de um objeto;  

Toda vez que criamos uma variável, ela tem essa referência `__proto__` que aponta para o `prototype` do tipo que criamos, esse tipo é chamado de  `Constructor`.

~~~javascript
'use strict';

const myText = 'Hello prototype!';

myText.split(''); // de onde vem esse split?
~~~
Mesmo código usando a função contrutora `string` que já carrega um `protorype`:

~~~javascript 
'use strict';

const myText = String('Hello protptype!');

console.log(myText.__proto__.split);
// f split() { [native code}
~~~

Então se fizermos uma comparação do `__proto__.split` ele vai ser igual a função `split` dentro do `prototype` da função `String`.

~~~javascript 
'use strict';

const myText = String('Hello prototype!');

console.log(myText.__proto__.split === String.prototype.split); // true
~~~
## **E se criarmos uma function como no exemplo abaixo?**

~~~javascript
'use strict';

function Animal() {
    this.qtdePatas = 4; 
};

const cachoro = new Animal();

console.log(cachorro.qtdePatas); // 4 
~~~

Mas o que é este `new Foo(...)` ? O que ocorre quando pegamos uma função construtora e chamamos ela com o operador `new` ?

1. Um objeto é criado, herdando o `Foo.prototype`
2. A função construtora `Foo` é chamada com os argumentos especificados e com o `this` vinculado ao novo objeto criado 
3. Caso a função contrutora tenha um `return` explicito, será respeitado o seu `return`. Se não, será retornado o objeto criado no passo 1. 
----------------------------------------------------------
## *Criando uma função derivada de outra*

Podemos criar uma função contrutora derivada de outra, usando a função `call`. 

A função `call` permite passar um contexto para a função ser executada, como se fosse uma herança.

~~~javascript 
'use strict';

function Animal(qtdePatas) {
    this.qtdePatas = qtdePatas;
};

function Cachorro(morde) {
    Animal.call(this, 4);

    this.morde = morde;
};

const pug = new Cachorro(false);

console.log(pug) // Cachorro {qtdePatas: 4, morde: false}
~~~

Implementando novos metodos dentro das funções `Animal` e `Cachorro`.

~~~javascript
'use strict';

function Animal(qtdePatas) {
    this.qtdePatas = qtdePatas;
    this.movimentar = function() {}
};

function Cachorro(morde) {
    Animal.call(this, 4);

    this.morde = morde;
    this.latir = functIon() {
        console.log('Au, Au!');
    }
};

const pug = new Cachorro(false);
const pitBull = new Cachorro(true);
~~~

Porém temos um problema, toda vez que criarmos um novo objeto `new Cachorro`, a `function latir` e a `function movimentar` será criada. Nesse caso como todos eles vão se movimentar e latir da mesma maneira, não queremos ficar repetindo as funções, vamos criar a solução para isto partindo do princípio de que quando criarmos a nossa função construtora ela permite que ecrevamos no `prototype`, sabemos que o `prototype` contém a definição do nosso objeto, sendo assim podemos criar `qtdePatas` e `movimentar` de maneira padronizada para nossa função `Animal`, da mesma forma para a função `Cachorro`, mas com uma diferença, quando formos criar o `prototype de Cachorro` temos que informar que é derivado do `prototype de Animal`.

~~~javascript 
'use strict';
 
function Animal() {};

Animal.prototype.qtdePatas = 0;
Animal.protorype.movimentar = function() {}

function Cachorro(morde) {
    this.qtdePatas = 4;
    this.morde = morde;
}

Cachorro.prototype = object.create(Animal);
Cachorro.prototype.latir = function() {
    console.log('Au, Au!')
};

const pug = new Cachorro(false);
const pitBull = new Cachorro(true);
~~~
----------------------------------------------------------

### ___Classes___
 - Criado a partir do **ES6**
 - Simplificação da herança de protótipos
 - Palavra chave **Class**

Vamos usar como exemplo a `funciton Animal` que criamos anteriormente.

~~~javascript
class Animal {
    constructor(qtdePatas){
        this.qtdePatas = 4;
    };
};

class Cachorro extends Animal {
    constructor(morde) {
        super(4);
        this.morde = 4;
    };
};

const pug = new Cachorro(false);

console.log(pug) // Cachorro {qtdePatas: 4, morde: 4}
~~~
-------------------------------------------------------

### ___Modificadores de Acesso #___
 - Será implementado a partir da versão 12 do node.js
 - Ainda não tem suporte no browsers.
 - Controle de privado/publico

Sem o modificador de acesso, temos que criar funções para acessar, alterar ou incrementar na função contrutora:

~~~javascript
'use strict';

function Person(initialName){
    let name = initialName // Atributo nome que é privado

    this.getName = function() {
        return name;
    }

    this.setName = function(newName) {
        name = newName;
    }
}

const p = new Person('Willames');

console.log(p) // Person {getName: f, setName:  f}

p.getName(); // 'Willames'

p.name // undefined

p.setName('André')

p.getName() // 'André'
~~~

Usando o modificador de acesso para o mesmo exemplo:

~~~javascript
'use strict';

class Person(){
    #name = '' // o modificador de acesso (#), determina que uma variável é privada

    constructor(initialName) {
        this.#name = initialName
    }

    setName(name) {
        this.#name = name
    }

    getName() {
        return this.#name
    }
    
}

const p = new Person('Willames');

console.log(p) // Person {getName: f, setName:  f}

p.getName(); // 'Willames'

p.name // undefined

p.setName('André')

p.getName() // 'André'
~~~
-------------------------------------------------------

### ___Encapsulamento___

 - Ocultar detalhes do funcionamento interno
 - Na versão 12 do node.js usa-se os metodos `get` e `set`

------------------------------------------------------

### ___Static___
 - Acessar metodos ou atributos sem instânciar

~~~javascript
'use strict';

class Person {
    static walk() {
        console.log('walking...')
    }
}
console.log(Person.walk())// walking...
~~~
