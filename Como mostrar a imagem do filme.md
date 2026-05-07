# Como mostrar a imagem do filme usando a API do TMDB

**Disciplina:** Desenvolvimento em JavaScript  
**Professor:** Romulo Pereira  
**Tema:** Exibição de imagens do TMDB no front-end

## 1. Entendendo o problema

Quando buscamos os filmes em cartaz na API do **TMDB**, a resposta traz várias informações sobre cada filme, como título, descrição, data de lançamento, gêneros e caminho da imagem.

Porém, a API **não envia a imagem completa pronta** dentro do campo do filme. Ela envia apenas uma parte do caminho da imagem, chamada `poster_path`.

Isso significa que o aluno precisa aprender a montar o endereço completo da imagem antes de exibi-la na página.

## 2. O que é o `poster_path`?

O campo `poster_path` representa o caminho parcial da imagem do pôster do filme.

Por exemplo, um filme pode retornar o seguinte valor:

```text
/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg
```

Esse valor sozinho **não é suficiente** para abrir a imagem no navegador. Para funcionar, ele precisa ser unido com a URL base de imagens do TMDB.

## 3. URL base das imagens

Para mostrar uma imagem do TMDB, usamos a seguinte estrutura:

```text
https://image.tmdb.org/t/p/TAMANHO/CAMINHO_DA_IMAGEM
```

No nosso exercício, vamos usar o tamanho `w185`, que gera uma imagem com largura aproximada de 185 pixels.

| Parte | Significado |
|---|---|
| `https://image.tmdb.org/t/p/` | Endereço base das imagens do TMDB. |
| `w185` | Tamanho da imagem. |
| `/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg` | Caminho da imagem recebido no campo `poster_path`. |

## 4. Exemplo funcionando

A imagem abaixo é um exemplo real de pôster funcionando com o tamanho `w185`:

```text
https://image.tmdb.org/t/p/w185/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg
```

Você pode testar abrindo este link no navegador:

[https://image.tmdb.org/t/p/w185/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg](https://image.tmdb.org/t/p/w185/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg)

## 5. Como montar a imagem no JavaScript

Imagine que temos um objeto chamado `filme`, e esse objeto possui o campo `poster_path`.

```javascript
const filme = {
  title: "Exemplo de Filme",
  poster_path: "/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg"
};
```

Para montar o endereço completo da imagem, criamos primeiro a URL base:

```javascript
const urlBaseImagem = "https://image.tmdb.org/t/p/w185";
```

Depois, juntamos a URL base com o valor de `poster_path`:

```javascript
const imagemCompleta = urlBaseImagem + filme.poster_path;
```

O resultado será:

```text
https://image.tmdb.org/t/p/w185/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg
```

## 6. Usando template string

Outra forma de montar a mesma imagem é usando **template string**.

```javascript
const imagemCompleta = `${urlBaseImagem}${filme.poster_path}`;
```

As duas formas funcionam. Para alunos iniciantes, a concatenação com `+` pode ser mais fácil de entender no primeiro momento.

## 7. Colocando a imagem no HTML

Depois que o endereço completo da imagem foi montado, ele deve ser colocado no atributo `src` de uma tag `img`.

```html
<img src="https://image.tmdb.org/t/p/w185/b3WeTp42eJSRuE4UZfyPCOJW4c.jpg" alt="Pôster do filme">
```

No JavaScript, esse HTML pode ser montado junto com as demais informações do filme.

```javascript
const cardFilme = `
  <div class="filme">
    <img src="${imagemCompleta}" alt="Pôster do filme ${filme.title}">
    <h2>${filme.title}</h2>
  </div>
`;
```

## 8. Exemplo dentro de uma função

A função abaixo recebe um filme e monta um pequeno bloco HTML com a imagem e o título.

```javascript
function montarCardDoFilme(filme) {
  const urlBaseImagem = "https://image.tmdb.org/t/p/w185";
  const imagemCompleta = urlBaseImagem + filme.poster_path;

  return `
    <div class="filme">
      <img src="${imagemCompleta}" alt="Pôster do filme ${filme.title}">
      <h2>${filme.title}</h2>
    </div>
  `;
}
```

## 9. Cuidado com filmes sem imagem

Alguns filmes podem vir sem imagem. Nesse caso, o campo `poster_path` pode estar vazio ou com valor `null`.

Para evitar erro ou imagem quebrada, podemos verificar se existe imagem antes de montar a tag `img`.

```javascript
function montarImagemDoFilme(filme) {
  const urlBaseImagem = "https://image.tmdb.org/t/p/w185";

  if (filme.poster_path === null) {
    return "<p>Imagem não disponível</p>";
  }

  const imagemCompleta = urlBaseImagem + filme.poster_path;

  return `<img src="${imagemCompleta}" alt="Pôster do filme ${filme.title}">`;
}
```

## 10. Resumo da lógica

Para mostrar a imagem do filme, o aluno deve seguir uma sequência simples.

| Passo | O que fazer |
|---|---|
| 1 | Pegar o valor do campo `poster_path`. |
| 2 | Criar a URL base `https://image.tmdb.org/t/p/w185`. |
| 3 | Juntar a URL base com o `poster_path`. |
| 4 | Usar o resultado no atributo `src` da tag `img`. |
| 5 | Verificar se `poster_path` não está vazio ou nulo. |

## 11. Exemplo final simplificado

```javascript
const urlBaseImagem = "https://image.tmdb.org/t/p/w185";
const imagemCompleta = urlBaseImagem + filme.poster_path;

listaFilmes.innerHTML += `
  <div class="filme">
    <img src="${imagemCompleta}" alt="Pôster do filme ${filme.title}">
    <h2>${filme.title}</h2>
    <p>${filme.overview}</p>
  </div>
`;
```

## 12. Conclusão

A parte mais importante é entender que o campo `poster_path` não é uma imagem completa. Ele é apenas o caminho final da imagem. Para exibir o pôster, é necessário montar a URL completa usando a base de imagens do TMDB.

Com essa lógica, cada filme exibido na tela poderá ter seu próprio pôster, deixando a aplicação mais visual e mais próxima de um sistema real de consulta de filmes.

## Referência

[1]: https://developer.themoviedb.org/reference/movie-images "TMDB — Movie Images"
