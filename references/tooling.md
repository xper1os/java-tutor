# Ferramentas e ambiente

Ambiente do aluno (verificado em 2026-10-10): **Windows 11**, **JDK 25** (`java`/`javac` no PATH), **VS Code** instalado, **git** instalado, **Maven não instalado** (use o Maven Wrapper `mvnw`, que não exige instalação). Confirme de novo se algo falhar.

## Editor
- **VS Code** + extensão **"Extension Pack for Java"** (Microsoft): realce, autocompletar, botão ▶ Run, debugger. Abrir a pasta do projeto: `code .`
- Alternativa: **IntelliJ IDEA Community** (mais completo para Java, mais pesado).
- Nas Fases 0–2, incentive rodar pelo **terminal** (para entender o que acontece); o botão ▶ vem depois.
- Debugger (a partir da Fase 2): breakpoint, step over/into, ver variáveis — ótimo complemento ao modo Raio-X.

## Comandos essenciais

| Objetivo | Comando |
|---|---|
| Ver versão | `java -version` / `javac -version` |
| Rodar um arquivo direto (estudo) | `java Main.java` |
| Rodar com vários arquivos na mesma pasta | `java Main.java` (o launcher encontra as outras classes na pasta) |
| Compilar e rodar ("de verdade") | `javac Main.java` → `java Main` |
| Vários arquivos / pacotes | `javac -d out (Get-ChildItem -Recurse -Filter *.java).FullName` → `java -cp out br.com.app.Main` (PowerShell) |
| Maven (Fase 8+), PowerShell | `.\mvnw.cmd compile`, `.\mvnw.cmd test`, `.\mvnw.cmd package` |
| Spring Boot (Fase 10) | `.\mvnw.cmd spring-boot:run` |
| Testar API | navegador para GET; `curl.exe -X POST http://localhost:8080/gastos -H "Content-Type: application/json" -d '{\"descricao\":\"Uber\",\"valor\":25}'` |

No Claude Code, o aluno pode rodar um comando com `!` na frente (ex.: `! java Main.java`) para a saída aparecer na conversa. Programas que leem do teclado (`IO.readln`/`Scanner`) funcionam melhor no terminal do VS Code.

## Java 25: formas de escrever o `main`
```java
// Arquivo compacto (Java 25) — ótimo para começar
void main() {
    String nome = IO.readln("Seu nome: ");
    IO.println("Olá, " + nome + "!");
}
```
```java
// Forma clássica — a que você verá em quase todo lugar
public class Main {
    public static void main(String[] args) {
        System.out.println("Olá!");
    }
}
```
`IO.readln(prompt)` lê uma linha do teclado. Mais adiante, apresente `Scanner` (muito usado em tutoriais): `Scanner sc = new Scanner(System.in); String linha = sc.nextLine();` — prefira `nextLine()` + conversão a `nextInt()` (evita o bug clássico da quebra de linha sobrando).

## Acentos no terminal do Windows
Se aparecer `Ol�` ou `OlÃ¡`: no PowerShell, `[Console]::OutputEncoding = [Text.Encoding]::UTF8` antes de rodar; se persistir, `java -Dstdout.encoding=UTF-8 Main.java`. Para não repetir, pode ir no perfil do PowerShell (`notepad $PROFILE`).

## Pasta do projeto
Sugira fora do OneDrive (ex.: `C:\Users\<usuario>\projetos-java\<nome>`) — a sincronização disputa arquivos gerados (`.class`, `target/`) e pode travar builds.

## Git (opcional, recomendado a partir da Fase 1)
- `git init` uma vez; ao fim de cada passo/fase: `git add .` + `git commit -m "Fase 2: menu em loop com métodos"`.
- `.gitignore` com `*.class`, `out/`, `target/`, `.idea/`, `.vscode/`.
- Ensine como "máquina do tempo": dá para voltar se algo quebrar. Não aprofunde (branches etc.) antes da hora.

## Gerar projeto Maven (Fase 8)
Opções, da mais didática para a mais rápida:
1. VS Code: Ctrl+Shift+P → "Java: Create Java Project" → Maven → `maven-archetype-quickstart`.
2. start.spring.io sem dependências (já vem com `mvnw`).
3. O tutor escreve o `pom.xml` mínimo (boilerplate) e explica cada bloco; gerar o wrapper exige Maven instalado, então prefira 1 ou 2.

`pom.xml` deve usar `<maven.compiler.release>25</maven.compiler.release>` e JUnit Jupiter (versão 5.x estável).
