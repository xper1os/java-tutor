# Tipos de exercício

Sempre **um por vez**. Espere a resposta, dê feedback, e só então passe ao próximo. Uma rodada de prática tem 3–5 itens. Varie os tipos. Use, quando possível, o domínio do projeto do aluno (gastos, jogos...).

## Do mais fácil ao mais difícil

1. **Múltipla escolha** (bom quando o aluno está travando)
   > Qual tipo usar para guardar `19.90`? (a) int (b) double (c) boolean
2. **Prever a saída** — o melhor exercício para "entender o funcionamento"
   > O que este código imprime?
   > ```java
   > int x = 5;
   > x = x + 2;
   > IO.println(x * 2);
   > ```
3. **Completar a lacuna**
   > `for (int i = 0; i ___ lista.size(); i++)`
4. **Achar o bug** (código curto com 1 erro)
   > Por que este código nunca termina? `while (opcao != 0) { IO.println("Menu"); }`
5. **Explicar uma linha** com suas palavras
   > O que `Gasto g = new Gasto("Uber", 25.0);` faz, passo a passo?
6. **Teste de mesa** (tabela com o valor das variáveis a cada volta do loop)
7. **Escrever um método** com assinatura dada
   > Escreva `boolean ehCaro(Gasto g)` que retorna `true` se o valor passar de 100.
8. **Refatorar** (melhorar código que funciona: extrair método, renomear, trocar `for` por stream)
9. **Tarefa do projeto** (passo do roadmap: o aluno implementa no app real)
10. **Desafio aberto** (funcionalidade nova, sem guia; só o objetivo e o critério de pronto)

## Dicas progressivas (quando o aluno trava)
1. Relembre o conceito em 1 linha ("Para repetir até o usuário digitar 0, qual loop vimos?").
2. Mostre um exemplo **parecido** já resolvido (outro contexto, mesma ideia).
3. Dê o esqueleto com lacunas:
   ```java
   while (______) {
       opcao = ______;
   }
   ```
4. Só então, se ele já tentou e pedir, mostre a solução — e peça uma variação para ele fazer sozinho.

## Checkpoint de fase
- 3–4 perguntas (mistura de prever saída, achar bug, explicar) + 1 desafio pequeno no projeto, **sem dicas** no primeiro momento.
- Placar no fim ("3/4 + desafio ✅"). ≥ 75% → avança. Abaixo → 2–3 exercícios de reforço nos pontos que errou, depois refaz a parte que errou.

## Feedback
- Acertou: "✅ Isso!" + elogio específico. Se foi fácil demais, aumente um pouco no próximo.
- Errou: explique a causa (não só a resposta certa) e proponha um item **parecido** para ele tentar de novo.
- Fim da rodada: placar + 1 linha sobre o que melhorar.
