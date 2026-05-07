# Como usar `filter` em JavaScript

**Disciplina:** Desenvolvimento em JavaScript  
**Professor:** Romulo Pereira  
**Tema:** Filtrando dados no front-end

## 1. O que é o `filter`?

O `filter` é um método usado em arrays no JavaScript. Ele serve para criar uma **nova lista** contendo apenas os itens que passam por uma condição.

Em outras palavras, usamos `filter` quando temos uma lista maior e queremos separar apenas alguns elementos dessa lista.

> O `filter` não altera a lista original. Ele cria uma nova lista com os itens que atenderam à condição.

## 2. Exemplo simples: lista de nomes

Vamos começar com um exemplo simples, usando apenas uma lista de nomes.

```javascript
const nomes = ["Ana", "Bruno", "Carlos", "Amanda", "Beatriz", "João"];
```

Imagine que queremos buscar somente os nomes que começam com a letra **A**.

## 3. Usando `filter`

```javascript
const nomes = ["Ana", "Bruno", "Carlos", "Amanda", "Beatriz", "João"];

const nomesComA = nomes.filter(function(nome) {
  return nome.startsWith("A");
});

console.log(nomesComA);
```

O resultado será:

```javascript
["Ana", "Amanda"]
```

## 4. Entendendo o código

No exemplo anterior, o `filter` passa por cada item do array `nomes`.

| Parte do código | Significado |
|---|---|
| `nomes.filter(...)` | Percorre a lista de nomes. |
| `function(nome)` | Recebe um nome por vez. |
| `nome.startsWith("A")` | Verifica se o nome começa com a letra A. |
| `return` | Define se o nome entra ou não na nova lista. |

Se a condição retornar `true`, o item entra na nova lista. Se retornar `false`, o item fica de fora.

## 5. Outro exemplo: filtrar pelo texto digitado

Em uma aplicação real, o usuário pode digitar um texto em um campo de pesquisa. Nesse caso, podemos filtrar os nomes que possuem esse texto.

```javascript
const nomes = ["Ana", "Bruno", "Carlos", "Amanda", "Beatriz", "João"];

const textoDigitado = "an";

const nomesFiltrados = nomes.filter(function(nome) {
  return nome.toLowerCase().includes(textoDigitado.toLowerCase());
});

console.log(nomesFiltrados);
```

O resultado será:

```javascript
["Ana", "Amanda"]
```

Nesse exemplo, usamos `toLowerCase()` para evitar problema com letras maiúsculas e minúsculas. Assim, pesquisar por `an`, `An` ou `AN` pode funcionar da mesma forma.

## 6. A mesma lógica usando `for`

Antes de usar `filter`, é importante entender que ele faz uma repetição por trás. A mesma ideia pode ser feita com `for`.

```javascript
const nomes = ["Ana", "Bruno", "Carlos", "Amanda", "Beatriz", "João"];

const textoDigitado = "an";
const nomesFiltrados = [];

for (let i = 0; i < nomes.length; i++) {
  const nome = nomes[i];

  if (nome.toLowerCase().includes(textoDigitado.toLowerCase())) {
    nomesFiltrados.push(nome);
  }
}

console.log(nomesFiltrados);
```

O resultado será o mesmo:

```javascript
["Ana", "Amanda"]
```

## 7. Comparando `filter` e `for`

As duas formas resolvem o problema. A diferença é que o `filter` deixa o código mais curto e mais direto quando o objetivo é apenas filtrar uma lista.

| Forma | Característica |
|---|---|
| `filter` | Mais curto e indicado quando queremos gerar uma nova lista filtrada. |
| `for` | Mais detalhado e útil para entender a lógica passo a passo. |

## 8. Ligação com o trabalho dos filmes

No trabalho dos filmes, a ideia será parecida. Em vez de uma lista simples de nomes, teremos uma lista de filmes.

Cada filme terá informações como `title` e `overview`. O filtro poderá verificar se o texto digitado aparece no título ou na descrição.

Exemplo simplificado:

```javascript
const filmesFiltrados = filmes.filter(function(filme) {
  return filme.title.toLowerCase().includes(textoDigitado.toLowerCase()) ||
         filme.overview.toLowerCase().includes(textoDigitado.toLowerCase());
});
```

Nesse caso, o operador `||` significa **ou**. Portanto, o filme será mantido na lista se o texto aparecer no título **ou** na descrição.

## 9. Resumo

O método `filter` é usado quando queremos separar alguns itens de uma lista. Ele percorre o array, testa uma condição e cria uma nova lista apenas com os elementos que passaram no teste.

| Passo | O que acontece |
|---|---|
| 1 | Temos uma lista original. |
| 2 | Definimos uma condição. |
| 3 | O `filter` testa cada item. |
| 4 | Os itens aprovados entram em uma nova lista. |
| 5 | A lista original continua igual. |

## 10. Conclusão

O `filter` é uma ferramenta importante para trabalhar com listas no JavaScript. No exercício do TMDB, ele será usado para permitir que o usuário pesquise filmes sem precisar fazer uma nova requisição para a API. A filtragem acontece diretamente no front-end, usando os dados que já foram carregados.
