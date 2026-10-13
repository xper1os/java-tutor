# Roadmap do projeto

Um único projeto, construído em fases. Cada fase tem: **conceitos**, **passos** (cada passo = 1 conceito + 1 tarefa pequena), **entrega** (o que o app passa a fazer) e **checkpoint**.

Os exemplos usam o projeto "Controle de Gastos" (entidade `Gasto`). Para outro projeto, troque as entidades (ver `project-ideas.md`) — a sequência é a mesma.

Estrutura de pastas ao longo do tempo:
```
Fases 0–2:  meu-app/Main.java
Fases 3–7:  meu-app/src/  (vários .java, depois pacotes: model/, repository/, service/, ui/)
Fase 8+:    projeto Maven (pom.xml, src/main/java, src/test/java)
Fase 10:    projeto Spring Boot (gerado pelo start.spring.io)
```

---

## Fase 0 — Ambiente e primeiro programa
**Conceitos**: o que é Java, JDK, JVM, bytecode; compilar vs executar; terminal; editor.
**Passos**
1. Conferir `java -version` (JDK 25 já instalado). Criar a pasta do projeto. Abrir no VS Code (instalar "Extension Pack for Java" se ainda não tiver).
2. Primeiro programa com `void main() { IO.println("Olá!"); }` → rodar com `java Main.java`.
3. Mudar a mensagem, imprimir 3 linhas, provocar um erro de propósito (tirar um `;`) e ler a mensagem do compilador.
4. Raio-X: `javac Main.java` gera `Main.class` (bytecode) → `java Main` roda na JVM. Por que existe esse passo intermediário ("escreva uma vez, rode em qualquer lugar").
**Entrega**: o app imprime o nome dele e uma mensagem de boas-vindas.
**Checkpoint**: Qual a diferença entre JDK e JVM? O que tem dentro de um `.class`? O que o `javac` faz?

## Fase 1 — Fundamentos: variáveis, entrada e decisões
**Conceitos**: variáveis e tipos (`int`, `double`, `boolean`, `String`, `var`) — **já no passo 1, deixar claro: tipos primitivos (minúsculos, guardam o valor) vs `String`, que é uma CLASSE (maiúscula); e que `Integer`, `System`, `IO` também são classes (tudo com maiúscula antes do ponto)**. Não adiar essa distinção para a Fase 3; **métodos úteis de `String`** (`length()`, `toUpperCase()`, `trim()`, `isBlank()`, `contains()`, `equals()`) e como descobri-los (autocomplete após o `.`, Ctrl+Q no IntelliJ) — Strings são imutáveis: o método devolve uma NOVA String; operadores; concatenação; leitura do teclado (`IO.readln`, depois `Scanner`); conversão (`Integer.parseInt`, `Double.parseDouble`); `if/else`; `switch` moderno (`case 1 ->`); a forma clássica `public static void main(String[] args)`.
**Passos**
1. Variáveis: guardar e imprimir nome do usuário, saldo inicial.
2. Ler o nome do teclado e cumprimentar.
3. Ler um valor numérico, converter, fazer contas (somar gasto, calcular saldo).
4. `if/else`: avisar se o saldo ficou negativo.
5. Menu com `switch`: "1 - Adicionar gasto, 2 - Ver saldo, 0 - Sair".
6. Converter para a forma clássica (`public class Main`, `public static void main`, `System.out.println`) e entender cada palavra (sem aprofundar `static` ainda).
**Entrega**: menu que lê uma opção e responde (uma vez só).
**Checkpoint**: diferença entre `int` e `double`; por que `"5" + 3` dá `"53"`; prever a saída de um `if` aninhado; desafio: opção "3 - Ver se estourou o orçamento".

## Fase 2 — Repetição e métodos
**Conceitos**: `while`, `do-while`, `for`; `break`/`continue`; métodos (parâmetros, retorno, `void`); escopo de variáveis; dividir o programa em partes.
**Passos**
1. Menu em loop até o usuário escolher 0 (`while`).
2. `for`: imprimir uma tabela simples (ex.: parcelas de um gasto).
3. Extrair cada opção do menu para um método (`mostrarMenu()`, `lerValor()`).
4. Métodos com retorno: `double calcularSaldo(double saldo, double gasto)`.
5. Raio-X: pilha de chamadas — o que acontece quando um método chama outro; por que a variável de dentro do método "some" ao sair.
**Entrega**: menu que fica rodando, código organizado em métodos.
**Checkpoint**: quando usar `for` vs `while`; o que é escopo; prever a saída de um loop; desafio: validar que a opção digitada existe e repetir a pergunta se não existir.

