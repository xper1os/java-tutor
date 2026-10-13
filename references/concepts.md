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
