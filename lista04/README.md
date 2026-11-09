# Lista 04 — CSS: Flexbox (parte 2)

## 4. Tamanho de partida e atalho `flex`

**13. O que é o `flex-basis`? Se um item tem `width: 200px` e `flex-basis: 10rem`, qual medida vale como tamanho de partida?**

O `flex-basis` define o tamanho inicial do item no eixo principal. Nesse caso, vale o `flex-basis: 10rem`, pois ele tem prioridade sobre o `width` no cálculo do Flexbox.

**14. Por que usar `flex-basis: 0` faz o `flex-grow` repartir a faixa inteira, e não só a sobra?**

Porque os itens começam com tamanho zero. Assim, todo o espaço disponível na faixa fica como sobra para ser distribuída pelo `flex-grow`.

**15. Preencha a tabela com os valores equivalentes de cada atalho (crescimento, encolhimento e base):**

| Atalho | grow | shrink | basis |
|---|---:|---:|---|
| `flex: initial` | 0 | 1 | auto |
| `flex: 1` | 1 | 1 | 0% |
| `flex: auto` | 1 | 1 | auto |
| `flex: none` | 0 | 0 | auto |

**16. Dois itens, de conteúdo 100px e 300px, numa faixa de 600px. Calcule a largura final de cada um com `flex: 1` e depois com `flex: auto`. Por que os resultados diferem?**

- **Com `flex: 1`:** os dois itens começam com base zero. Como têm o mesmo peso de crescimento, dividem os 600px igualmente: **300px para cada um**.
- **Com `flex: auto`:** as bases são 100px e 300px. A soma é 400px, então sobram 200px. Cada item recebe mais 100px: o primeiro fica com **200px** e o segundo com **400px**.

Os resultados diferem porque `flex: 1` usa base zero, enquanto `flex: auto` usa o tamanho do conteúdo como base.

**17. Verdadeiro ou falso? Justifique. “`flex: 1` e `flex: auto` sempre dão o mesmo resultado quando os itens têm o mesmo conteúdo.”**

Verdadeiro, considerando itens com o mesmo conteúdo e as mesmas condições. Como as bases automáticas são iguais e os pesos de crescimento também, os dois atalhos acabam distribuindo o espaço igualmente entre eles.

## 5. O mínimo que trava o encolhimento

**18. Um item tem `flex-shrink: 1` e mesmo assim estoura a faixa por causa de uma palavra muito longa. Qual propriedade padrão está segurando o item e qual ajuste a solta?**

A propriedade é `min-width: auto`, que é o valor padrão dos itens flex e pode impedir que eles fiquem menores que o conteúdo. O ajuste é colocar `min-width: 0` no item.

**19. Em que situação você esperaria ver esse problema ao montar um miolo com menu e texto?**

Quando o texto tiver uma palavra, um link ou uma linha de código muito longa e não puder quebrar. Isso pode fazer a área do texto ultrapassar o espaço disponível e empurrar o menu.

## 6. `order` e `align-self`

**20. Observe o trecho e responda.**

```html
<div class="barra">
  <span>A</span>
  <span>B</span>
  <span class="primeiro">C</span>
</div>
```

```css
.barra {
  display: flex;
}

.primeiro {
  order: -1;
}
```

**a)** A ordem na tela será **C, A, B**, porque o item C recebeu `order: -1`.

**b)** A ordem de foco ao apertar Tab continuará sendo **A, B, C**, seguindo a ordem dos elementos no HTML.

**c)** Isso importa porque leitores de tela normalmente seguem a ordem do HTML. Se a ordem visual for diferente, a leitura pode ficar confusa para quem usa tecnologias assistivas.

**21. Qual é o valor padrão de `order`? Entre `order: -1` e `order: 2`, quem aparece primeiro?**

O valor padrão é `0`. O item com `order: -1` aparece primeiro, porque tem o menor valor.

**22. O pai tem `align-items: stretch`. O que acontece com um filho com `align-self: flex-end`? E com `align-self: auto`?**

Com `align-self: flex-end`, o filho fica alinhado ao final do eixo transversal e deixa de esticar. Com `align-self: auto`, ele usa o valor de `align-items` do pai; nesse caso, continua com `stretch`.

**23. Quando usar `align-self` e quando usar `align-items`?**

Uso `align-items` para alinhar todos os itens do contêiner de uma vez. Uso `align-self` quando quero mudar o alinhamento de apenas um item.

## 7. A página com miolo

**24. Nesta estrutura, quais elementos são itens de `.pagina` e quais são itens de `.miolo`?**

- Itens de `.pagina`: `header`, `.miolo` e `footer`.
- Itens de `.miolo`: `aside` e `main`.

**25. Por que `.miolo` precisa ter `display: flex` além de ser item de `.pagina`?**

Porque ser item de `.pagina` controla o tamanho e a posição do próprio `.miolo`, mas não organiza seus elementos internos. O `display: flex` faz o `aside` e o `main` ficarem lado a lado.

**26. Explique a função de cada declaração:**

```css
.pagina {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.miolo {
  display: flex;
  flex: 1;
}

aside {
  flex: 0 0 10rem;
}

main {
  flex: 1;
  min-width: 0;
}
```

- `.pagina`: transforma a página em um contêiner flexível, organiza os elementos em coluna e garante pelo menos a altura da tela.
- `.miolo`: também vira um contêiner flexível e cresce para ocupar o espaço livre entre o topo e o rodapé.
- `aside`: fica com base de `10rem`, sem crescer nem encolher.
- `main`: cresce para ocupar o espaço restante. O `min-width: 0` permite que ele encolha quando necessário, evitando que o conteúdo ultrapasse a faixa.

## 8. Erros comuns e síntese

**27. Um colega escreveu `flex-grow: 1` no contêiner e diz que não funciona. Qual é o erro e qual a correção?**

O erro é colocar `flex-grow` no contêiner. Essa propriedade deve ser colocada nos itens que estão dentro dele. A correção é usar `display: flex` no pai e `flex-grow: 1` no filho que deve crescer.

**28. Cite duas formas de resolver um item que estoura a faixa e explique quando cada uma é indicada.**

1. Usar `min-width: 0` no item flex, quando ele precisa poder encolher para caber no espaço disponível.
2. Usar `overflow-wrap: anywhere` no texto, quando uma palavra ou um link muito longo precisa quebrar linha para não ultrapassar o contêiner.

**29. Monte um resumo de uma frase para cada propriedade: `flex-basis`, `flex-grow`, `flex-shrink`, `order` e `align-self`.**

- `flex-basis`: define o tamanho inicial do item no eixo principal.
- `flex-grow`: define quanto o item pode crescer para ocupar o espaço que sobra.
- `flex-shrink`: define quanto o item pode encolher quando falta espaço.
- `order`: altera a ordem visual dos itens flex na tela.
- `align-self`: define o alinhamento de um item individual no eixo transversal.