## Fase 3 — Orientação a objetos: classes e objetos
**Conceitos**: classe vs objeto (forma de bolo vs bolo); atributos; construtor; `new`; `this`; métodos de instância; encapsulamento (`private` + getters); `toString()`; `record`; `enum`; referências (variável guarda o "endereço" do objeto); `static` explicado de verdade.
**Passos**
1. Criar `Gasto.java` com descrição, valor e data (`LocalDate`); construtor; criar objetos no `main`.
2. Encapsular: atributos `private`, getters, validação no construtor (valor > 0).
3. `toString()` para imprimir bonito.
4. `enum Categoria { MERCADO, TRANSPORTE, LAZER, ... }` e usar no `Gasto`.
5. Reescrever `Gasto` como `record` e comparar (quando usar cada um).
6. Raio-X: stack vs heap — duas variáveis apontando para o mesmo objeto; `==` vs `.equals()`.
**Entrega**: o app cria gastos como objetos (ainda um por vez).
**Checkpoint**: classe vs objeto; por que `private`; o que `this` significa; `==` vs `equals` com Strings; desafio: classe `Orcamento` com limite e método `estourou(double total)`.

## Fase 4 — Coleções: guardando muitos dados
**Conceitos**: arrays (e seus limites); `List`/`ArrayList`; generics básico (`List<Gasto>`); `for-each`; `Map`/`HashMap`; remover/buscar; índices.
**Passos**
1. Array de 3 gastos fixos → perceber o problema do tamanho fixo.
2. `ArrayList<Gasto>`: adicionar pelo menu e listar todos.
3. Total gasto (percorrer e somar).
4. Buscar por descrição; remover por número da lista.
5. `Map<Categoria, Double>`: total por categoria.
**Entrega**: CRUD em memória (adicionar, listar, buscar, remover, totais). 🎉 Primeiro app "de verdade".
**Checkpoint**: array vs `ArrayList`; o que é `<Gasto>`; quando usar `Map`; desafio: listar só os gastos acima de um valor.

## Fase 5 — Exceções e validação
**Conceitos**: o que é exceção; *stack trace*; `try/catch/finally`; exceções comuns (`NumberFormatException`, `NullPointerException`, `IndexOutOfBoundsException`); checked vs unchecked; `throw`; criar exceção própria.
**Passos**
1. Digitar "abc" no valor → ler o *stack trace* juntos.
2. `try/catch` para pedir o valor de novo.
3. Validar índice ao remover.
4. `throw new IllegalArgumentException` no construtor de `Gasto`; tratar no menu.
5. Exceção própria `GastoInvalidoException`.
**Entrega**: o app não "quebra" com entrada errada.
**Checkpoint**: ler um *stack trace* e achar a linha do aluno; checked vs unchecked; desafio: tratar data inválida.

## Fase 6 — Lambdas e Streams
**Conceitos**: interfaces funcionais (ideia); lambda (`g -> g.valor() > 100`); `stream()`, `filter`, `map`, `sorted`, `Comparator.comparing`, `sum`/`mapToDouble`, `collect`/`toList`, `groupingBy`; `Optional` básico.
**Passos**
1. Reescrever "total gasto" com stream e comparar com o `for`.
2. Filtrar por categoria; ordenar por valor/data.
3. Relatório: maior gasto, média, total por mês (`groupingBy`).
**Entrega**: menu de relatórios.
**Checkpoint**: traduzir um `for` para stream e vice-versa; prever o resultado de um pipeline; desafio: top 3 maiores gastos.

