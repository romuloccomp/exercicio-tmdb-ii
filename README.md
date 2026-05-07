# Trabalho Prático - Filmes em Cartaz II

**Disciplina:** Desenvolvimento em JavaScript  
**Professor:** Romulo Pereira  
**Tema:** Imagens, gêneros e filtro no front-end

## Continuação do exercício anterior

Este trabalho é a continuação do exercício anterior, disponível no repositório:

[https://github.com/romuloccomp/exercicio-tmdb-i](https://github.com/romuloccomp/exercicio-tmdb-i)

Na primeira parte, o objetivo foi iniciar o consumo da API do **The Movie Database — TMDB** e buscar os filmes em cartaz. Agora, nesta segunda parte, a aplicação deverá evoluir para mostrar mais informações ao usuário e permitir uma pesquisa simples na lista de filmes.

## Contexto

O(a) namorado(a), esposo(a) ou aquele crush especial convidou você para ir ao cinema, mas comentou que ficou confuso diante de tantas opções disponíveis.

Então, cheio(a) de entusiasmo e iniciativa, você responde com confiança:

> "Deixa comigo! Vou criar um sistema simples e organizado para facilitar essa escolha."

Agora que a aplicação já consegue buscar os filmes em cartaz, chegou o momento de melhorar a experiência da pessoa que vai escolher o filme.

## Desafio

Nesta segunda parte do trabalho, você deverá complementar a aplicação para exibir a **imagem do pôster**, mostrar os **gêneros dos filmes** e criar um **campo de filtro**.

O filtro deverá permitir que o usuário pesquise pelo **nome do filme** ou por alguma palavra presente na **descrição**. Essa filtragem deverá acontecer diretamente no front-end, usando a lista de filmes que já foi carregada da API.

## O que deve ser feito

| Etapa | Descrição |
|---|---|
| 1 | Exibir a imagem do pôster de cada filme. |
| 2 | Buscar a lista de gêneros dos filmes na API do TMDB. |
| 3 | Relacionar os IDs dos gêneros com seus respectivos nomes. |
| 4 | Mostrar os gêneros junto com cada filme. |
| 5 | Criar ou utilizar um campo de pesquisa na página. |
| 6 | Filtrar os filmes pelo título ou pela descrição. |
| 7 | Atualizar a lista na tela sem recarregar a página. |

## Imagem do pôster

A API do TMDB retorna o campo `poster_path`, que representa o caminho da imagem do filme. Para exibir a imagem, é necessário juntar esse caminho com a URL base de imagens do TMDB.[1]

A estrutura da imagem é:

```text
https://image.tmdb.org/t/p/w185/POSTER_PATH
```

Por exemplo, se o valor de `poster_path` for:

```text
/abc123.jpg
```

A imagem completa será:

```text
https://image.tmdb.org/t/p/w185/abc123.jpg
```

Informações completas em:

[Como mostrar a imagem do filme usando a API do TMDB](https://github.com/romuloccomp/exercicio-tmdb-ii/blob/main/Como%20mostrar%20a%20imagem%20do%20filme.md)

## Gêneros dos filmes

Na listagem de filmes em cartaz, os gêneros aparecem como números no campo `genre_ids`. Para transformar esses números em nomes, será necessário consultar a lista de gêneros da API do TMDB.[2]

Depois disso, o sistema deverá comparar os IDs do filme com os IDs da lista de gêneros e exibir os nomes encontrados.

API/URL de gêneros: https://api.themoviedb.org/3/genre/movie/list?language=pt-BR

Informações completas em:

[Como mostrar os gêneros](https://github.com/romuloccomp/exercicio-tmdb-ii/blob/main/Como%20mostrar%20os%20ge%CC%82neros.md)

## Filtro no front-end

O filtro deverá funcionar sem fazer uma nova requisição para a API. A lista original de filmes deve ficar guardada no JavaScript, e o filtro deve apenas decidir quais filmes continuam aparecendo na tela.

A pesquisa deve considerar:

| Campo | Como deve funcionar |
|---|---|
| Título | Se o texto digitado aparecer no título, o filme deve ser exibido. |
| Descrição | Se o texto digitado aparecer na descrição, o filme deve ser exibido. |
| Campo vazio | Todos os filmes devem voltar a aparecer. |

Para essa etapa, podem ser usados métodos de array como `filter` e `map`.

Informações completas em:

[Como filtrar](https://github.com/romuloccomp/exercicio-tmdb-ii/blob/main/Como%20usar%20filtrar.md)

## Entrega esperada

Ao final desta parte, a aplicação deverá mostrar uma lista de filmes em cartaz contendo **imagem**, **título**, **descrição** e **gêneros**. Além disso, o usuário deverá conseguir pesquisar filmes pelo título ou pela descrição usando um único campo de texto.

## Critérios de conclusão

| Critério | Situação esperada |
|---|---|
| Imagem | O pôster do filme aparece na listagem. |
| Gêneros | Os gêneros aparecem com nomes, e não apenas com IDs. |
| Filtro | O campo de pesquisa filtra por título ou descrição. |
| Front-end | O filtro acontece sem recarregar a página. |
| Lista original | Ao limpar o campo de pesquisa, todos os filmes voltam a aparecer. |

## Materiais de apoio

| Tema | Link |
|---|---|
| Imagem do pôster | [Como mostrar a imagem do filme usando a API do TMDB](https://github.com/romuloccomp/exercicio-tmdb-ii/blob/main/Como%20mostrar%20a%20imagem%20do%20filme.md) |
| Gêneros dos filmes | [Como mostrar os gêneros](https://github.com/romuloccomp/exercicio-tmdb-ii/blob/main/Como%20mostrar%20os%20ge%CC%82neros.md) |
| Filtro no front-end | [Como usar filtrar](https://github.com/romuloccomp/exercicio-tmdb-ii/blob/main/Como%20usar%20filtrar.md) |

## Referências

[1]: https://developer.themoviedb.org/reference/movie-images "TMDB — Movie Images"  
[2]: https://developer.themoviedb.org/reference/genre-movie-list "TMDB — Genre Movie List"
