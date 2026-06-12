# Caderneta · Dívidas Mensais

> Controle financeiro pessoal simples, rápido e sem dependências externas.

**Caderneta** é uma aplicação web para rastrear dívidas e despesas mensais. Roda 100% no navegador, armazena os dados localmente e não requer instalação, servidor ou conta.

---

## Funcionalidades

- **Gestão de dívidas** — adicione, edite e exclua dívidas com nome, valor, vencimento e categoria
- **Controle de renda** — informe o salário/renda de cada mês e veja quanto sobra
- **Dívidas recorrentes** — marque uma dívida como recorrente e ela será copiada automaticamente para o mês seguinte
- **Pagamentos** — marque dívidas como pagas com um toque; progresso exibido em barra e porcentagem
- **Múltiplos meses** — navegue entre meses por abas fixas na parte inferior
- **Filtros e ordenação** — busque por nome, filtre por categoria, ordene por vencimento, valor ou nome
- **Gráfico de categorias** — visualize a distribuição das dívidas por categoria em barras horizontais
- **Exportação** — faça backup completo dos dados em JSON (`caderneta-backup.json`)
- **Design responsivo** — mobile-first, funciona bem em qualquer tamanho de tela

---

## Tecnologias

| Camada      | Tecnologia                        |
|-------------|-----------------------------------|
| Markup      | HTML5                             |
| Estilos     | CSS3 com variáveis (tema via `:root`) |
| Scripts     | JavaScript puro (ES6+)            |
| Tipografia  | [Archivo](https://fonts.google.com/specimen/Archivo) + [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) (Google Fonts) |
| Persistência| `localStorage` do navegador       |

Sem frameworks, sem bundlers, sem node_modules — apenas um único arquivo `index.html`.

---

## Como usar

### Opção 1 — Abrir direto no navegador

```bash
# Clone o repositório
git clone https://github.com/ricardovsantos/dividex.git
cd dividex

# Abra o arquivo no seu navegador favorito
# Linux
xdg-open index.html

# macOS
open index.html

# Windows
start index.html
```

### Opção 2 — Servidor HTTP local

```bash
# Python 3
python -m http.server 8000

# Node.js (npx, sem instalação prévia)
npx serve .

# PHP
php -S localhost:8000
```

Acesse `http://localhost:8000` no navegador.

---

## Estrutura do projeto

```
dividex/
└── index.html   # Aplicação completa (HTML + CSS + JS em um único arquivo)
```

---

## Como funciona

### Estado da aplicação

Toda a lógica de estado é mantida em um objeto central persistido no `localStorage` com a chave `caderneta-v1`:

```js
{
  months: {
    "<id>": {
      name: "Jun 26",
      salary: 3000,
      debts: [
        {
          id: "abc12345",
          name: "Aluguel",
          value: 1200,
          due: 5,        // dia do vencimento
          cat: "Fixa",   // categoria
          rec: true,     // recorrente?
          paid: false
        }
      ]
    }
  },
  order: ["<id1>", "<id2>"],  // sequência dos meses
  current: "<id>"              // mês ativo
}
```

### Categorias disponíveis

| Categoria    | Descrição                     |
|--------------|-------------------------------|
| Fixa         | Despesas fixas mensais        |
| Assinatura   | Serviços de assinatura        |
| Cartão       | Fatura de cartão de crédito   |
| Empréstimo   | Parcelas de empréstimo        |
| Pessoa       | Dívida com pessoa física      |
| Outro        | Demais despesas               |

### Resumo financeiro

O painel superior exibe:

- **Sobra** — `Renda − Total de dívidas` (verde se positivo, vermelho se negativo)
- **Renda** — valor informado para o mês
- **Total Dívidas** — soma de todas as dívidas do mês
- **A Pagar** — soma das dívidas ainda não marcadas como pagas
- **Progresso** — porcentagem de dívidas pagas no mês

---

## Tema e cores

As cores são definidas por variáveis CSS no `:root` e podem ser customizadas diretamente no `index.html`:

| Variável        | Valor padrão | Uso                          |
|-----------------|-------------|------------------------------|
| `--paper`       | `#ECEFF1`   | Fundo geral                  |
| `--card`        | `#FFFFFF`   | Fundo dos cards              |
| `--ink`         | `#16241F`   | Cor principal do texto        |
| `--ledger`      | `#0B5C46`   | Cor primária (verde escuro)   |
| `--debt`        | `#C0392B`   | Alertas e valores negativos  |
| `--gold`        | `#B98A2F`   | Destaque / ponto decorativo  |

---

## Dados e privacidade

- Todos os dados ficam **exclusivamente no seu navegador** via `localStorage`
- Nenhuma informação é enviada para servidores externos
- Use a função **Exportar** para fazer backup antes de limpar o cache do navegador
- O arquivo de backup pode ser importado manualmente colando o JSON no `localStorage` via console do navegador

---

## Compatibilidade

Qualquer navegador moderno com suporte a ES6 e `localStorage`:

- Chrome / Edge 80+
- Firefox 75+
- Safari 13.1+
- Opera 67+

---

## Licença

Distribuído sob a licença **MIT**. Veja o arquivo `LICENSE` para mais detalhes.

---

## Autor

Desenvolvido por [Ricardo Santos](https://github.com/ricardovsantos).
