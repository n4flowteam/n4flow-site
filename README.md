# n4flow — Site institucional

Site estático da **n4flow** (IA, Dados & Automação). HTML, CSS e JS puros, sem build step, sem dependências.

## Estrutura

```
.
├── index.html                     # Home
├── automacao/index.html           # /automacao/
├── ia/index.html                  # /ia/
├── dados/index.html               # /dados/
├── sobre/index.html               # /sobre/
├── diagnostico/
│   ├── index.html                 # /diagnostico/ (formulário)
│   └── obrigado.html              # /diagnostico/obrigado.html
├── assets/
│   └── img/                       # Imagens do site (referenciadas por /assets/img/...)
│       ├── home-hero.png
│       ├── home-velocimetro.png
│       ├── automacao-equipe.jpg
│       ├── dados-profissional.jpg
│       ├── ia-executivo.png
│       └── antonio-bennati.jpg
├── 404.html                       # Página de erro customizada
├── favicon.svg                    # Ícone do site
├── .nojekyll                      # Desliga o Jekyll no GitHub Pages
└── .gitignore
```

Cada seção do site é uma pasta com `index.html`, então as URLs ficam limpas (`/ia/` em vez de `/ia.html`). Isso funciona igual em GitHub Pages, Netlify, Vercel e Cloudflare Pages.

## Subir no GitHub

```bash
cd n4flow-site
git init
git add .
git commit -m "Site institucional n4flow"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/n4flow-site.git
git push -u origin main
```

## Hospedar

### Opção 1 — Netlify (recomendado, formulário funciona)

1. Entre em [app.netlify.com](https://app.netlify.com) e escolha **Add new site → Import from Git**.
2. Selecione o repo. Não há build command — apenas **Publish directory: `/`**.
3. Vá em **Site settings → Domain management** e aponte o domínio `n4flow.com.br`.

O formulário de diagnóstico usa `data-netlify="true"`. No Netlify, as submissões aparecem em **Forms** no painel, já com os campos organizados.

### Opção 2 — GitHub Pages

1. No repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / root**.
2. O site sobe em `https://SEU-USUARIO.github.io/n4flow-site/`.

> ⚠️ **Atenção:** no GitHub Pages o formulário de diagnóstico **não processa as submissões** (GitHub Pages é 100% estático). Para o formulário funcionar, hospede pelo Netlify ou troque a integração por [Formspree](https://formspree.io), [Getform](https://getform.io) ou similar — basta alterar o `action` do `<form>` em `diagnostico/index.html`.

### Opção 3 — Vercel / Cloudflare Pages

Conecte o repo em [vercel.com](https://vercel.com) ou [pages.cloudflare.com](https://pages.cloudflare.com), sem framework, deploy direto.

## Rodar localmente

Qualquer servidor estático serve. Com Python:

```bash
cd n4flow-site
python3 -m http.server 8000
```

Acesse `http://localhost:8000`.

## O que foi ajustado dos originais

- Nomes normalizados (`index (63).html` → `index.html`; pastas para cada seção).
- Removido o script residual do Cloudflare (`email-decode.min.js`) que só funcionava no ambiente anterior.
- Adicionado `favicon.svg`, `404.html` e `.nojekyll`.
- Links internos (`/`, `/ia/`, `/sobre/` etc.) validados — nenhum aponta para arquivo inexistente.
- **Imagens extraídas do HTML** — antes elas estavam embutidas em base64 dentro dos arquivos (a página `/ia/` tinha 4.7MB). Agora estão em `/assets/img/` como arquivos separados, o que:
  - reduziu o HTML da `/ia/` de **4.7MB para 83KB**;
  - permite cache separado das imagens (após o primeiro acesso elas não são mais baixadas);
  - **qualidade 100% preservada** — as imagens foram extraídas bit-a-bit, sem nenhuma recompressão (hash SHA-256 idêntico ao binário original embutido).

## Contato

São Paulo, SP · Atendimento em todo o Brasil
