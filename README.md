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

O **Kiss - Keep It Stupid Simple / Keep It Simple, Stupid!**, o **SOLID** do Robert C. Martin, também conheciso por Uncle Bob e o **Cognitive Complexity** do Sr Thomas J. McCabe simplesmente resumem a regra de ouro e todo programador um dia passa a entender a regra de ouro, mesmo sem conhecer os trabalhos deles.

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

Porém, além de tudo, a interface também é a base da mudança inesperada de forma mais segura, e falaremos disso mais tarde.

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

Como regra simples, a primeira letra maiúscula para nomes de chaves dentro do struct ou nomes de funções as tornam públicas, e letras minúsculas privadas.

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

> Meu código só vai ser desenvolvido por mim e eu não necessito disso...

Nunca cometa o erro de não criar a interface. Tecnicamente, a interface é apenas um contrato, mas, na verdade, ela é um grande salva-vidas para quando os parâmetros de projeto mudam do dia para a noite.

Entenda agora a beleza da interface em Golang no exemplo abaixo:

```golang
  var a Area
      a = &Quadrado{}
      a.Set(16.0)
      fmtPrintf("área: %v\n", a.Area())
      
      // circulo é um objeto completamente diferente
      a = &Circulo{}
      a.Set(16.0)
      fmt.Printf("área: %v\n", a.Area())
```

Esse é um exemplo bem simples e serve apenas de exemplo, mas, o ponto aqui é o seguinte, a interface **Area** foi feita para calcular área de figuras planas. Logo temos, **a = &Quadrado{}** permite ao ponteiro de interface **a** calcular a área de um quadrado, e **a = &Circulo{}** permite ao mesmo ponteiro calcular a área de um circulo, apenas mudando uma linha, ou seja, o código pode mudar e crescer de forma segura.

Um exemplo real simples, muito comum e simples de acontecer, o projeto foi feito para usar MySql e já faz dois anos que trabalhamos nele, mas, hoje surgiu um cliente muito grande e ele só trabalha com PostgreSQL e a reunião é para ontem.

Regra simples para poupar muito tempo a você do futuro: sempre monte um objeto em vez de usar o objeto padrão criado por outras pessoas para todos os pontos do código importantes, por mais remota que seja esta possibilidade de mudança, e monte a sua interface para ela.

Exemplo prático:

```golang
  // código original de exemplo
  db, err := sql.Open("mysql", "root:password@tcp(127.0.0.1:3306)/test")
```

Nesse ponto, há vários problemas, tipo, o MongoDB tem métodos totalmente diferentes e é uma possibilidade bem real de acontecer um dia.
Pode ser que o drive de banco fique obsoleto por algum motivo qualquer. 
Exemplo real, um dia apareceu um texto tipo "esse código não é muito bom e eu não recomendo mais que seja usado" no repositório do drive mais usado para MongoDB em golang e não há obrigação nenhuma de quem fez o novo drive de seguir o drive antigo.

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

Apenas para deixar bem claro, crie um encapsulamento para todos os códigos críticos e tente deixar o objeto dele com funções genéricas, assim, você pode usar uma interface e apenas mudar o ponteiro do objeto sem que houver necessidade de mudanças críticas no código.

> Motivação: Lá pelo início dos anos 2000 assinei um contrato pagando muito bem para fazer um projeto em MySql e tudo foi feito no prazo combinado e entregue conforme o contrato. No dia da apresentação técnica para o pessoal da implantação, o técnico responsável diz: nós só trabalhamos com Postgre e o sistema tem de mudar... cobrei um valor bem alto e pedi 30 dias; fui para casa, mudei uma string, testei e segui a vida de forma mais feliz.

Entendeu a beleza do encapsulamento junto com interface em golang? O contrato permite mudanças seguras. Apenas lembre de fazer várias interfaces, uma para cada grupo de funcionalidade.

## LSP - Liskov substitution principle
Princípio da substituição de Liskov - Os objetos derivados devem ser substituíveis por seus objetos base.

Quando a gente vem de hardware, a gente aprende a otimizar todo o código, mas, certas otimizações de desempenho não são muito legais para a organização do código, principalmente para bancos de dados e afins.

Por exemplo, muitos programadores usam o JSon, JavaScript Object Notation, já os drivers do MongoDB usam o BSon, JSon binário, os bancos SQL devolvem valores próprios do drive, e assim vai, cada um faz de um modo.

