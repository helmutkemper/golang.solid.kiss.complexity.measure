# SOLID, KISS e Complexity Measure - Uma abordagem para o desenvolvedor Golang
Dicas de programação em golang para programadores

### Conteúdo

| Conteúdo                                                                                                                           |
|------------------------------------------------------------------------------------------------------------------------------------|
| [Sobre](https://github.com/helmutkemper/golang.solid.kiss.complexity.measure/edit/master/README.md#Sobre)                          |
| [Licença](https://github.com/helmutkemper/golang.solid.kiss.complexity.measure/edit/master/README.md#Licença)                      |
| [Links](https://github.com/helmutkemper/golang.solid.kiss.complexity.measure/edit/master/README.md#Links)                          |

### Sobre

Faz um tempo que penso em compartilhar conhecimento, por isto, vou deixar este documento público, mesmo que inacabado, para que a comunidade possa acompanhar meu trabalho e participar.

A minha intenção inicial é compartilhar minha experiência e encontrar mais pessoas dispostas a compartilhar e discutir a melhor forma de fazer com outros programadores, por isto, este material é focado em pessoas que já fazem desenvolvimento de código e já conseguem programar alguma coisa em Golang.

Todos são bem vindos para adicionar material e discutir a melhor forma de programar algo, mas, todas as dicusões devem ser técnicas e relevantes a comunidade.

### Licença

Todo o conteúdo é baseado na lincença Apache 2.0 e você é libre para fazer o que queizer com este conteúdo, dentro dos limites da licença.

 ### Links
 
[Desing Principles](https://fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf)

[Cognitive Complexity](https://www.sonarsource.com/docs/CognitiveComplexity.pdf)


## Regra de ouro

Você do futuro vai ter de usar seus códigos depois de mais de um ano sem lembrar que este código existia e você vai está muito cansado doido para sair da frente do computador e algo muito bom está te esperando, mas, você tem de trabalhar no teu código antigo.

Se você não se esforça para entender esta regra, você não merece ser desenvolvedor, porque, cedo ou tarde, alguém além de você vai pegar seus códigos e vai passar por isto.

O **Kiss - Keep It Stupid Simple / Keep It Simple, Stupid!**, o **SOLID** do Oncle Bob e o **Cognitive Complexity** do Thomas J. McCabe, Sr simplesmente resumem a regra de ouro.  

## Os princípios do SOLID

**SRP - Single responsibility principle**
Princípio da Responsabilidade Única - Um objeto deve ter uma, e somente uma, responsabilidade para cuidar.

**OCP - Open/closed principle**
Princípio do Aberto/Fechado - Você deve ser capaz de estender um comportamento de um objeto sem a necessidade de modificá-lo.

**LSP - Liskov substitution principle**
Princípio da substituição de Liskov - Os objetos derivados devem ser substituíveis por seus objetos base.

**ISP - Interface segregation principle**
Princípio da segregação de interfaces - Muitas interfaces específicas são melhores do que uma interface única geral.

**DIP - Dependency inversion principle**
Princípio da inversão de dependência - Dependa de abstrações e não de implementações.



## Orientação a Objeto e Inteface

Por experiência própria, eu demorei muito entre o dia que eu estudei orientação a objeto e o dia que eu realmente comecei a pensar em orientação a objeto, e se você ainda está estudando, ou faz pouco tempo que estudou, não se preocupe, você, provavelmente vai demorar a entender esta afirmação, pois, é muito mais fácil pensar sem ela.

A base da orientação a objeto em Golang é o **[Struct{}](https://gobyexample.com/structs)**. Na prática, o struct é um tipo definido pelo usuário com a capacidade de agrupar vários outros tipos e funções.

Veja o seguinte código genérico de exemplo:

```javascript
  class Quadrado implements Area{
    private var comprimento;
    
    public function set(x) {
      comprimento = x
    }
    
    public function area() {
      return comprimento * comprimento
    }
  }
  
  class Circulo implements Area{
    private var comprimento;
    private var rasio;
    
    public function set(x) {
      comprimento = x
    }
    
    public function getRaio() {
      return comprimento/2
    }
    
    public function area() {
      return math.PI * getRaio()*getRaio()
    }
  }
  
  interface Area{
    function set(x)
    area()
  }
```

Esse é um código simples onde há duas classes, uma para calcular a área de um quadrado e outra para calcular a área de um círculo além de uma interface simples.

Todo livro que eu li se concentra muito na classe e explica um monte de coisas sobre ela, mas, hoje eu vejo a interface como sendo a parte mais importante de todas e vou começar por ela.

A interface é um simples contrato de como todas as funções públicas vão ser quando estiverem prontas, por tanto, ela deveria ser a primeira coisa a ser montada em um trabalho em grupo.

Na prática, o grupo vai se reunir e imaginar algo tipo, temos dois grupos de trabalho, o primeiro grupo vai trabalhar nas funcionalidades de como implementar a área de um círculo e o segundo grupo vai implementar as funcionalidades de cálculo da área de um quadrado.
Os grupos discutem e decidem, necessitamos no mínimo de dois métodos, um para definir o valor e um outro para pegar o resultado da área.
É nesse ponto onde a interface se mostra extremamente eficiente, ela é um contrato a ser seguido por todos os grupos, mas, a interface é um contrato de funções mínimas, e não uma armadilha a suas classes, ou seja, sua classe vai ter obrigatoriamente os mesmos métos com os mesmos tipos da interface, mas, isto não te obriga a ter apenas eles, por isto, na segunda classe há um método a mais, o getRaio().

Agora vamos imaginar o seguinte, existe um terceiro grupo encarregado de montar uma interface gráfica e esse grupo necessita de mais tempo para confeccionar a interface gráfica do que os desenvolvedores necessitam para implementar, mas, como em todo projeto, o tempo é muito apertado e eles não podem esperar as funcionalidades ficarem prontas.

A grande beleza da interface é o fato dela permitir dados "mokados", ou seja, dados fantazia próximos ao real e com a finalidade de permitir o grupo da interface gráfica começar a trabalhar enquanto o resto fica pronto.

Por exemplo:

```javascript
  class Mokado implements Area{
    public function set(x) {
      
    }
    
    public function area() {
      return 16
    }
  }

  interface Area{
    function set(x)
    area()
  }
```

Como você pode ver no exemplo, a classe **Mokado** compila e é funcional a ponto da equipe de interface gráfica começar a trabalhar e vê se a parte dela funciona como esperado.

O outro ponto a ser lembrado é o **ISP - Interface segregation principle**, ou princípio da segregação de interfaces - Muitas interfaces específicas são melhores do que uma interface única geral.

Na prática isto quer dizer o seguinte, faça interface expecíficas para grupo de coisas específicas.

Imagine um código de player de vídeo. Ele necessita de um monte de controles de vídeo, tipo, play, pausa, velocidade, legenda, etc.
Você pode fazer uma interface gigante com todas as funcionalidades, provavelmente vai funcionar, mas, pode ser um tiro no pé e o **ISP** é justamente para evitar isto, ou seja, crie uma interface para as funções básicas de vídeo, tipo, play e pausa, e crie outra para as funções de legendas, e assim por diante.

O grande segredo é: divida suas interfaces em grupos por necessidade.

Agora vamos ver a mesma coisa pelo ponto de vista do Golang.

```golang
  import "math"
  
  type Quadrado struct {
    comprimento float64 // 'c'omprimento = private e 'C'omprimento = public
  }
  
  func(el *Quadrado) Set(comprimento float64) {
    el.comprimento = comprimento
  }
  
  func(el *Quadrado) Area() float64 {
    return el.comprimento * el.comprimento
  }

  type Circulo struct {
    comprimento float64
    raio float64
  }
  
  func(el *Circulo) Set(comprimento float64) {
    el.comprimento = comprimento
  }
  
  func(el *Circulo) Area() float64 {
    return el.GetRaio() * el.GetRaio() * math.Pi
  }
  
  func(el *Circulo) GetRaio() float64 {
    return el.comprimento/2
  }
  
  type Area interface {
    Set(comprimento float64)
    Area() float64
  }
```

No exemplo abaixo temos o equivalente a uma classe escrita em Golang.
Nos livros, você vai ver três formas de escrever uma função associada a um struct, como eu fiz, com a função do lado de fora, com um ponteiro, simplesmente escrevendo o nome da função após a chave ou escrever a função dentro do próprio struct.

Primeira regra, caso você goste de escrever as funções dentro do struct, para você, **Kiss** quer dizer **Keep It Simple, Stupid!**, caso contrario, **Kiss** quer dizer **Keep It Stupid Simple** e não se iluda, se você acha que isso foi grosseria, espera até uma outra pessoa receber seu código e ouvir algo tipo, você só vai para casa hoje depois disso ficar pronto.

```golang
  import "math"
  
  type Quadrado struct {
    comprimento float64 // 'c'omprimento = private e 'C'omprimento = public
  }
  
  func(el *Quadrado) Set(comprimento float64) {
    el.comprimento = comprimento
  }
  
  func(el *Quadrado) Area() float64 {
    return el.comprimento * el.comprimento
  }

```

Como regra simples, primeira letra maiúcula para nomes de chaves dentro do struct ou nomes de funções as tornam públicas, e letras minúsculas privadas.

**func(el *Quadrado) Set(comprimento float64)** é uma função pertencente ao struct Quadrado, e **el *Quadrado** define o termo **el** como sendo o **this** de várias linguagens, onde **el *Quadrado** permite o valor dentro do struct ser alterado e **el Quadrado**, sem o asterísco de ponteiro, permite apenas leitura.

No início, eu sempre usava termos mais explicativos para o **el**, tipo, **func(elementoDeArea *Quadrado) Set(comprimento float64)**, mas, a prática me mostrou a necesside de copiar/colar muito cabeçalho de função, e hoje eu coloco simplesmente **el** de element.

```golang
  type Area interface {
    Set(comprimento float64)
    Area() float64
  }
```

Já o uso da interface é bem simples, basta apontar o objeto assim: **var variavel nomeInterface = &nomeStruct{}**

```golang
  var a Area = &Quadrado{}
      a.Set(16.0)
  fmtPrintf("área: %v\n", a.Area())
```

Para o desenvolvedor, apenas definir o tipo da variável como sendo a interface, **var a Area**, já faz o editor reconhecer e usar o autocompletar.

> Mas, meu código só vai ser desenvolvido por mim...

Nunca cometa o erro de não criar a interface. Tecnicamente, a interface é apenas um contrato, mas, na verdade, ela é um grande salva vidas para quando os parâmetros de projeto mudam do dia para a noite.

Um exemplo simples da vida real muito comum e simples de acontecer, o projeto foi feito para usar MySql e já faz dois anos que trabalhamos nele, mas, hoje surjiu um cliente muito grande e ele só trabalha com PostgreSQL e a reunião é para ontem.

Regra simples que pode poupar muito tempo a você do futuro: sempre monte um objeto em vez de usar o objeto padrão criado por outras pessoas para todos os pontos do código importantes, por mais remota que seja esta possibilidade de mudança um dia e monte a sua interface para ela.

Exemplo prático:

```golang
  // código original de exemplo
  db, err := sql.Open("mysql", "root:password@tcp(127.0.0.1:3306)/test")
```

Nesse ponto, há vários proplemas, tipo, o MongoDB tem métodos totalmente diferentes e é uma possibilidade bem real de acontecer um dia.
Pode ser que o drive de banco fique obceloto por algum motivo qualquer. Por xemplo da vida real, um dia apareceu um texto tipo "esse código não é muito bom e eu não recomendo mais que seja usado" no repositório do drive mais usado para MongoDB em golang e não obrigação nenhuma de quem fez o drive novo de seguir o drive antigo.

Hoje, eu faria algo parecido como exemplo abaixo.

```golang
  const (
    KConnectionTypeTcp TypeConn iota + 1
    KConnectionTypeUdp
  )
  
  type BancoDeDados interface {
    User(user string)
    Password(pass string)
    TypeConnection(typeConn TypeConn)
    Host(host string)
    Port(port string)
    Connect() error
  }
  
  type MySql struct {
    db *sql.MySQLDriver
    ...
  }
  
  func(el *MySql) Connect() error {
    if el.user == "" {
      return erros.New("user name not set")
    }
    
    ...
    
    el.db.Open("mysql", el.user + ":" + el.password + "@(" + el.host + ":" + el.port + ")/" + el.dbName )
  }
```

Isso dá um pouco de trabalho inicial, mas, isto salva a vida quando algo muda no projeto e todo programador sabe, o projeto muda o tempo todo.

Então, acredite em mim, meu primeiro computador foi um TK-90X em 1986 e eu nunca vi um projeto grande não mudar no meio.

> Motivação: Lá pelo início dos anos 2000 eu assinei um contrato pagando muito bem para fazer um projeto em MySql e tudo foi feito no prazo combinado e entregue conforme o contrato. No dia da apresentação técnica para o pessoal da implantação, o técnoco responssável diz: nós só trabalhamos com Postgre e o sistema tem de mudar... cobrei um valor bem alto e pedi 30 dias; fui para casa, mudei uma string, testei e segui a vida de forma mais feliz.

