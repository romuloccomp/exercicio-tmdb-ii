# Como mostrar os gêneros dos filmes usando JavaScript

**Disciplina:** Desenvolvimento em JavaScript  
**Professor:** Romulo Pereira  
**Tema:** Relacionando IDs com nomes de gêneros

## 1. Entendendo o problema

Na API do **TMDB**, cada filme pode trazer uma lista de gêneros. Porém, na resposta dos filmes em cartaz, esses gêneros normalmente aparecem como **IDs**, ou seja, como números.

Por exemplo, um filme pode vir assim:

```javascript
const filme = {
  title: "Filme de Exemplo",
  genre_ids: [28, 12, 878]
};
```

Nesse caso, o filme possui três gêneros, mas ainda não sabemos os nomes deles. Sabemos apenas os códigos: `28`, `12` e `878`.

Para mostrar os nomes na tela, precisamos comparar esses IDs com uma segunda lista: a lista completa de gêneros.

## 2. Lista de gêneros

A lista de gêneros pode ser entendida como uma tabela de referência. Cada gênero possui um `id` e um `name`.

```javascript
const generos = [
  { id: 28, name: "Ação" },
  { id: 12, name: "Aventura" },
  { id: 16, name: "Animação" },
  { id: 35, name: "Comédia" },
  { id: 878, name: "Ficção científica" }
];
```

Agora temos duas informações importantes.

| Informação | Exemplo | Significado |
|---|---|---|
| `genre_ids` | `[28, 12, 878]` | Lista de IDs dos gêneros de um filme. |
| `generos` | `{ id: 28, name: "Ação" }` | Lista usada para descobrir o nome de cada ID. |

## 3. Objetivo

O objetivo é transformar isto:

```javascript
[28, 12, 878]
```

Nisto:

```javascript
["Ação", "Aventura", "Ficção científica"]
```

Depois disso, fica mais fácil mostrar os nomes dos gêneros junto com o filme na tela.

## 4. Usando `find` para buscar um gênero

O método `find` serve para procurar **um item dentro de um array**. Ele percorre a lista e retorna o primeiro elemento que atender à condição.

Primeiro, vamos buscar apenas um gênero.

```javascript
const generos = [
  { id: 28, name: "Ação" },
  { id: 12, name: "Aventura" },
  { id: 16, name: "Animação" },
  { id: 35, name: "Comédia" },
  { id: 878, name: "Ficção científica" }
];

const idProcurado = 28;

const generoEncontrado = generos.find(function(genero) {
  return genero.id === idProcurado;
});

console.log(generoEncontrado);
```

O resultado será:

```javascript
{ id: 28, name: "Ação" }
```

## 5. Entendendo o código com `find`

| Parte do código | Significado |
|---|---|
| `generos.find(...)` | Percorre a lista de gêneros. |
| `function(genero)` | Recebe um gênero por vez. |
| `genero.id === idProcurado` | Verifica se o ID do gênero é igual ao ID procurado. |
| `generoEncontrado` | Guarda o objeto encontrado. |

Se a condição for verdadeira, o `find` retorna aquele objeto. Se nenhum item for encontrado, o resultado será `undefined`.

## 6. Buscando vários gêneros de um filme

Um filme pode ter vários IDs de gênero. Por isso, podemos percorrer a lista `genre_ids` e, para cada ID, usar `find` na lista de gêneros.

```javascript
const filme = {
  title: "Filme de Exemplo",
  genre_ids: [28, 12, 878]
};

const generos = [
  { id: 28, name: "Ação" },
  { id: 12, name: "Aventura" },
  { id: 16, name: "Animação" },
  { id: 35, name: "Comédia" },
  { id: 878, name: "Ficção científica" }
];

const nomesDosGeneros = filme.genre_ids.map(function(idGenero) {
  const generoEncontrado = generos.find(function(genero) {
    return genero.id === idGenero;
  });

  return generoEncontrado.name;
});

console.log(nomesDosGeneros);
```

O resultado será:

```javascript
["Ação", "Aventura", "Ficção científica"]
```

## 7. Cuidado quando o gênero não for encontrado

Em alguns casos, pode acontecer de um ID não existir na lista de gêneros. Para evitar erro, podemos verificar se o gênero foi encontrado antes de acessar o `name`.

