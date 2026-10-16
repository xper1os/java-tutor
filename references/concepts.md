# Conceitos: como explicar

Formato padrão de explicação (máx. ~15 linhas):
1. **Em uma frase**: o que é.
2. **Analogia** do dia a dia.
3. **Exemplo mínimo** (3–10 linhas), de preferência no contexto do projeto do aluno.
4. **Armadilha comum** (1 linha).
5. **Mini exercício** (o aluno faz).

---

## JDK, JRE, JVM, bytecode
- **JVM**: a "máquina virtual" que executa programas Java. Analogia: um console de videogame — o jogo (bytecode) roda em qualquer console (JVM) de qualquer TV (Windows, Linux, Mac).
- **Bytecode** (`.class`): o código traduzido pelo `javac` para a linguagem da JVM.
- **JDK**: kit do desenvolvedor = compilador (`javac`) + JVM (`java`) + bibliotecas.
- `java Main.java` compila em memória e roda (atalho para estudo). `javac` + `java` é o fluxo "real".

## Variáveis e tipos
- Variável = caixa com etiqueta (nome) e formato (tipo). `int idade = 30;`
- Primitivos: `int`, `long`, `double`, `boolean`, `char` — guardam o **valor** direto.
- `String` (e todo objeto) — a variável guarda uma **referência** (o "endereço") do objeto.
- **`null` só existe para classes.** `null` = "não aponta para nenhum objeto". `String nome = null;` compila; `int total = null;` **não** (`incompatible types: <null> cannot be converted to int`) — primitivo sempre tem um valor (atributo `int` não inicializado vale `0`, `boolean` vale `false`, objeto vale `null`). Cada primitivo tem sua **classe empacotadora** (*wrapper*), que aceita `null`: `int`→`Integer`, `double`→`Double`, `boolean`→`Boolean`, `char`→`Character`, `long`→`Long`. Analogia SQL: primitivo = coluna `NOT NULL`; classe = coluna que aceita `NULL`. Consequência prática: ao validar um parâmetro `String`, testar `== null` **antes** de chamar método nele (`titulo == null || titulo.isBlank()`), senão `NullPointerException`. (Mais tarde: *autoboxing* — `Integer x = null; int y = x;` compila e quebra com NPE ao rodar; listas só guardam classes: `List<Integer>`, nunca `List<int>`.)
- `var` deixa o compilador deduzir o tipo, mas o tipo continua fixo: `var x = 10; x = "oi";` não compila.
- Armadilhas: `5 / 2` é `2` (divisão inteira); `0.1 + 0.2` não é exatamente `0.3` (para dinheiro "de verdade" use `BigDecimal` — mencione na Fase 3+, não exija antes).

## Tipagem estática
Java confere os tipos **antes** de rodar. Analogia: um formulário que não deixa você digitar letras no campo CPF. Muitos erros aparecem já na compilação — isso é bom.

## if / switch / loops
- `if` = bifurcação na estrada. `switch` = elevador com botões (cada `case` é um andar).
- `while` = "enquanto a condição for verdadeira, repita" (não sabe quantas vezes). `for` = "repita N vezes" (sabe quantas). `for-each` = "para cada item da lista".
- Armadilha: loop infinito por esquecer de atualizar a condição; `=` (atribuir) vs `==` (comparar).

## Métodos
- Método = receita com nome. Parâmetros = ingredientes. Retorno = o prato pronto. `void` = receita que faz algo mas não "devolve" nada (ex.: imprimir).
- Escopo: variável criada dentro de um método só existe ali dentro (como o que acontece em Vegas...).
- Bom método: nome com verbo (`calcularTotal`), faz **uma** coisa, cabe na tela.

## Classe e objeto
- **Classe** = forma de bolo / planta de uma casa. **Objeto** = o bolo / a casa construída. `new` = construir.
- Atributos = características (cor, tamanho). Métodos = comportamentos (abrir porta).
- **Construtor** = o que acontece no momento em que o objeto nasce; garante que ele nasce válido.
- **`this`** = "eu mesmo" (o objeto atual). `this.valor = valor;` → "o MEU valor recebe o valor que veio de fora".

