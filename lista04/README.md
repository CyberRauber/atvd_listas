Lista 04 - Flexbox (parte 2)

13. O que é o flex-basis? Se um item tem width: 200px e flex-basis: 10rem, qual medida vale como tamanho de partida?

O flex-basis define o tamanho inicial. Nesse caso, vale 10rem.

14. Por que usar flex-basis: 0 faz o flex-grow repartir a faixa inteira, e não só a sobra?

Porque os itens começam com tamanho zero, então o flex-grow divide todo o espaço entre eles.

15. Preencha a tabela com os valores equivalentes de cada atalho:

flex: initial = grow 0, shrink 1, basis auto
flex: 1 = grow 1, shrink 1, basis 0%
flex: auto = grow 1, shrink 1, basis auto
flex: none = grow 0, shrink 0, basis auto

16. Dois itens, de conteúdo 100px e 300px, numa faixa de 600px. Calcule a largura final de cada um com flex: 1 e depois com flex: auto. Por que os resultados diferem?

Com flex: 1, os dois dividem os 600px igualmente, ficando com 300px cada.

Com flex: auto, eles começam com 100px e 300px. Sobram 200px, que são divididos igualmente. No final ficam 200px e 400px.

A diferença é que flex: 1 começa do zero, enquanto flex: auto considera o tamanho do conteúdo.

17. Verdadeiro ou falso? “flex: 1 e flex: auto sempre dão o mesmo resultado quando os itens têm o mesmo conteúdo.”

Verdadeiro. Se os itens têm o mesmo conteúdo e as mesmas condições, acabam dividindo o espaço igualmente.

18. Um item tem flex-shrink: 1 e mesmo assim estoura a faixa por causa de uma palavra muito longa. Qual propriedade padrão está segurando o item e qual ajuste a solta?

É o min-width: auto, que impede o item de ficar menor que o conteúdo. Para resolver, uso min-width: 0.

19. Em que situação você esperaria ver esse problema ao montar um miolo com menu e texto?

Quando tem uma palavra ou link muito grande que não quebra linha e acaba empurrando o menu.

20. Observe o trecho e responda.

HTML:

    <div class="barra">
      <span>A</span>
      <span>B</span>
      <span class="primeiro">C</span>
    </div>

CSS:

    .barra {
      display: flex;
    }

    .primeiro {
      order: -1;
    }

a) Na tela, a ordem será C, A, B, porque o item C recebeu order: -1.

b) Os span não recebem foco pelo Tab normalmente. Se fossem focáveis, a ordem do Tab continuaria A, B, C, seguindo o HTML.

c) Isso importa porque o leitor de tela segue a ordem do HTML. Se ela ficar diferente da ordem visual, pode confundir.

21. Qual é o valor padrão de order? Entre order: -1 e order: 2, quem aparece primeiro?

O valor padrão é 0. O item com order: -1 aparece primeiro, porque tem o menor valor.

22. O pai tem align-items: stretch. O que acontece com um filho com align-self: flex-end? E com align-self: auto?

Com flex-end, o filho fica no final e não estica. Com auto, segue o alinhamento do pai, então continua com stretch.

23. Quando usar align-self e quando usar align-items?

Uso align-items para alinhar todos os itens e align-self para mudar o alinhamento de apenas um.

24. Nesta estrutura, quais elementos são itens de .pagina e quais são itens de .miolo?

De .pagina: header, .miolo e footer.
De .miolo: aside e main.

25. Por que .miolo precisa ter display: flex além de ser item de .pagina?

Porque o display: flex organiza os elementos que estão dentro dele, o aside e o main.

26. Explique a função de cada declaração:

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

.pagina organiza os elementos em coluna e ocupa pelo menos a altura da tela.
.miolo coloca o menu e o texto lado a lado e ocupa o espaço livre.
aside fica com tamanho fixo de 10rem.
main ocupa o espaço que sobra e pode encolher quando precisar.

27. Um colega escreveu flex-grow: 1 no contêiner e diz que não funciona. Qual é o erro e qual a correção?

O flex-grow foi colocado no contêiner, mas deve ser usado no item que precisa crescer. No pai uso display: flex e no filho flex-grow: 1.

28. Cite duas formas de resolver um item que estoura a faixa e explique quando cada uma é indicada.

Uso min-width: 0 para permitir que o item encolha.
Uso overflow-wrap: anywhere para quebrar palavras ou links muito grandes.

29. Monte um resumo de uma frase para cada propriedade: flex-basis, flex-grow, flex-shrink, order e align-self.

flex-basis: define o tamanho inicial.
flex-grow: define quanto o item pode crescer.
flex-shrink: define quanto o item pode encolher.
order: muda a ordem visual.
align-self: muda o alinhamento de um item específico.
