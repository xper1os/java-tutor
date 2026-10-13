# Ideias de projeto

Na primeira sessão, apresente 3–4 opções em poucas linhas e deixe o aluno escolher (ou propor a dele). Todas seguem o mesmo `roadmap.md`; só mudam as entidades e as funcionalidades de exemplo.

| Projeto | Entidade principal | Enum (Fase 3) | Map/relatório (Fases 4 e 6) | Endpoint final (Fase 10) |
|---|---|---|---|---|
| 💰 **Controle de Gastos** (padrão) | `Gasto` (descrição, valor, data, categoria) | `Categoria` | total por categoria, gasto por mês, maior gasto | `GET /gastos`, `GET /relatorios/mensal` |
| 🎮 **Catálogo de Jogos/Filmes/Séries** | `Titulo` (nome, ano, plataforma/gênero, nota, status) | `Status` (QUERO_JOGAR, JOGANDO, ZERADO) / `Genero` | média de notas por gênero, quantos zerados | `GET /titulos?status=JOGANDO` |
| ✅ **Lista de Tarefas** | `Tarefa` (título, prazo, prioridade, concluída) | `Prioridade` | tarefas atrasadas, por prioridade | `PATCH /tarefas/{id}/concluir` |
| 📚 **Biblioteca Pessoal** | `Livro` (título, autor, páginas, lido) + `Emprestimo` | `Genero` | páginas lidas no ano, livros por autor | `POST /emprestimos` |
| 🏋️ **Registro de Treinos** | `Treino` (data, exercício, séries, carga) | `GrupoMuscular` | evolução de carga, treinos por semana | `GET /treinos/evolucao` |
| 🧑‍💼 **Cadastro de Clientes/Pedidos** (mais "corporativo") | `Cliente`, `Pedido`, `ItemPedido` | `StatusPedido` | faturamento por cliente/mês | `GET /clientes/{id}/pedidos` |

## Como escolher
- Prefira um tema que o aluno **usaria de verdade** — motivação vale mais que o tema "perfeito".
- Projetos com **2 entidades relacionadas** (Biblioteca, Clientes/Pedidos) são ótimos para a Fase 9–10 (relacionamentos), mas comece só com a entidade principal; a segunda entra na Fase 7 ou 9.
- Se o aluno trabalha com sistemas corporativos/bancos de dados (ex.: SQL), o **Clientes/Pedidos** conecta bem com o dia a dia dele.

## Nome e pasta
Combine um nome curto em minúsculas com hífen (`controle-gastos`). Sugira uma pasta **fora do OneDrive** (ex.: `C:\Users\<usuario>\projetos-java\controle-gastos`) — a sincronização pode atrapalhar arquivos gerados (`.class`, `target/`). Registre o caminho no histórico.
