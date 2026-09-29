# QA-Test-Cypress

![Cypress](https://img.shields.io/badge/Cypress-15-17202C?style=flat&logo=cypress&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)

End-to-end (E2E) test automation with **Cypress** against two real-world, high-traffic marketplaces:

| Project | Website | Specs | Test cases |
|---|---|---|---|
| [`Teste MercadoLivre`](./Teste%20MercadoLivre) | [mercadolivre.com.br](https://www.mercadolivre.com.br) 🇧🇷 | 8 | 39 |
| [`Test Subito Italia`](./Test%20Subito%20Italia) | [subito.it](https://www.subito.it) 🇮🇹 | 7 | 36 |

Every test case is also documented in a **Given / When / Then** format, including the expected result and a **priority level** (High / Medium / Low). This makes the suite readable for anyone on the team, not only for the people who write code.

## 🎯 Why this project

Testing public production websites that I don't control is a good exercise in the real-world problems of UI automation:

- **Third-party noise:** production sites throw uncaught JavaScript errors from ads and trackers, so the specs handle `uncaught:exception` to avoid false failures.
- **Cookie consent banners:** Subito.it shows a GDPR banner that blocks the page. A custom command (`cy.acceptCookies()`) closes it only when it appears.
- **Slow, heavy pages:** the timeouts are tuned (`defaultCommandTimeout: 10000`, `pageLoadTimeout: 30000`) so the tests stay stable.
- **Changing UIs:** the selectors are grouped by page section, so maintenance stays local when the site changes.

## 🧪 What is covered

Both suites test the **homepage** of each marketplace, split into one spec per UI area:

| Area | Mercado Livre | Subito.it | What is validated |
|---|:---:|:---:|---|
| Header & navigation | ✅ 7 | ✅ 6 | Logo, search bar, login/sign-up links, cart |
| Search | ✅ 5 | ✅ 6 | Typing, clearing, empty search, form `action` and field `name`, submitting a term |
| Carousel / banners | ✅ 4 | ✅ 4 | Visibility, images loaded, navigation buttons |
| Categories | ✅ 10 | ✅ 10 | Section visible, main categories listed, icons, clickable links |
| Quick access | ✅ 4 | — | Shortcut cards, titles and icons |
| Featured ads / recommendations | ✅ 2 | ✅ 3 | Product cards rendered with images |
| Page metadata (SEO) | ✅ 4 | ✅ 3 | `<title>`, canonical URL, `lang` attribute, favicon |
| Page structure | ✅ 3 | ✅ 4 | Header, footer, page fully loaded (`readyState`) |

## 📁 Project structure

```
QA-Test-Cypress/
├── Teste MercadoLivre/
│   ├── cypress/
│   │   ├── e2e/
│   │   │   ├── header.cy.js              # one spec per UI area
│   │   │   ├── header_documentacao.md    # Given/When/Then docs for that spec
│   │   │   └── ...
│   │   ├── fixtures/
│   │   └── support/
│   ├── cypress.config.js
│   └── package.json
│
└── Test Subito Italia/
    ├── cypress/
    │   ├── e2e/                          # specs (baseUrl: https://www.subito.it/)
    │   └── support/commands.js           # cy.acceptCookies()
    ├── docs/                             # Given/When/Then docs per spec
    ├── cypress.config.js
    └── package.json
```

## 📝 Test documentation example

Every spec has a matching Markdown file that describes each test case. Example from the Mercado Livre search suite (the docs are written in Portuguese):

> **Teste 3: Campo de busca vazio não redireciona**  
> **Dado que:** o usuário acessa a página inicial do Mercado Livre  
> **e:** o campo de busca está vazio  
> **e:** o usuário clica no botão de busca  
> **então:** a página não deve redirecionar  
> **Grau de importância:** Médio — evita buscas vazias que poderiam causar erros

## 🚀 How to run

**Requirements:** Node.js 18+ and npm.

```bash
git clone https://github.com/mvterrito-ui/QA-Test-Cypress.git
cd QA-Test-Cypress

# pick one of the projects
cd "Teste MercadoLivre"      # or: cd "Test Subito Italia"

npm install

npm run cy:open   # interactive mode (Cypress Test Runner)
npm run cy:run    # headless mode (terminal)
```

> ⚠️ These tests run against **live production websites**. If the site changes its layout or blocks automated traffic (captcha, geo-blocking), some tests may fail. That is expected behavior for this kind of suite, and it doesn't mean the test logic is wrong.

## 🛠️ Tech stack

- [Cypress 15](https://www.cypress.io/): E2E testing framework
- JavaScript (CommonJS)
- Node.js / npm

## 👤 Author

**Marcos Territo**, QA Engineer on the path to SDET
[GitHub](https://github.com/mvterrito-ui) · [LinkedIn](https://www.linkedin.com/in/mvterrito/)
