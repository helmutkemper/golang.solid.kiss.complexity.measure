# SOLID, KISS e Complexity Measure - Uma conversa com o desenvolvedor Golang
Dicas de programação em golang para programadores

### Conteúdo

| Conteúdo                                                                                                                           |
|------------------------------------------------------------------------------------------------------------------------------------|
| [Sobre](https://github.com/helmutkemper/golang.solid.kiss.complexity.measure/edit/master/README.md#Sobre)                          |
| [Licença](https://github.com/helmutkemper/golang.solid.kiss.complexity.measure/edit/master/README.md#Licença)                      |
| [Links](https://github.com/helmutkemper/golang.solid.kiss.complexity.measure/edit/master/README.md#Links)                          |

### Sobre

Já faz um tempo onde penso em compartilhar conhecimento, mas, não sou muito bom em transformar pensamentos em texos, por isto, peguei uma carona nos textos do SOLID, do Uncle Bob (e ele sabe disso), do trabalho **Cognitive Complexity** do Sr. Thomas J. McCabe e do método **Kiss - Keep It Stupid Simple / Keep It Simple, Stupid!**.

A intenção inicial é compartilhar a minha e encontrar mais pessoas dispostas a compartilhar as suas próprias experiências e discutir a melhor forma de fazer com outros programadores, por isto, este material é focado em pessoas desenvolvedoras de código e que já conseguem programar alguma coisa em Golang.

Todos são bem vindos para adicionar material e discutir a melhor forma de programar algo, mas, todas as discussões devem ser técnicas e relevantes a comunidade.

### Licença

Todo o conteúdo é baseado na licença Apache 2.0 e você é livre para fazer o que quiser com este conteúdo, dentro dos limites da licença e dando o crédito.

### Links
 
[Desing Principles](https://fi.ort.edu.uy/innovaportal/file/2032/1/design_principles.pdf)

[Cognitive Complexity](https://www.sonarsource.com/docs/CognitiveComplexity.pdf)


## Regra de ouro

Você do futuro vai ter de usar os seus códigos depois de mais de um ano sem lembrar que este código existia e vai estar muito cansado, doido para sair da frente do computador e algo muito bom vai estar te esperando, mas, você tem de trabalhar no seu código antigo.

Se você não se esforça para entender esta regra, você não merece ser desenvolvedor, porque, cedo ou tarde, alguém além de você vai pegar os seus códigos e vai passar por isto.

O **Kiss - Keep It Stupid Simple / Keep It Simple, Stupid!**, o **SOLID** do Uncle Bob e o **Cognitive Complexity** do Sr Thomas J. McCabe simplesmente resumem a regra de ouro e todo programador um dia passa a entender a regra de ouro, mesmo sem conhecer os trabalhos deles.

## Introdução dada pelo Uncle Bob

O que é arquitetura de software? A resposta é, multicamada.

No topo superior, há os padrões de arquitetura definindo o formato geral e a arquitetura da aplicação de software. Na camada abaixo há a arquitetura relativa ao propósito da aplicação, e na camada abaixo, reside a arquitetura dos módulos e as suas interconexões.

Este é o padrão de projeto para pacotes, componentes e classes e este é o nível que nos preocuparemos nesse capítulo. O nosso escopo, neste capítulo, é bastante limitado, porém, há muito mais a ser dito sobre os princípios e padrões expostos aqui.


Arquitetura e dependências

O que dá errado com o software? 

O design de muitos aplicativos de software começa como uma imagem vital na mente dos seus projetistas. Nesta fase, ele é limpo, elegante e atraente. Ele tem uma beleza simples que faz com que os designers e implementadores desejem vê-lo funcionando. Alguns desses aplicativos conseguem manter essa pureza de design durante o desenvolvimento inicial e no primeiro lançamento. Então, algo começa a acontecer. O software começa a apodrecer. No começo não é tão ruim. Uma verruga feia aqui, um truque desajeitado ali, mas a beleza do design ainda persiste. No entanto, com o tempo, à medida que a podridão continua, as partes feias e feridas apodrecedoras acumulam-se até dominarem o design do aplicativo. O programa se torna uma massa de código onde os desenvolvedores acham cada vez mais difícil de manter. 

Eventualmente, o simples esforço necessário para fazer as alterações mais simples da aplicação se torna tão alto que os engenheiros e gerentes da linha de frente choram por uma reformulação do projeto original.

Tais reformulações raramente são bem sucedidas. Embora os designers comecem com boas intenções, eles acham que estão a atirar em alvos em movimento. O sistema antigo continua a evoluir e mudar, e o novo design deve acompanhar. As verrugas e úlceras se acumulam no novo design antes mesmo de chegar ao seu primeiro lançamento. Nesse dia fatídico, geralmente muito mais tarde do esperado, o pântano de problemas no novo design pode ser tão ruim que os designers já estão chorando por outra reformulação.


Sintomas do projeto em decomposição

Existem quatro sintomas principais que nos dizem, os projetos estão apodrecendo. Eles não são ortogonais, mas estão relacionados entre si de maneira muito simplista, ou seja, sempre há: rigidez, fragilidade, imobilidade e viscosidade.

Rigidez: Rigidez é a tendência para o software ser difícil de mudar, mesmo de maneiras simples. Toda a mudança causa uma cascata de mudanças subsequentes nos módulos dependentes. O que começa como uma simples mudança de dois dias em um módulo cresce em uma maratona de várias semanas de mudança, em módulo após módulo, enquanto os engenheiros buscam o fio da mudança através do aplicativo.

Quando o software se comporta dessa maneira, os gerentes temem a permitir aos engenheiros resolvam problemas não críticos. Essa relutância deriva do fato de eles não saberem, com nenhuma confiabilidade, quando os engenheiros finalizarão as mudanças. Se os gerentes soltarem os engenheiros para mergulharem nesses problemas, eles poderão ficar imersos por longos períodos, então, o design do software começa a assumir algumas características de um motel barato - os engenheiros fazem check-in, mas não fazem check-out.

Quando os medos do gerente se tornam tão agudos eles passam a se recusam a permitir alterações no software, a rigidez oficial entra em cena, e o que começa como uma deficiência de design vira uma política de gerenciamento adversa.

Fragilidade: Intimamente relacionada à rigidez está a fragilidade. Fragilidade é a tendência do software quebrar em muitos lugares a cada alteração. Frequentemente, a quebra ocorre em áreas sem relação conceitual com a área alterada. Tais erros enchem os corações dos gerentes de presságios. A cada autorização de correção, eles temem uma falha inesperada em algum lugar não relacionado no software.

A fragilidade só piora e a probabilidade de quebrar aumenta com o tempo, aproximando-se cada vez mais da certeza até fica impossível manter esse software. Cada correção piora ainda mais o problema, introduzindo mais problemas do que resolvido.

Esse software faz com que gerentes e clientes suspeitem que os desenvolvedores perderam o controle do software; A desconfiança reina e a credibilidade é perdida.

Viscosidade: A viscosidade vem de duas formas: viscosidade do design e viscosidade do ambiente. Quando confrontados com uma mudança, os engenheiros geralmente encontram mais de uma maneira de fazer a alteração. Algumas preservando o design, outras não (ou seja, são hacks). Quando as maneiras de se fazer uma alteração complicam a preservação do design, e os hacks começam a ser mais fáceis de se fazer, a viscosidade do design é alta, ou seja, o design está errado e torna o modo errado mais fácil de ser implementado do que o correto.

A viscosidade do ambiente ocorre quando o ambiente de desenvolvimento é lento e ineficiente. Por exemplo, se os tempos de compilação forem muito longos, os engenheiros serão tentados a fazer alterações que não forçam recompilações grandes, mesmo que essas alterações não sejam ideais do ponto de vista do design. Se o sistema de controle de código-fonte precisar de horas para fazer o check-in em apenas alguns arquivos, os engenheiros ficarão tentados a fazer alterações com um menor número possível de check-ins, independentemente do design ser preservado.

Apenas gostaria de complementar o texto do Uncle Bob com um ponto a mais, viscosidade do contratante do projeto.

É a primeira reunião do projeto, todos estão reunidos e os prazos de desenvolvimento são lançados de forma honesta. Logo em seguida, alguém da diretora, provavelmente alguém que nunca participou de um projeto grande, começa a fazer uns cálculos de cabeça em voz alta e logo em seguida corta todos os prazos pela metade. No meu caso, demorei a entender isto, mas, o projeto deu errado nesse momento e a maioria nos desenvolvedores ainda não notou isto. Eles apenas vão para os ambientes de trabalho e fazem o melhor possível. Algum tempo depois, todos passam a colocar a culpa em outra pessoa e o trabalho fica horrível, mas, na verdade, esse é só um sintoma tardio de algo muito mais sério. 

Conclusão: Esses sintomas são os sinais reveladores da arquitetura pobre. Qualquer software que os exiba, sofrerá de um design doente e apodrecerá de dentro para fora.

Mas, o que faz essa podridão ocorrer?

Alterando os requerimentos

A causa imediata da degradação do projeto é bem compreendida. Os requisitos foram alterados de formas não previstas pelo design inicial. Geralmente, essas alterações precisam ser feitas rapidamente e podem ser feitas por engenheiros sem familiaridade com a filosofia do design original. Portanto, mesmo a alteração no design funcionando, ela viola o design original e pouco a pouco, as mudanças continuam a chegar, essas violações se acumulam até a malignidade se instalar.

No entanto, não podemos culpar a deriva dos requisitos para a degradação do design. Nós, como engenheiros de software, sabemos muito bem como os requisitos mudam. De fato, muitos de nós percebemos a valatilidade exceciva do documento de requisitos do projeto. Se nossos projetos estão falhando devido à chuva constante de requisitos variáveis, são os nossos projetos que são os culpados. De alguma forma, precisamos encontrar uma maneira de tornar nossos projetos resilientes à essas mudanças.


Gerenciamento de dependência

Que tipos de mudanças fazem os projetos apodrecerem? Quando alterações introduzem novas e não planejadas dependências. Cada um dos quatro sintomas mencionados acima é causado direta ou indiretamente por dependências impróprias entre os módulos do software. É a arquitetura de dependência que está se degradando, e com ela, a capacidade do software de ser mantido.

Para evitar a degradação da arquitetura de dependência, as dependências entre os módulos em um projeto devem ser gerenciadas. Esse gerenciamento consiste na criação de firewalls de dependência. Entre esses firewalls, as dependências não se propagam.

O Design Orientado a Objetos está repleto de princípios e técnicas para criar esses firewalls e gerenciar dependências de módulos. São esses princípios e técnicas discutidos aqui. Primeiro, examinaremos os princípios e depois as técnicas ou padrões de design para ajudam a manter a arquitetura de dependência de um aplicativo.



































































































## Os princípios do SOLID

**SRP - Single responsibility principle**
Princípio da Responsabilidade Única - Um objeto deve ter uma, e somente uma, responsabilidade para cuidar.

**OCP - Open/closed principle**
Princípio do Aberto/Fechado - Você deve ser capaz de estender um comportamento de um objeto sem a necessidade de o modificar.

**LSP - Liskov substitution principle**
Princípio da substituição de Liskov - Os objetos derivados devem ser substituíveis por seus objetos base.

**ISP - Interface segregation principle**
Princípio da segregação de interfaces - Muitas interfaces específicas são melhores que uma interface única geral.

**DIP - Dependency inversion principle**
Princípio da inversão de dependência - Dependa de abstrações e não de implementações.














## Orientação a Objeto e Inteface

Por experiência própria, demorei muito entre o dia onde estudei orientação a objeto e o dia onde realmente comecei a pensar em orientação a objeto. 
Se você ainda está a estudar, ou faz pouco tempo, não se preocupe, você, provavelmente vai demorar a entender esta afirmação, pois, é muito mais fácil pensar sem ela.

A base da orientação a objeto em Golang é o **[Struct{}](https://gobyexample.com/structs)**. Na prática, o struct é um tipo definido pelo usuário com a capacidade de agrupar vários outros tipos e funções.

Veja o seguinte código genérico de exemplo:

```
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

Todos os livros lidos por mim se concentravam muito na classe e explicavam um monte de coisas sobre ela, mas, hoje vejo a interface como sendo uma parte muito importante e vou começar por ela.

A interface é um simples contrato de como todas as funções públicas vão ser quando estiverem prontas, por tanto, ela deveria ser a primeira coisa a ser montada em um trabalho em grupo.

Na prática, o grupo vai se reunir e imaginar algo tipo, temos dois grupos de trabalho, o primeiro grupo vai trabalhar nas funcionalidades de como implementar a área de um círculo e o segundo grupo vai implementar as funcionalidades de cálculo da área de um quadrado.
Os grupos discutem e decidem, necessitamos no mínimo de dois métodos, um para definir o valor e outro para pegar o resultado da área.
É nesse ponto onde a interface se mostra extremamente eficiente. Ela é um contrato a ser seguido por todos os grupos, mas, a interface é um contrato de funções mínimas, e não uma armadilha a suas classes. Na prática, a sua classe vai ter obrigatoriamente os mesmos métodos com os mesmos tipos da interface, mas, isto não obriga a ter apenas eles, por isto, na segunda classe há um método a mais, o getRaio().

Agora vamos imaginar o seguinte, existe um terceiro grupo, inesperado, encarregado de montar uma interface gráfica. Obviamente, esse grupo necessita de mais tempo para confeccionar uma interface gráfica surpresa do que os desenvolvedores necessitam para implementar, mas, como em todo projeto, o tempo é muito apertado e eles não podem esperar as funcionalidades ficarem prontas.

A grande beleza da interface é o fato dela permitir dados "mokados", ou seja, dados fantasia próximos ao real e com a finalidade de permitir o grupo da interface gráfica começar a trabalhar enquanto o resto fica pronto.

Por exemplo:

```
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

Como dá para ver no exemplo, a classe **Mokado** compila e é funcional a ponto da equipe de interface gráfica começar a trabalhar e vê se a parte dela funciona como esperado.

A interface também é a base da mudança inesperada de forma mais segura, e falaremos disso mais tarde.

O outro ponto a ser lembrado é o **ISP - Interface segregation principle**, ou princípio da segregação de interfaces - Muitas interfaces específicas são melhores que uma interface única geral.

Na prática, isto diz o seguinte, faça interfaces específicas para grupo de funcionalidades específicas.

Imagine um código de player de vídeo. Ele necessita de um monte de controles de vídeo, tipo, play, pausa, velocidade, legenda, etc.
Você pode fazer uma interface gigante com todas as funcionalidades, provavelmente vai funcionar, mas, pode ser um tiro no pé e o **ISP** é justamente para evitar isto, ou seja, crie uma interface para as funções básicas de vídeo, tipo, play e pausa, e crie outra para as funções de legendas, e assim por diante.

O grande segredo é: divida as suas interfaces em grupos por necessidade.

Agora vamos ver a mesma coisa pelo ponto de vista do Golang antes de continuar.

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

No exemplo temos o equivalente a uma classe escrita em Golang.
Nos livros, você vai ver três formas de escrever uma função associada a um struct, como fiz; com a função do lado de fora, com um ponteiro, simplesmente escrevendo o nome da função após a chave; escrever a função dentro do próprio struct.

Primeira regra, caso você goste de escrever as funções dentro do struct, para você, **Kiss** quer dizer **Keep It Simple, Stupid!**, caso contrario, **Kiss** quer dizer **Keep It Stupid Simple** e não se iluda, se você pensa que isso foi grosseria, espera até uma outra pessoa receber seu código e ouvir algo tipo, você só vai para casa hoje depois disso ficar pronto.

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

Como regra simples, primeira letra maiúscula para nomes de chaves dentro do struct ou nomes de funções as tornam públicas, e letras minúsculas privadas.

**func(el \*Quadrado) Set(comprimento float64)** é uma função pertencente ao struct Quadrado, e **el \*Quadrado** define o termo **el** como sendo o **this** de várias linguagens, onde **el \*Quadrado** permite o valor dentro do struct ser alterado e **el Quadrado**, sem o asterisco de ponteiro, permite apenas a leitura do valor.

No início, eu sempre usava termos mais explicativos para o **el**, tipo, **func(elementoDeArea \*Quadrado) Set(comprimento float64)**, mas, a prática mostrou a necessidade de copiar/colar muito cabeçalho de função, e hoje coloco simplesmente **el** de element.

```golang
  type Area interface {
    Set(comprimento float64)
    Area() float64
  }
```

Já o uso da interface é bem simples, basta apontar o objeto assim: **var variável nomeInterface = &nomeStruct{}**

```golang
  var a Area = &Quadrado{}
      a.Set(16.0)
  fmtPrintf("área: %v\n", a.Area())
```

Para o desenvolvedor, apenas definir o tipo da variável como sendo a interface, **var a Area**, já faz o editor reconhecer e usar o autocompletar.

> Mas, meu código só vai ser desenvolvido por mim...

Nunca cometa o erro de não criar a interface. Tecnicamente, a interface é apenas um contrato, mas, na verdade, ela é um grande salva vidas para quando os parâmetros de projeto mudam do dia para a noite.

Entenda agora a beleza da interface em Golang no exemplo abaixo:

```golang
  var a Area
      a = &Quadrado{}
      a.Set(16.0)
      fmtPrintf("área: %v\n", a.Area())

      a = &Circulo{}
      a.Set(16.0)
      fmt.Printf("área: %v\n", a.Area())
```

Esse é um exemplo bem simples e serve apenas de exemplo, mas, o ponto aqui é o seguinte, a interface **Area** foi feita para calcular área de figuras planas. Logo temos, **a = &Quadrado{}** permite ao ponteiro de interface **a** calcular a área de um quadrado, e **a = &Circulo{}** permite ao mesmo ponteiro calcular a área do circulo apenas mudando uma linha, ou seja, o código pode mudar e crescer de forma segura.

Um exemplo real simples, muito comum e simples de acontecer, o projeto foi feito para usar MySql e já faz dois anos que trabalhamos nele, mas, hoje surgiu um cliente muito grande e ele só trabalha com PostgreSQL e a reunião é para ontem.

Regra simples para poupar muito tempo a você do futuro: sempre monte um objeto em vez de usar o objeto padrão criado por outras pessoas para todos os pontos do código importantes, por mais remota que seja esta possibilidade de mudança um dia, e monte a sua interface para ela.

Exemplo prático:

```golang
  // código original de exemplo
  db, err := sql.Open("mysql", "root:password@tcp(127.0.0.1:3306)/test")
```

Nesse ponto, há vários proplemas, tipo, o MongoDB tem métodos totalmente diferentes e é uma possibilidade bem real de acontecer um dia.
Pode ser que o drive de banco fique obsoleto por algum motivo qualquer. 
Exemplo real, um dia apareceu um texto tipo "esse código não é muito bom e eu não recomendo mais que seja usado" no repositório do drive mais usado para MongoDB em golang e não há obrigação nenhuma de quem fez o drive novo de seguir o drive antigo.

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

Isso dá um pouco de trabalho inicial, mas, isto salva a vida quando algo muda no projeto, e todo programador sabe, o projeto muda o tempo todo.

Então, acredite em mim, meu primeiro computador foi um TK-90X em 1986 e eu nunca vi um projeto grande não mudar no meio.

> Motivação: Lá pelo início dos anos 2000 assinei um contrato pagando muito bem para fazer um projeto em MySql e tudo foi feito no prazo combinado e entregue conforme o contrato. No dia da apresentação técnica para o pessoal da implantação, o técnico responsável diz: nós só trabalhamos com Postgre e o sistema tem de mudar... cobrei um valor bem alto e pedi 30 dias; fui para casa, mudei uma string, testei e segui a vida de forma mais feliz.

Entendeu a beleza da interface em golang? O contrato permite mudanças seguras. Apenas lembre de fazer várias interfaces, uma para cada grupo de funcionalidade.

Vamos agora imaginar uma nova situação, o código do quadrado está em produção e não pode mais ser alterado, mas, nem todo retângulo é um quadrado e você agora necessita fazer alterações:

> Regra da imutabilidade: Uma fez publicado, o código não pode ter métodos e funcionamento alterados.

Há um compromisso sagrado no golang: um código escrito em go 0.1 deve rodar em go 1.14 sem problemas e você deve respeitar isto. Então, comente os métodos obsoletos com **Deprecated:** seguido do texto de explicação e novos métodos a serem usados.

Agora vamos criar o objeto **Retângulo** expandido as funcionalidades do objeto **Quadrado**

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
  
  type Retangulo struct{
    Quadrado
  }
  
  func(el *Retangulo) SetAltura(comprimento float64) {
    
  }
  
  func(el *Retangulo) SetComprimento(comprimento float64) {
  
  }
  
  func test() {
    var a AreaComplexa = &Retangulo{}
    a.SetAltura(1.0)
    a.SetComprimento(1.0)
    a.Area()
  }
  
  type AreaComplexa interface {
    SetAltura(comprimento float64)
    SetComprimento(comprimento float64)
    Area() float64
  }
  
  type Area interface {
    Set(comprimento float64)
    Area() float64
  }

```