## Encapsulamento
- `private` + métodos públicos = caixa eletrônico: você não mexe no cofre direto, usa as operações permitidas, que validam.
- Benefício: garante regras (valor nunca negativo) num lugar só.

## Object, herança mínima, `@Override` e `toString()`
> Tópico que costuma travar: o aluno acerta as previsões mas se perde na hora de **escrever** o `toString`. Motivo: o passo junta 4 ideias novas de uma vez (herança, sobrescrever, assinatura exata, `return` de String). **Separe em etapas** (ver Fase 3 no `roadmap.md`) e explique o "por que `return` e não `println`" **antes** de pedir o código, não como pergunta surpresa depois.

1. **Provocar primeiro**: `System.out.println(t1);` sem `toString` → `Tarefa@29176cc1`. Pergunte antes de rodar: "o que vai sair?". Esse texto vem de algum lugar: o `println` chama `t1.toString()`, que a `Tarefa` **herdou**.
2. **Herança mínima, fora do projeto** (o aluno ainda não viu `extends`): `class Cachorro extends Animal` = o filho **recebe tudo** da mãe (herda a casa) e pode **reformar um cômodo** (sobrescrever um método). Exemplo que funcionou:
   ```java
   class Animal   { String som() { return "..."; } }
   class Cachorro extends Animal { @Override String som() { return "Au au!"; } }
   class Peixe    extends Animal { }   // herda e NÃO reforma
   ```
   **Regra da busca**: o Java procura o método **na classe do objeto**; se não acha, **sobe para a mãe**. `new Cachorro().som()` → `Au au!`; `new Peixe().som()` → `...`. Peça para o aluno prever as duas saídas.
3. **`@Override` = pedido de conferência**, não é ele que sobrescreve. Mostre o erro de digitação: `String Som()` **sem** `@Override` compila calado (vira método novo, o bug passa despercebido); **com** `@Override` → `does not override or implement a method from a supertype`. Por isso o mercado usa `@Override` sempre.
4. **Ligar ao projeto**: toda classe sem `extends` herda de **`Object`** (a "mãe de todas"). Tabela de paralelo: `Animal`→`Object`, `som()`→`toString()`, `Peixe` (não reformou)→`Tarefa` hoje (por isso o `Classe@hash`). O número depois do `@` vem do endereço na memória e muda a cada execução.
5. **Por que `return` e não `println`** (explicar antes de pedir o código):
   - a assinatura do `Object` promete **devolver** uma `String` → sem `return` dá `missing return statement`;
   - quem chama decide o que fazer com o texto (imprimir, montar outra String, gravar em arquivo, mandar para a web). Analogia SQL: um `SELECT` **devolve** linhas; quem chamou decide se mostra, exporta ou grava. Conecte a algo que o aluno já fez: "calcular" (return) separado de "mostrar" (println);
   - **o `+` com objeto também chama `toString()`**: `"Pendente: " + t2` → `Pendente: [ ] Fazer o README`. Ótimo para conferir se entendeu.
6. **Assinatura exata**: `public String toString()`, sem parâmetros. `public` é obrigatório porque não se pode **reduzir** o acesso herdado (sem ele: `attempting to assign weaker access privileges; was public`).
- Armadilhas: `tostring`/`ToString` sem `@Override` (compila, nunca é chamado); imprimir dentro do `toString`; `"..." + this` dentro do próprio `toString` → chama a si mesmo infinitamente → `StackOverflowError`.
- Analogia extra se ainda não clicar: o `Object` tem uma "ficha de apresentação" padrão e genérica (`Tarefa@29176cc1`, como um crachá só com o número do funcionário); o `toString` próprio é preencher o crachá com nome e situação.

## static
- `static` = pertence à **classe**, não a cada objeto. Analogia: o regulamento do condomínio (um só, compartilhado) vs o apartamento de cada morador.
- Por que `main` é `static`: a JVM precisa chamá-lo sem ter criado nenhum objeto antes.
- Erro clássico: chamar método não-static de dentro do `main` static (ver `common-errors.md`).