O problema disso é a compatibilidade, também conhecida como portabilidade do código.

Por exemplo, o SQL Server tem o tipo **mssql.UniqueIdentifier**, mas, na verdade, este tipo é um **[16]byte**, definido por **type UniqueIdentifier [16]byte**.

Veja o exemplo abaixo tirado de um parser de SQL para MongoDB.

```golang
type Client struct {
	ID                      int
	Phone                   sql.NullString
	Email                   string
	Password                string
	UniqueID                mssql.UniqueIdentifier
}
```

Esse struct usa os tipos, não nativos do golang, **sql.NullString** e **mssql.UniqueIdentifier** para arquivar dados e isto deixa o código não portável.

A maneira de resolver isto é dividir o software em camadas. Lembre-se, arquitetura de software é multicamada, por isso, multicamada é a primeira coisa dita por Uncle Bob no seu manifesto do **SOLID**.

No final das contas, tanto o Uncle Bob quanto o Liskov dizem para você dividor o seu código em camadas distintas.
Por exemplo, vamos pegar dados de um banco SQL Server e devolver esse dado a nossa aplicação. A forma mais fácil E ERRADA DE FAZER ISTO é ler o dado e usar ele na forma nativa imaginada pelo criador do drive. A única forma de deixar o código reaproveitável é criar uma camada de dados e converter o dado para um formato nativo do golang.

Por exemplo, **sql.NullString** pode virar

```golang

  type NullString struct {
    String string
    Valid  bool
  }

```
 
e **mssql.UniqueIdentifier** pode virar
 
```golang

type UniqueIdentifier [16]byte

```

Na prática, você vai montar um pequeno módulo seu com os tipos nativos e todos os dados vão passar por este módulo.
 
```
  consumidor           modulo                 banco            
  +--------------+     +---------------+      +---------------+
  |              |     |               |      |               |
  |    formato   |     |  parser para  |      |  inserção do  |
  |    nativo    | --> |  formato do   | -->  |    dado no    |
  |    golang    |     |     banco     |      |     banco     |
  |              |     |               |      |               |
  +--------------+     +---------------+      +---------------+

  banco                modulo                 consumidor
  +--------------+     +---------------+      +---------------+
  |              |     |               |      |               |
  |  leitura do  |     |  parser para  |      |  dado pronto  |
  |   dado no    | --> |    formato    | -->  |   para uso    |
  |    banco     |     |    nativo     |      |               |
  |              |     |               |      |               |
  +--------------+     +---------------+      +---------------+

```

Uma dica são as funções **MarshalJSON() ([]byte, error) {...}** e **UnmarshalJSON(data []byte) error{...}** para fazer o parser personalizado do JSon de forma a atender todas as suas necessidades. 

A grande questão do JSon são dois pontos de vista, a conversão de dados deixa o processamento mais lento, mas, ao mesmo tempo, ela deixa o código modular e independente. Veja o caso do Linux, você pode ter uma interface gráfica bonita instalando o Ubuntu ou uma interface gráfica leve instalando o Lubuntu, onde os dois usam os mesmos núcleos de código e todas as informações entre ambiente gráfico e comando são passados por um texto padronizado. Por outro lado, o fato do Ubunto ser modular de mais faz o desempenho dele não ser muito bom para jogos.

```golang

    type Time struct {
      time.Time
    }
    
    func (t Time) MarshalJSON() ([]byte, error) {
      return json.Marshal(t.Time.Unix())
    }
    
    func (t *Time) UnmarshalJSON(data []byte) error {
      var i int64
      if err := json.Unmarshal(data, &i); err != nil {
        return err
      }
      t.Time = time.Unix(i, 0)
      return nil
    }

```

Vamos ao exemplo prático: a nossa aplicação tem um módulo de cliente com as seguintes regras:

| Campo          | Descrição                                                                                                         |
|----------------|-------------------------------------------------------------------------------------------------------------------|
| Id             | inteiro maior do que zero (16 bytes)                                                                              |
| Phone          | string ou nil (opcional)                                                                                          |
| Email          | string                                                                                                            |
| Password       | string                                                                                                            |

É início de projeto e vamos usar um banco SQL, tipo SQL Server, logo, o struct Client pode facilmente ser 

```golang
    type Client struct {
      Id                      mssql.UniqueIdentifier
      Phone                   sql.NullString
      Email                   string
      Password                string
    }
```