## Fase 7 — Organização, interfaces e arquivos
**Conceitos**: pacotes e `import`; separar responsabilidades (camadas: `model`, `repository`, `service`, `ui`); `interface` e polimorfismo; herança vs composição (ideia); ler/gravar arquivos com `java.nio.file.Files` (CSV); `try-with-resources`; compilar vários arquivos (`javac -d out` + `java -cp out`).
**Passos**
1. Mover classes para pacotes; compilar e rodar com vários arquivos.
2. Criar `GastoService` (regras) e deixar `Main` só com o menu.
3. `interface GastoRepository` + `GastoRepositoryMemoria`.
4. `GastoRepositoryArquivo`: salvar em `gastos.csv` ao sair, carregar ao abrir.
5. Trocar a implementação em uma linha → entender polimorfismo na prática.
**Entrega**: 🎉 os dados sobrevivem ao fechar o app.
**Checkpoint**: por que separar em camadas; o que uma interface "promete"; desafio: exportar relatório para `relatorio.txt`.

## Fase 8 — Maven e testes automatizados
**Conceitos**: por que ferramenta de build; Maven (`pom.xml`, dependências, `src/main/java` vs `src/test/java`, `mvnw`); JUnit 5 (`@Test`, `assertEquals`, `assertThrows`); TDD (ideia).
**Passos**
1. Criar o projeto Maven (pode ser pelo VS Code ou gerando o `pom.xml` com o tutor — boilerplate) e mover o código.
2. `./mvnw compile` / `./mvnw package` — entender o ciclo.
3. Primeiro teste: total de gastos.
4. Teste de exceção: gasto com valor negativo.
5. Escrever um teste **antes** de uma funcionalidade nova (TDD).
**Entrega**: projeto com build e testes passando.
**Checkpoint**: o que o `pom.xml` faz; o que é uma dependência; desafio: 3 testes para o relatório.

## Fase 9 — Banco de dados com JDBC
**Conceitos**: banco relacional e SQL (revisão rápida: `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`); JDBC (`Connection`, `PreparedStatement`, `ResultSet`); SQL injection e por que usar `?`; H2 ou SQLite embutidos (sem instalar servidor).
**Passos**
1. Adicionar a dependência do H2 (ou SQLite) no `pom.xml`; criar a tabela.
2. `GastoRepositoryJdbc` implementando a mesma interface → trocar e tudo continua funcionando.
3. Consultas com filtro (`WHERE`, `ORDER BY`) feitas no banco.
**Entrega**: 🎉 dados em banco de dados de verdade.
**Checkpoint**: por que `PreparedStatement`; como a interface da Fase 7 facilitou essa troca; desafio: total por categoria com `GROUP BY`.

## Fase 10 — API web com Spring Boot
**Conceitos**: HTTP (GET/POST/PUT/DELETE, status, JSON); o que é um framework; Spring Boot (start.spring.io, `@RestController`, `@GetMapping`, `@PostMapping`, `@Service`, injeção de dependência); Spring Data JPA (`@Entity`, `JpaRepository`); testar com navegador/`curl`/Postman.
**Passos**
1. Gerar o projeto em start.spring.io (Web, Data JPA, H2) e rodar o "hello".
2. `GET /gastos` retornando uma lista fixa em JSON.
3. Ligar ao banco com JPA; `POST /gastos` para criar.
4. `PUT`, `DELETE`, validação (`@Valid`) e tratamento de erros (404/400).
5. Reaproveitar a lógica de relatórios num endpoint `GET /relatorios/mensal`.
**Entrega**: 🎉 API REST completa — o mesmo app, agora acessível pela web.
**Checkpoint**: o que a injeção de dependência resolve; o que acontece numa requisição do início ao fim (Raio-X); desafio: endpoint de busca por categoria.

## Depois (opcional, conforme interesse)
- Front-end simples (HTML + `fetch`) consumindo a API
- Docker, deploy, segurança (Spring Security), testes de integração
- Concorrência (threads, virtual threads)
- Git e GitHub de forma mais completa (branches, PRs)

---

## Regras de progressão
- Não pule fases. Dentro de uma fase, passos podem ser agrupados se o aluno estiver indo bem.
- Ao começar uma fase, diga em 2–3 linhas o que o app vai ganhar e quais conceitos vêm aí.
- Ao terminar uma fase: checkpoint → comemorar → sugerir commit (se usar git) → atualizar histórico.