## record e enum
- `record Gasto(String descricao, double valor) {}` = classe de dados imutável com construtor, getters (`descricao()`), `equals`, `hashCode` e `toString` prontos.
- `enum` = lista fechada de opções (como os naipes do baralho). Evita erro de digitação de Strings ("mercdo").

## Referências, stack e heap (Raio-X)
- **Stack (pilha)**: variáveis locais e chamadas de métodos. Cada chamada empilha um "quadro"; ao terminar, desempilha. Analogia: pilha de pratos.
- **Heap**: onde moram os objetos criados com `new`. A variável na stack guarda só a seta para o objeto no heap.
```
Gasto a = new Gasto("Pizza", 50);
Gasto b = a;          // b aponta para o MESMO objeto
b.setValor(60);       // a.getValor() agora também é 60!

 STACK            HEAP
 a ──────┐
         ├──▶ [Gasto: "Pizza", 60]
 b ──────┘
```
- `==` compara as setas (mesmo objeto?). `.equals()` compara o conteúdo. Por isso Strings se comparam com `.equals()`.
- `null` = seta que não aponta para nada. Usar `.` numa seta vazia → `NullPointerException`.
- **Garbage collector**: objetos sem nenhuma seta apontando são recolhidos automaticamente.

## Coleções
- Array = estacionamento com número fixo de vagas. `ArrayList` = fila que cresce sozinha. `Map` = agenda de contatos (chave → valor). `Set` = lista sem repetidos.
- Generics `<Gasto>`: a etiqueta "aqui só entra Gasto" — o compilador barra o resto.
- Armadilha: índices começam em 0; remover item de uma lista enquanto percorre com for-each → `ConcurrentModificationException`.

## Exceções
- Exceção = alarme de incêndio: algo deu errado, a execução normal para e o alarme "sobe" pelos métodos até alguém tratar (`catch`). Se ninguém tratar, o programa cai e mostra o *stack trace*.
- **Checked** (ex.: `IOException`): o compilador obriga a tratar ou declarar (`throws`). **Unchecked** (`RuntimeException`): erro de programação, não obriga.
- Não use `catch (Exception e) {}` vazio — engolir erro é esconder o problema.

## Interface e polimorfismo
- Interface = contrato / tomada padrão: qualquer aparelho com o plugue certo funciona. `GastoRepository` promete `salvar` e `listar`; memória, arquivo ou banco cumprem do seu jeito.
- Polimorfismo = o mesmo comando (`repositorio.salvar(g)`) com comportamentos diferentes dependendo do objeto real.
- Herança (`extends`) = "é um" (Cachorro é um Animal). Prefira composição ("tem um") na maioria dos casos.

## Lambdas e Streams
- Lambda = função curta e sem nome que você passa como argumento: `g -> g.valor() > 100` ("dado um g, responda se o valor é maior que 100").
- Stream = esteira de fábrica: os itens passam por estações (`filter` → `map` → `sorted`) e no fim são coletados (`toList`, `sum`).
- Stream não altera a lista original.

## Build, dependências e testes
- Maven = gerente de obra: baixa as dependências (bibliotecas), compila, testa e empacota seguindo o `pom.xml` (a planta da obra).
- Teste automatizado = um programa que confere se o seu programa faz o que deveria. Roda em segundos, sempre igual.

## JDBC e banco
- JDBC = o "tradutor" padrão entre Java e qualquer banco SQL. `Connection` (ligação), `PreparedStatement` (comando com lacunas `?`), `ResultSet` (as linhas que voltaram).
- `?` em vez de concatenar Strings → evita SQL injection.

## Spring Boot
- Framework = uma casa pré-montada: você decora e põe os móveis (suas regras), a estrutura (servidor web, conexão com banco) já vem.
- Injeção de dependência = em vez de cada classe criar o que precisa com `new`, o Spring entrega pronto (como um restaurante: você pede o prato, não vai na cozinha buscar os ingredientes).
- Fluxo de uma requisição: navegador → `GET /gastos` → Controller → Service → Repository → banco → volta o JSON.