```javascript
const nomesDosGeneros = filme.genre_ids.map(function(idGenero) {
  const generoEncontrado = generos.find(function(genero) {
    return genero.id === idGenero;
  });

  if (generoEncontrado) {
    return generoEncontrado.name;
  }

  return "Gênero não encontrado";
});
```

Essa verificação evita erro caso `generoEncontrado` seja `undefined`.

## 8. Transformando a lista em texto

Depois de gerar a lista com os nomes dos gêneros, podemos transformar o array em um texto usando `join`.

```javascript
const textoGeneros = nomesDosGeneros.join(", ");

console.log(textoGeneros);
```

O resultado será:

```text
Ação, Aventura, Ficção científica
```

Esse texto pode ser exibido dentro do card do filme.

## 9. Exemplo final usando `find`

```javascript
function buscarNomesDosGeneros(filme, generos) {
  const nomesDosGeneros = filme.genre_ids.map(function(idGenero) {
    const generoEncontrado = generos.find(function(genero) {
      return genero.id === idGenero;
    });

    if (generoEncontrado) {
      return generoEncontrado.name;
    }

    return "Gênero não encontrado";
  });

  return nomesDosGeneros.join(", ");
}
```

Usando a função:

```javascript
const textoGeneros = buscarNomesDosGeneros(filme, generos);

console.log(textoGeneros);
```

Resultado:

```text
Ação, Aventura, Ficção científica
```

## 10. A mesma lógica usando `for`

Também podemos resolver o mesmo problema usando `for`. Essa versão é mais longa, mas ajuda a entender o passo a passo.

```javascript
function buscarNomesDosGenerosComFor(filme, generos) {
  const nomesDosGeneros = [];

  for (let i = 0; i < filme.genre_ids.length; i++) {
    const idGenero = filme.genre_ids[i];

    for (let j = 0; j < generos.length; j++) {
      const genero = generos[j];

      if (genero.id === idGenero) {
        nomesDosGeneros.push(genero.name);
      }
    }
  }

  return nomesDosGeneros.join(", ");
}
```

Usando a função:

```javascript
const textoGeneros = buscarNomesDosGenerosComFor(filme, generos);

console.log(textoGeneros);
```

Resultado:

```text
Ação, Aventura, Ficção científica
```

## 11. Comparando `find` e `for`

As duas formas funcionam. A diferença é que o `find` deixa o código mais direto quando queremos procurar um item dentro de uma lista.

| Forma | Característica |
|---|---|
| `find` | Mais direto para buscar um item específico dentro de um array. |
| `for` | Mais detalhado e útil para visualizar a repetição passo a passo. |

## 12. Ligação com o trabalho dos filmes

No trabalho do TMDB, a lista de filmes vem com `genre_ids`, enquanto a lista de gêneros vem em outro endpoint da API. A lógica será a seguinte.

| Passo | O que fazer |
|---|---|
| 1 | Buscar os filmes em cartaz. |
| 2 | Buscar a lista de gêneros. |
| 3 | Para cada filme, pegar o array `genre_ids`. |
| 4 | Para cada ID, procurar o gênero correspondente na lista de gêneros. |
| 5 | Mostrar os nomes dos gêneros no card do filme. |

## 13. Exemplo simplificado para o card do filme

```javascript
const textoGeneros = buscarNomesDosGeneros(filme, generos);

const cardFilme = `
  <div class="filme">
    <h2>${filme.title}</h2>
    <p>${filme.overview}</p>
    <p><strong>Gêneros:</strong> ${textoGeneros}</p>
  </div>
`;
```

## 14. Conclusão

Para mostrar os gêneros dos filmes, precisamos relacionar duas listas: a lista de IDs que vem em cada filme e a lista completa de gêneros. O `find` ajuda a localizar o objeto do gênero pelo ID, enquanto o `map` ajuda a transformar a lista de IDs em uma lista de nomes.

A versão com `for` mostra a mesma lógica de maneira mais detalhada. Ela pode ser útil para entender o funcionamento interno antes de usar métodos como `find` e `map`.

## Referência

[1]: https://developer.themoviedb.org/reference/genre-movie-list "TMDB — Genre Movie List"