Como você poder ver, **client** vai atender todas as nossas necessidades atuais e você vai terminar logo, claro, o código não é portável e usa dois tipos nativos de drive de banco SQL, **mssql.UniqueIdentifier** e **sql.NullString**, mas, este é um problema para você do futuro.

Como o futuro é amanhã e estamos vivendo o hoje, basta fazer algo tipo

```golang
      var id mssql.UniqueIdentifier
      id.Scan(1)
      
      var phone sql.NullString
      phone.Scan("123456")
      
      var a = Client{
        Id: id,
        Phone: phone,
        Email: "user@company.com",
        Password: "pass",
      }
```

Como você pode ver, foi simples e prático popular **client** com dados e inserir no banco. Claro, estamos falando de um sistema complexo com várias tabelas grandes.

O problema, o código não é portável e agora estamos no futuro! Fechamos contrato com uma empresa muito grande, pagando muito bem, mas, a empresa usa um banco noSQL e você não lembra mais como esse código foi feito (isto é um exemplo bem real, acredite em mim!).

Ates de proceguir, um problema de usar códigos de terceiros, são pequenos erros, tipo, **sql.NullString** é na verdade

```golang
    type NullString struct {
      String string
      Valid  bool // Valid is true if String is not NULL
    }
```

Porém, **String** é reservado pelo golang, mas, o compilador vai aceitar a construção **String string** dentro do **struct**. O problema disso é fato de todo typo criado pelo desenvolvedor aceitar a função **func (el novoTipo) String() string {...}** como sendo uma função automática para converter o tipo em string, por exemplo, **fmt.Printf("%v", novoTipo)**.

> **func (el novoTipo) String() string {...}** não tem ponteiro, ou seja, não pode ser **el \*novoTipo**

Vamos fazer a mesma coisa do modo certo e explicar:

Primeiro você vai criar um módulo **client** na sua estrutura de código, mais ou menos assim:

```golang
    // este é im arquivo dentro do módulo client
    type UniqueIdentifier [16]byte
    
    func(el *UniqueIdentifier) Set(value interface{}) {
    
      // faz a conversão de tipos
      switch converted := value.(type) {
      case nil:
        *el = [16]byte{0x00}
    
      // todo: fazer outros tipos (int, uint, float, ...)
      case int64:
        b := make([]byte, 16)
        binary.LittleEndian.PutUint64(b, uint64(converted))
        for i := 0; i != 16; i += 1 {
          el[i] = b[i]
        }
    
      case string:
        v, _ := strconv.Atoi(converted)
        el.Set(int64(v))
      }
    }
    
    // apenas a função String() funciona de forma automática, Int64() é só para deixar 
    // organizado
    func(el UniqueIdentifier) Int64() int64 {
      b := make([]byte, 16)
      for i := 0; i != 16; i += 1 {
        b[i] = el[i]
      }

      // BigEndian e LittleEndian é a ordem como os bits são organizados, da direita para 
      // a esqueda ou da esqueda para a direita
      // Basta respeitar a mesma ordem para recuperar os dados
      // Essa tecnica permite transformar qualquer dado em binário e arquivar.
      return int64(binary.LittleEndian.Uint64(b))
    }
    
    // Eu sempre faço a função String() para ajudar na hora do debug
    func(el UniqueIdentifier) String() string {
      b := make([]byte, 16)
      for i := 0; i != 16; i += 1 {
        b[i] = el[i]
      }
      i := int64(binary.LittleEndian.Uint64(b))
      return strconv.FormatInt(i, 10)
    }
```

```golang
    // este é im arquivo dentro do módulo client
    type NullString struct {
      // Acredito que o termo certo seria protected para value e valid, em vez de privade
      value string

      // valid is true if String is not NULL
      valid bool 
    }
    
    func(el *NullString) Set(value interface{}) {
    
      el.valid = true
    
      switch converted := value.(type) {
      case nil:
        el.value = ""
        el.valid = false
    
      // todo: fazer outros tipos (int, uint, float, ...)
      case int64:
        el.value = strconv.FormatInt(converted, 10)
    
      case string:
        el.value = converted
      }
    }
    
    func(el NullString) String() string {
      if el.valid == false {
        return "nil string"
      }
    
      return el.value
    }
```

