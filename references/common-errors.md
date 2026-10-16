# Erros comuns: como traduzir

Ensine o aluno a ler um erro em 3 passos:
1. **Onde**: `Main.java:12` → arquivo e **linha**. O `^` mostra a coluna.
2. **O quê**: a primeira frase depois de `error:` (compilação) ou o nome da exceção (execução).
3. **Stack trace** (execução): procure a primeira linha `at ...` que cita um arquivo **dele** — as linhas `java.base/...` são internas do Java.

Importante: o compilador às vezes acusa a linha **seguinte** à do erro real (ex.: `;` faltando na linha anterior). E corrija **o primeiro erro primeiro** — um erro pode gerar vários em cascata.

## Erros de compilação (`javac`)

| Mensagem | Tradução | Causa típica |
|---|---|---|
| `';' expected` | faltou ponto e vírgula | fim de instrução sem `;` (olhe a linha anterior também) |
| `cannot find symbol` | "não conheço esse nome" | erro de digitação, variável fora do escopo, falta `import`, maiúscula/minúscula (`string` vs `String`) |
| `incompatible types: X cannot be converted to Y` | tipos não combinam | `int x = "5";`, método retornando tipo errado, `double` em `int` sem conversão, `int x = null;` (`<null> cannot be converted to int` — primitivo não aceita `null`; use `Integer` se precisar de "sem valor") |
| `possible lossy conversion from double to int` | vai perder casas decimais | `int total = 10.5;` → use `double` ou converta com `(int)` conscientemente |
| `missing return statement` | o método promete devolver algo e algum caminho não devolve | `return` só dentro do `if`, sem `else` |
| `non-static method X cannot be referenced from a static context` | o `main` (static) tentou usar algo de objeto | chamar método de instância direto no `main` → tornar `static` ou criar um objeto |
| `variable X might not have been initialized` | variável usada antes de receber valor | declarar sem atribuir e usar num caminho do `if` |
| `variable X is already defined` | nome repetido no mesmo escopo | declarar `int x` duas vezes |
| `reached end of file while parsing` | faltou fechar `}` | chaves desbalanceadas |
| `class X is public, should be declared in a file named X.java` | nome do arquivo ≠ nome da classe | renomear arquivo ou classe |
| `unreported exception X; must be caught or declared to be thrown` | exceção *checked* não tratada | `Files.readAllLines` sem `try/catch` ou `throws IOException` |
| `'else' without 'if'` | `else` solto | `;` depois do `if (...)` ou chaves erradas |
| `unclosed string literal` | aspas não fechadas | `"Olá` |
| `bad operand types for binary operator` | operação sem sentido entre tipos | `"a" - 1`, `&&` com números |
| `tostring() in X does not override or implement a method from a supertype` | o `@Override` não achou esse método na classe mãe | nome digitado errado (`tostring`, `ToString`) ou parâmetros diferentes. **Sem** `@Override` o mesmo erro compila calado e o método nunca é chamado |
| `toString() in X cannot override toString() in Object` + `attempting to assign weaker access privileges; was public` | sobrescreveu reduzindo o acesso | faltou `public` no `toString()` (quem sobrescreve não pode restringir o acesso herdado) |
| `X is not abstract and does not override abstract method Y` | a classe não cumpriu o contrato da interface | faltou implementar um método da interface |

## Erros de execução (exceções)

| Exceção | Tradução | Causa típica |
|---|---|---|
| `NumberFormatException: For input string: "abc"` | texto não é número | `Integer.parseInt` com entrada do usuário inválida (ou vazia: `""`) |
| `NullPointerException` | usou um objeto que não existe (`null`) | atributo/lista não inicializado (`List<Gasto> gastos;` sem `= new ArrayList<>()`), método retornou `null`. O Java mostra **qual** variável era null — leia a mensagem |
| `ArrayIndexOutOfBoundsException` / `IndexOutOfBoundsException: Index 3 out of bounds for length 3` | posição não existe | índices vão de 0 a tamanho-1; usuário digitou 3 querendo o 3º item |
| `InputMismatchException` | `Scanner.nextInt()` recebeu texto | entrada errada; prefira ler a linha inteira e converter |
| `ArithmeticException: / by zero` | divisão inteira por zero | média de lista vazia |
| `ConcurrentModificationException` | lista alterada enquanto era percorrida | `remove` dentro de for-each → use `removeIf` ou `Iterator` |
| `ClassCastException` | conversão de tipo impossível | cast forçado errado |
| `StackOverflowError` | pilha de chamadas estourou | recursão sem fim (método chamando a si mesmo, ou `toString` chamando `toString`, ex.: `return "Tarefa: " + this;` dentro do próprio `toString`) |
| `NoSuchFileException` | arquivo não encontrado | caminho relativo errado — o caminho é relativo à pasta **de onde** o `java` foi executado |
| `IllegalArgumentException` | argumento inválido | geralmente lançado de propósito pela validação dele (bom sinal!) |

## Problemas do ambiente

| Sintoma | Causa | Solução |
|---|---|---|
| Acentos viram `Ã©` ou `�` no terminal | codificação do console do Windows | No PowerShell: `[Console]::OutputEncoding = [Text.Encoding]::UTF8` (ou `chcp 65001`) antes de rodar; se persistir, `java -Dstdout.encoding=UTF-8 Main.java`. Salvar o `.java` em UTF-8 (padrão do VS Code) |
| `'java' não é reconhecido...` | JDK fora do PATH | ver `tooling.md` |
| `error: can't find main(String[]) method in class` | `main` com assinatura errada | conferir `public static void main(String[] args)` ou `void main()` |
| `Could not find or load main class Main` | rodou `java Main` na pasta errada / sem compilar / pacote | estar na pasta do `.class`; com pacotes, `java -cp out pacote.Main` |
| Mudança no código não aparece | rodou o `.class` antigo | recompilar (`javac`) ou usar `java Main.java` |
| `./mvnw` não roda no PowerShell | sintaxe Windows | usar `.\mvnw.cmd compile` |

## Como agir (modo Debug)
1. Use o formato de erro do SKILL.md.
2. Se não tiver o código, peça **só as linhas próximas** (ou leia o arquivo do projeto).
3. Dê uma dica, não a correção. Ex.: "A linha 14 usa `gastos`, mas onde ela recebeu um valor? Procure onde você declarou a lista."
4. Depois de corrigir, pergunte "por que deu esse erro?" para fixar.
5. Registre o tipo de erro no histórico; se repetir, entra na fila de revisão.
