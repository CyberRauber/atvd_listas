# Lista 04 — Flexbox (parte 2)

## 4. Tamanho inicial e atalho `flex`

**13. O que é o `flex-basis`? Se um item tem `width: 200px` e `flex-basis: 10rem`, qual medida vale como tamanho de partida?**

O `flex-basis` define o tamanho inicial do item no eixo principal. Nesse exemplo, vale o `flex-basis: 10rem`, que é usado pelo Flexbox no lugar do `width`.

**14. Por que usar `flex-basis: 0` faz o `flex-grow` repartir a faixa inteira, e não só a sobra?**

Porque os itens começam com tamanho zero. Assim, o espaço disponível fica para ser dividido pelo `flex-grow`.

**15. Preencha a tabela com os valores equivalentes de cada atalho (crescimento, encolhimento e base):**

| Atalho | grow | shrink | basis |
|---|---:|---:|---|
| `flex: initial` | 0 | 1 | auto |
| `flex: 1` | 1 | 1 | 0% |
| `flex: auto` | 1 | 1 | auto |
| `flex: none` | 0 | 0 | auto |

**16. Dois itens, de conteúdo 100px e 300px, numa faixa de 600px. Calcule a largura final de cada um com `flex: 1` e depois com `flex: auto`. Por que os resultados diferem?**

- Com `flex: 1`, os dois começam com base zero e dividem os 600px igualmente: **300px para cada um**.
- Com `flex: auto`, as bases são 100px e 300px. Sobram 200px, que são divididos entre os dois. No final, ficam **200px e 400px**.

A diferença é que `flex: 1` começa do zero, enquanto `flex: auto` considera o tamanho do conteúdo como base.

**17. Verdadeiro ou falso? Justifique. “`flex: 1` e `flex: auto` sempre dão o mesmo resultado quando os itens têm o mesmo conteúdo.”**

Verdadeiro, considerando que os itens tenham o mesmo conteúdo e as mesmas condições. Nesse caso, as bases ficam iguais e os dois atalhos distribuem o espaço da mesma forma.

## 5. O mínimo que impede o encolhimento

**18. Um item tem `flex-shrink: 1` e mesmo assim estoura a faixa por causa de uma palavra muito longa. Qual propriedade padrão está segurando o item e qual ajuste a solta?**

É o `min-width: auto`, que pode impedir o item de ficar menor que o conteúdo. Para resolver, basta usar `min-width: 0`.

**19. Em que situação você esperaria ver esse problema ao montar um miolo com menu e texto?**

Quando o texto tiver uma palavra, um link ou uma linha de código muito longa que não consiga quebrar. Isso pode fazer o conteúdo passar do espaço disponível e empurrar o menu.

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

**a)** Na tela, a ordem será **C, A, B**, porque o item C recebeu `order: -1`.

**b)** A ordem do foco ao apertar Tab continua sendo **A, B, C**, pois segue a ordem dos elementos no HTML.

**c)** Isso é importante para a acessibilidade, porque leitores de tela normalmente seguem a ordem do HTML. Se a ordem visual for diferente, a leitura pode ficar confusa.

**21. Qual é o valor padrão de `order`? Entre `order: -1` e `order: 2`, quem aparece primeiro?**

O valor padrão é `0`. O item com `order: -1` aparece primeiro, pois tem o menor valor.

**22. O pai tem `align-items: stretch`. O que acontece com um filho com `align-self: flex-end`? E com `align-self: auto`?**

Com `align-self: flex-end`, o filho fica no final do eixo transversal e não estica. Com `align-self: auto`, ele segue o `align-items` do pai e continua com `stretch`.

**23. Quando usar `align-self` e quando usar `align-items`?**

Uso `align-items` para alinhar todos os itens de uma vez. Já o `align-self` serve para mudar o alinhamento de apenas um item.

## 7. A página com miolo

**24. Nesta estrutura, quais elementos são itens de `.pagina` e quais são itens de `.miolo`?**

- Itens de `.pagina`: `header`, `.miolo` e `footer`.
- Itens de `.miolo`: `aside` e `main`.

**25. Por que `.miolo` precisa ter `display: flex` além de ser item de `.pagina`?**

Porque ser item de `.pagina` organiza o próprio `.miolo`, mas não os elementos que estão dentro dele. O `display: flex` organiza o `aside` e o `main lado a lado.

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

- `.pagina`: organiza os elementos em coluna e ocupa pelo menos a altura da tela.
- `.miolo`: organiza seus elementos com Flexbox e cresce para ocupar o espaço livre.
- `aside`: mantém a base de 10rem, sem crescer nem encolher.
- `main`: ocupa o espaço que sobra. O `min-width: 0` permite que ele encolha quando precisar.

## 8. Erros comuns e resumo

**27. Um colega escreveu `flex-grow: 1` no contêiner e diz que não funciona. Qual é o erro e qual a correção?**

O erro é colocar `flex-grow` no contêiner. Essa propriedade deve ficar no item que precisa crescer. No pai, uso `display: flex`; no filho, `flex-grow: 1`.

**28. Cite duas formas de resolver um item que estoura a faixa e explique quando cada uma é indicada.**

1. Usar `min-width: 0` no item flex, para permitir que ele encolha.
2. Usar `overflow-wrap: anywhere` no texto, quando uma palavra ou um link muito longo precisa quebrar linha.

**29. Monte um resumo de uma frase para cada propriedade: `flex-basis`, `flex-grow`, `flex-shrink`, `order` e `align-self`.**

- `flex-basis`: define o tamanho inicial do item.
- `flex-grow`: define quanto o item pode crescer.
- `flex-shrink`: define quanto o item pode encolher.
- `order`: muda a ordem visual dos itens.
- `align-self`: muda o alinhamento de um item específico.
