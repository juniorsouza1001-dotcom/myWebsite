# Histórico de Pesquisas

Este documento descreve a implementação feita no projeto para gravar pesquisas no `localStorage` e os ajustes visuais realizados na caixa principal.

## Objetivo

- Persistir histórico de buscas em `localStorage`
- Criar funções reutilizáveis em JavaScript
- Não alterar a cor de fundo da página
- Ajustar a caixa principal para um tom bege

## Arquivos modificados

### `script.js`

Funções adicionadas:

- `const SEARCH_HISTORY_KEY = 'searchHistory'`
  - chave usada no `localStorage`

- `getSearchHistory()`
  - lê o valor salvo em `localStorage`
  - converte de JSON para array
  - retorna `[]` quando não há histórico ou o dado está inválido

- `saveSearchQuery(query)`
  - valida se o valor é uma string não vazia
  - usa `trim()` para remover espaços extras
  - evita salvar o mesmo termo em sequência
  - limita o histórico a 20 itens
  - converte o array para JSON e salva em `localStorage`

- `clearSearchHistory()`
  - remove a chave de histórico do `localStorage`

Exposição global das funções:

- `window.getSearchHistory = getSearchHistory`
- `window.saveSearchQuery = saveSearchQuery`
- `window.clearSearchHistory = clearSearchHistory`

Isso permite usar as funções diretamente no console do navegador ou em outros scripts.

## Como funciona o `localStorage`

O `localStorage` armazena apenas strings. Por isso a abordagem é:

1. Ler o valor com `localStorage.getItem(SEARCH_HISTORY_KEY)`
2. Converter de JSON com `JSON.parse(rawHistory)`
3. Atualizar o array de histórico
4. Salvar de volta com `localStorage.setItem(SEARCH_HISTORY_KEY, JSON.stringify(history))`

Exemplo de valor salvo:

```json
["busca 1", "busca 2", "busca 3"]
```

## Uso das funções

No console do navegador ou em outro script, use:

```js
saveSearchQuery('minha pesquisa')
const history = getSearchHistory()
clearSearchHistory()
```

## Ajuste visual da caixa principal

A caixa principal do layout foi ajustada para um tom bege sem alterar o fundo geral do site.

Estilos aplicados na regra da caixa principal:

- `background: #f4e8d3;`
- `border: 1px solid rgba(26, 23, 20, 0.08);`
- `box-shadow: 0 20px 40px rgba(26, 23, 20, 0.08);`

Se houver um pseudo-elemento de overlay, use algo leve como:

- `background: rgba(210, 160, 110, 0.08);`
- `opacity: 0.12`

Isso garante um visual bege suave e mantém o fundo da página intacto.

## Como aplicar em outros estudos

1. Copie o conteúdo de `script.js` para outro projeto.
2. Mantenha a constante `SEARCH_HISTORY_KEY` com a chave desejada.
3. Importe ou inclua o script na página HTML.
4. Chame `saveSearchQuery`, `getSearchHistory` e `clearSearchHistory` conforme necessário.

### Dicas

- Use `trim()` para evitar entradas vazias ou apenas com espaços.
- Sempre trate `JSON.parse()` com `try/catch` para evitar erros quando o valor de `localStorage` estiver inválido.
- Limite o número de itens salvos para não lotar o armazenamento.
- `localStorage` é específico do domínio, então só estará disponível no mesmo site/origem.

## Resumo rápido

- `getSearchHistory()` lê o histórico
- `saveSearchQuery(query)` salva uma pesquisa nova
- `clearSearchHistory()` apaga todo o histórico
- A caixa do hero foi deixada bege com bordas suaves e sombra leve
