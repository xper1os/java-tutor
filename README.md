# java-tutor — Skill para Claude Code

Professor particular de Java para iniciantes brasileiros. Você aprende **construindo um app do zero**: começa com um programa de console e termina com uma API web com banco de dados. Cada conceito novo é explicado em português e entra no projeto na hora em que ele precisa.

## Instalação

Pré-requisitos: [Claude Code](https://claude.com/claude-code) e [git](https://git-scm.com/).

```bash
git clone https://github.com/xper1os/java-tutor ~/.claude/skills/java-tutor
```

Depois abra o Claude Code na pasta onde quer criar seu projeto e digite `/java-tutor` (ou "vamos programar"). Na primeira sessão o tutor faz algumas perguntas, ajuda a escolher o app e configura o ambiente (JDK, editor).

Para atualizar a skill:

```bash
git -C ~/.claude/skills/java-tutor pull
```

Seu histórico fica em `progress/learner-profile.md`, criado automaticamente a partir do modelo `progress/learner-profile.template.md`. Ele é pessoal e está no `.gitignore`, então não vai para o repositório e não é apagado ao atualizar.

## Estrutura
```
java-tutor/
├── SKILL.md                    # Comportamento, regras, modos
├── README.md                   # Este arquivo
├── references/
│   ├── roadmap.md              # Fases 0–10 do projeto (passos, entregas, checkpoints)
│   ├── project-ideas.md        # Opções de app (gastos, jogos, tarefas, pedidos...)
│   ├── concepts.md             # Conceitos com analogias + Raio-X (stack/heap)
│   ├── common-errors.md        # Erros do javac/java traduzidos
│   ├── exercise-types.md       # Tipos de exercício e dicas progressivas
│   └── tooling.md              # JDK 25, VS Code, terminal, Maven, git, Windows
├── progress/
│   ├── learner-profile.template.md  # Modelo em branco do histórico
│   └── learner-profile.md           # Seu histórico (criado na 1ª sessão, fora do git)
└── examples/
    └── sessions.md             # Exemplos de interações
```

## Trilha
| Fase | O app ganha... | Você aprende |
|---|---|---|
| 0 | primeiro programa | JDK, JVM, compilar e executar |
| 1 | menu que responde | variáveis, tipos, entrada, if/switch |
| 2 | menu em loop | loops, métodos, escopo |
| 3 | gastos como objetos | classes, objetos, encapsulamento, record, enum, stack/heap |
| 4 | CRUD em memória | arrays, List, Map |
| 5 | não quebra com entrada errada | exceções |
| 6 | relatórios | lambdas e streams |
| 7 | salva em arquivo | pacotes, camadas, interfaces, arquivos |
| 8 | build e testes | Maven, JUnit |
| 9 | banco de dados | SQL, JDBC |
| 10 | API web | HTTP, Spring Boot, JPA |

## Como usar
| Gatilho | O que acontece |
|---|---|
| `vamos programar` / `/java-tutor` | Retoma o projeto onde parou (com revisão rápida) |
| `próximo passo` | Próximo conceito + tarefa |
| colar código / `revisa meu código` | Revisão com dicas (sem dar a resposta pronta) |
| colar erro / `deu erro` | Tradução do erro + como achar a causa |
| `explica interfaces` | Conceito com analogia e exemplo |
| `raio-x` | Mostra linha a linha o que acontece na memória |
| `desafio` / `exercício` | Prática avulsa |
| `faz pra mim` | Demonstração explicada + uma variação para você fazer |
| `revisão` | Revisa o que você errou/aprendeu antes |
| `meu progresso` | Resumo: fase, o que já sabe, o que o app faz |
| `mais devagar` / `mais rápido` | Ajusta o tamanho dos passos |
| `chega por hoje` | Resumo e salva o progresso |

## Dicas
- Rode o código você mesmo no terminal do VS Code. No Claude Code, `! java Main.java` mostra a saída na conversa.
- Erros de compilação fazem parte do aprendizado: cole a mensagem inteira.
- Sessões curtas e frequentes rendem mais. Faça commit no git ao fim de cada fase.
- Para reiniciar do zero, apague `progress/learner-profile.md`: na próxima sessão ele é recriado a partir do modelo.

## Licença

[MIT](LICENSE)
