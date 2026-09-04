# Portfólio — Thiago Ribeiro (Professor de História)

Site de página única (`index.html`) com todo o CSS e JavaScript embutidos
(`<style>`/`<script>` inline). Os textos e listas de projetos/sistemas ficam
em `data/projects.json` e `data/systems.json`, carregados via `fetch()` — é
isso que permite editar o conteúdo pelo painel admin sem mexer no HTML. As
fotos e capturas de tela ficam como arquivos externos na pasta `assets/`.

Tema visual "terminal / dual-boot" (dark mode, verde/azul), usado como
linguagem visual. O conteúdo é sobre a atuação como professor de História e
os projetos pedagógicos e sistemas desenvolvidos para a escola.

## Site publicado (GitHub Pages)

`https://zandrafir.github.io/portfolio-thiago-ribeiro/`

Todo push para a branch `main` atualiza o site publicado automaticamente
(pode levar 1–2 minutos para propagar).

## Painel admin — criar projetos e adicionar fotos de qualquer aparelho

Acesse `https://zandrafir.github.io/portfolio-thiago-ribeiro/admin.html`.

Esse painel edita o repositório do GitHub diretamente pelo navegador — sem
precisar de servidor, sem precisar me acionar. Para usar:

1. Gere um **token de acesso pessoal (fine-grained)** em
   [github.com/settings/personal-access-tokens/new](https://github.com/settings/personal-access-tokens/new):
   - **Repository access** → *Only select repositories* → escolha
     `portfolio-thiago-ribeiro`.
   - **Permissions → Repository permissions** → `Contents` → **Read and write**.
   - Gere e copie o token (começa com `github_pat_...`).
2. Abra o admin, cole o token e clique em **Conectar**.
3. O token fica salvo só no navegador daquele aparelho (`localStorage`) — não
   passa por nenhum servidor além do próprio GitHub. Em outro celular/computador,
   basta gerar/colar o token de novo.

No painel dá para:

- Criar, editar e excluir **projetos pedagógicos** (título, descrição curta e
  completa, badges/rótulos, fotos).
- Enviar fotos direto do celular ou computador — a imagem é redimensionada no
  próprio navegador antes de subir, então funciona bem mesmo com fotos grandes
  de celular.
- Criar, editar e excluir **sistemas para a escola** (descrição, badges,
  captura de tela, links de acesso/GitHub).

Cada ação (salvar, criar, enviar foto) gera um commit no repositório — dá
para ver o histórico completo em
`https://github.com/Zandrafir/portfolio-thiago-ribeiro/commits/main`.

⚠️ O arquivo `admin.html` não tem senha própria além do token do GitHub — ele
está público (é um site estático), mas só quem tiver um token válido com
permissão de escrita no repositório consegue de fato alterar algo. Trate o
token como uma senha: não compartilhe, e se desconfiar que vazou, revogue em
[github.com/settings/tokens](https://github.com/settings/tokens) e gere outro.

## Como visualizar localmente

Como o site agora carrega `data/*.json` via `fetch()`, abrir `index.html`
direto com duplo clique (`file://`) não funciona — o navegador bloqueia
`fetch` de arquivos locais. Para testar localmente, rode um servidor simples
dentro da pasta:

```
python3 -m http.server 8000
```

e acesse `http://localhost:8000/`.

## Estrutura

```
portfolio-site/
├── index.html                  # site completo (HTML + CSS + JS inline)
├── admin.html                  # painel admin (CMS via GitHub Contents API)
├── data/
│   ├── projects.json            # projetos pedagógicos (editável pelo admin)
│   └── systems.json             # sistemas para a escola (editável pelo admin)
├── assets/
│   ├── gallery/                 # fotos dos projetos pedagógicos
│   │   ├── analise-leis/
│   │   ├── escape-room-revolucao/
│   │   ├── festa-junina/
│   │   ├── folclore/
│   │   ├── folclore-apresentacao/
│   │   ├── lumen-rpg/
│   │   ├── micro-rpg-napoleonico/
│   │   ├── tutoria-coletiva/
│   │   └── vozes-femininas/
│   ├── systems/                 # capturas de tela dos sistemas (S.I.I.F., Eletivas, Radar, EphimCoins)
│   └── education/                # capas antigas (mantidas como referência/backup)
└── README.md
```

Rostos de alunos nas fotos foram borrados (pixelizados) por privacidade —
apenas rostos de pessoas reais, sem alterar cartazes, desenhos ou ilustrações
produzidos pelos alunos.

## Seções do site

- **Sobre mim**: trajetória (Ensino Médio 1º/2º → Ensino Fundamental 8º/9º)
  dentro do ano letivo de 2026, a combinação entre humanidades, educação e
  tecnologia, e o enquadramento no Programa Ensino Integral.
- **Projetos na Educação**: projetos pedagógicos, cada um com descrição
  completa e galeria com todas as fotos (clique para abrir a foto em tela
  cheia, use as setas do teclado para navegar).
- **Sistemas para a Escola**: sistemas desenvolvidos para apoiar o dia a dia
  da escola.

Não há seção de contato, por opção do autor.

## Personalização manual (sem usar o admin)

- **Textos/projetos/sistemas**: edite diretamente `data/projects.json` e
  `data/systems.json` — cada objeto tem `id`/`title`, `badges`, `short`,
  `full` (ou `desc`), e `photos` (array de caminhos relativos dentro de
  `assets/gallery/`) ou `links`.
- **Fotos de um projeto já existente**: adicione o arquivo em
  `assets/gallery/<slug>/` e inclua o caminho relativo (ex.:
  `"minha-pasta/05.jpg"`) no array `photos` do projeto em
  `data/projects.json`.
- **Cores/tema**: variáveis no topo do bloco `<style>` de `index.html`
  (`:root { --accent, --bg, ... }`).

## Publicação

O site é publicado via **GitHub Pages** a partir da branch `main` (raiz do
repositório). Por ser HTML + CSS + JS puro (sem build step), também pode ser
publicado em qualquer outro serviço estático (Vercel, Netlify, Cloudflare
Pages) apontando para a mesma pasta.