```golang
    // este é im arquivo dentro do módulo client
    type Client struct {
      ID                      UniqueIdentifier
      Phone                   NullString
      Email                   string
      Password                string
    }
    
    func (el Client) ToDb() ClientSql {
      var id mssql.UniqueIdentifier
      id.Scan(el.ID.Int64())
    
      // el.Phone.'v'alue, funciona apenas dentro do mesmo módulo
      var phone sql.NullString = struct {
        String string
        Valid  bool
      }{String: el.Phone.value, Valid: el.Phone.valid}
    
      return ClientSql{
        ID: id,
        Phone: phone,
        Email: el.Email,
        Password: el.Password,
      }
    }
```

```golang   
    // este é im arquivo dentro do módulo client
    type ClientSql struct {
      ID                      mssql.UniqueIdentifier
      Phone                   sql.NullString
      Email                   string
      Password                string
    }
```

Antes de começar a explicar o código acima, vamos criar dentro da sua estrutura de código um módulo chamado **factoryClient**. Esse é um padrão de boas práticas de software e não é usado só pelo golang. A ideia do factory é simplificar a inicialização de objetos muito complexos. O outro ponto, é golang não aceita sobrecarga de métodos, aquele monte de funções com o mesmo nome e tipos definidos, pois, a turma do golang deixa bem claro dois pontos, sobrecarga pode causar erros difíceis de serem percebidos em códigos complexos e golang não aceita parâmetros opcionáis peno mesmo motivo. Então, a saída criar dentro do módulo factory um monte de função iniciadas por **New** + **NomeFunção**.

> O módulo **factory** sempre deve começar pela palavra **factory** e ser concatenado com o nome do módulo pai, assim, basta começar a digitar **factory** e deixar a magia do autocompletar atuar.

```golang
    // módulo factoryClient

    //Create a new Client with id, phone, email and password
    func New(id, phone interface{}, email, password string) *Client {
      var idConverted UniqueIdentifier
      idConverted.Set(id)
    
      var phoneConverted NullString
      phoneConverted.Set(phone)
    
      // golang não deixa você cometer os principais erros do C, ou seja, este é um 
      // ponteiro válido, pois, o retorno da função não limpa a memória, quem limpa é o 
      // garbage collector.
      return &Client{
        ID: idConverted,
        Phone: phoneConverted,
        Email: email,
        Password: password,
      }
    }

    //Create a new Client with id, email and password (without phone)
    func NewWithoutPhone(id interface{}, email, password string) *Client {
      var idConverted UniqueIdentifier
      idConverted.Set(id)
    
      var phoneConverted NullString
      ph.Set(nil)
    
      return &Client{
        ID: idConverted,
        Phone: phoneConverted,
        Email: email,
        Password: password,
      }
    }
```

A grande magia do factory sempre vai ser vista pelo seu eu do futuro, aquela mesma pessoa doida para ir viver um pouco e sem a menos lembrança de que código é este, graças a magia do autocompletar.

```golang
    var client1 = factoryClient.New(1, 123456, "mail@company.com", "pass")
    var client2 = factoryClient.NewWithoutPhone(1, "mail@company.com", "pass")
```

Estamos no futuro, e **client** necessita ser migrado para outra plataforma noSQL e o código legado está bem feito.

> Código legado não quer dizer código ruim, só que dizer, a gente não usa mais este código. Código ruim é sinonimo de inexperiência. 

## OCP - Open/closed principle
Princípio do Aberto/Fechado - Você deve ser capaz de estender um comportamento de um objeto sem a necessidade de o modificar.

```golang
    type ClientGeneric struct {
      Client
    }

    func (el Client) ToDb() ClientNoSql {...}
```

Isso é o mesmo de 

```
    class ClientGeneric extends Client {
      override function ToDb() :ClientNoSql {...}
    }
```

Percebe como ficou fácil? Quando você coloca um tipo dentro do outro, o novo tipo herda todas as propriedades e métodos, então, basta reescrever apenas o necessário. 

```golang
    var c ClientGeneric
    c.Password = "pass"
```

Há ainda duas outras formas de modificar um struct. A primeira forma funciona desde que os structs envolvidos techam chaves de nomes diferentes.

```golang
    type ClientGeneric struct {
      Client
      OutroStruct
    }
```

Caso contrário, basta adicionar uma chave com um novo nome para pelo menos uma das chaves em conflito.

```golang
    type ClientGeneric struct {
      NovoNome Client
      NomeOpcional OutroStruct
    }
```

Logo

```golang
    var c ClientGeneric
    c.NovoNome.Password = "pass"
```
