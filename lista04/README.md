1-O(s) conteiner(s) é(são) o{s} elemento "pai" e o(s) itens são os elementos filhos dele (na fila). O "display: flex" é colocado no contêiner(s).

2- eixo horizontal.

3- É o espaço que fica livre depois de colocar os itens. Quem distribui essa sobra é o flex-grow: [algo]

4- o valor padrão de flex-grow é 0, o que significa que o item não cresce pra poder ocupar o espaço sobrando.

5- A mesa é o conteiner, os pratos são o tamanho inicial do item, a sobra representa o espaço livre na mesa e o peso do flex-grow define quanto cada item recebe desse espaço

6- A declaração é "flex-grow: 1"; e vai no elemento da marca

7- 2+3+1=6 |> 600/6 = 100 |>
|> Primeiro peso: 100*2=200px |>
|> Segundo peso: 100*3=300px |>
|> Terceiro peso: 100*1=100px

8- 100 + 100 + 100 = 300px |> 600 - 300 = 300px |>
0 + 1 + 2 = 3 |> 300 / 3 = 100px |>
|> Primeiro peso: 100px |>
|> Segundo peso: 100+100 = 200px |>
|> Terceiro peso: 100+200 = 300px
Tamanhos finais:

9- quando falta espaço. O valor padrão é 1

10- falta 200. (600 pra 800 = |200|)
Como os dois itens têm o mesmo tamanho e flex-shrink: 1, cada um perde 100px.
2x + 200 = 800 |> 2x = 800 - 200 |> 2x = 600
|>  600/2 = x |> x = 300px

11- (O primeiro item não encolhe porque tem "flex-shrink: 0" então continua com 400px) |> 
Primeiro item: 400px |>
|> Segundo item: 400 - 200 = 200px
Sim, cabe.

12- um ícone ao lado de um texto. Ele pode ter o flex-shrink: 0 para não ficar achatado quando faltar espaço no conteiner, deixando o texto diminuir para caber.