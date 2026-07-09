# Tabuleiro Final 🔴⚫

Jogo de perguntas e respostas em formato de game show, com tabuleiro de 6 categorias e
5 níveis de pontuação (100 a 500). Feito em React + Vite, com um painel de administração
simples para quem não é da área técnica.

## Estrutura de pastas

```
jeopardy-game/
├── index.html
├── package.json
├── vite.config.js
├── public/
│   └── board-icon.svg
└── src/
    ├── main.jsx                  # ponto de entrada do React
    ├── App.jsx                   # estado geral do jogo e navegação entre telas
    ├── App.module.css
    ├── styles/
    │   └── tokens.css            # paleta de cores, tipografia e reset global
    ├── data/
    │   └── defaultGameData.js    # conteúdo de exemplo (6 categorias x 5 perguntas)
    ├── utils/
    │   ├── youtube.js            # conversão de links do YouTube para embed
    │   ├── storage.js            # leitura/escrita no navegador (localStorage)
    │   └── backup.js             # exportar/importar backup em .json
    └── components/
        ├── StartScreen.jsx       # tela inicial
        ├── GameBoard.jsx         # tabuleiro (6 colunas x 5 linhas)
        ├── QuestionCell.jsx      # cada célula/botão do tabuleiro
        ├── QuestionModal.jsx     # tela da pergunta durante o jogo
        ├── MediaRenderer.jsx     # exibe imagem e/ou vídeo do YouTube
        ├── ScoreBoard.jsx        # placar dos times
        ├── RulesModal.jsx        # regras do jogo
        ├── Toast.jsx             # mensagens de confirmação
        ├── AdminPanel.jsx        # painel do administrador (abas e ações gerais)
        ├── AdminStepGameInfo.jsx     # etapa 1: nome do jogo
        ├── AdminStepTeams.jsx        # etapa 2: times
        ├── AdminStepQuestions.jsx    # etapa 3: categorias e perguntas
        ├── AdminStepReview.jsx       # etapa 4: revisão + backup
        ├── AdminPreviewModal.jsx     # pré-visualização de uma pergunta
        └── AdminForm.module.css      # estilos compartilhados dos formulários
```

## Como rodar localmente

Pré-requisito: ter o [Node.js](https://nodejs.org) instalado (versão 18 ou mais recente).

```bash
# 1. entre na pasta do projeto
cd jeopardy-game

# 2. instale as dependências (só precisa fazer isso uma vez)
npm install

# 3. rode o projeto em modo de desenvolvimento
npm run dev
```

O terminal vai mostrar um endereço parecido com `http://localhost:5173`. Abra esse
endereço no navegador para ver o jogo.

Para gerar uma versão otimizada, pronta para publicar:

```bash
npm run build
```

Isso cria uma pasta `dist/` com os arquivos finais do site.

## Como personalizar o jogo pela interface

Você **não precisa mexer em nenhum arquivo de código** para personalizar o jogo.

1. Na tela inicial, clique em **"Personalizar jogo"** (ou acesse a rota `/admin`).
2. **Etapa 1 — Informações do jogo:** defina o nome do jogo e o subtítulo.
3. **Etapa 2 — Times:** edite o nome de cada time, adicione ou remova times (mínimo de 2).
4. **Etapa 3 — Categorias e perguntas:** escolha uma categoria nas abas, edite seu nome, e
   preencha o texto da pergunta e da resposta de cada um dos 5 valores (100 a 500). Use o
   botão **"Pré-visualizar pergunta"** para ver exatamente como ela vai aparecer durante o jogo.
5. **Etapa 4 — Revisar e jogar:** confira um resumo de tudo o que foi preenchido e, se quiser,
   baixe ou carregue um backup do jogo.
6. Clique em **"Salvar alterações"** para confirmar tudo.
7. Clique em **"Voltar ao jogo"** e depois em **"Começar jogo"**.

Tudo o que é salvo fica guardado automaticamente no navegador — se você fechar a aba e abrir
de novo, o conteúdo personalizado continua lá.

Outras ações disponíveis no rodapé do painel:
- **Resetar apenas a partida:** zera a pontuação dos times e libera todas as perguntas de novo,
  sem apagar o conteúdo que você personalizou.
- **Restaurar exemplo inicial:** apaga tudo e volta para o conteúdo de exemplo que vem pronto
  com o jogo.

## Como adicionar imagens

No campo **"Link da imagem"** de cada pergunta, cole o endereço de uma imagem publicada na
internet (por exemplo, um link que termine em `.jpg`, `.png` ou `.webp`). A imagem vai
aparecer automaticamente dentro da tela da pergunta. Se o campo ficar em branco, nenhum
espaço vazio é exibido.

## Como adicionar vídeos do YouTube

No campo **"Link do vídeo do YouTube"**, cole o link normal do vídeo, exatamente como você
copia do navegador ou do celular. Os formatos abaixo funcionam automaticamente:

- `https://www.youtube.com/watch?v=XXXXXXXXXXX`
- `https://youtu.be/XXXXXXXXXXX`

O sistema identifica o vídeo e o exibe dentro de um player, já pronto para tocar quando a
pergunta for aberta. Se o link não for reconhecido, um aviso aparece no painel admin para
você conferir o endereço.

## Como baixar e carregar backup

Na etapa 4 do painel admin ("Revisar e jogar"):

- **Baixar backup:** gera um arquivo com todo o conteúdo do jogo (nome, times, categorias,
  perguntas, respostas, imagens e vídeos). Guarde esse arquivo em um lugar seguro.
- **Carregar backup:** escolha um arquivo de backup baixado anteriormente para trazer todo
  aquele conteúdo de volta — útil para abrir o mesmo jogo em outro computador.

## Como publicar online

### Vercel
1. Crie uma conta em [vercel.com](https://vercel.com) e instale a CLI (opcional) ou use o site.
2. Suba a pasta do projeto para um repositório no GitHub.
3. No painel da Vercel, clique em "Add New Project", escolha o repositório e mantenha as
   configurações padrão (a Vercel detecta automaticamente que é um projeto Vite).
4. Clique em "Deploy". Em poucos minutos, você recebe um link público do jogo.

### Netlify
1. Crie uma conta em [netlify.com](https://netlify.com).
2. Rode `npm run build` localmente para gerar a pasta `dist/`.
3. Na Netlify, arraste a pasta `dist/` para a área de deploy manual (ou conecte o repositório
   do GitHub e configure o comando de build como `npm run build` e a pasta de saída como `dist`).
4. Após a publicação, você recebe um link público para acessar o jogo de qualquer lugar.

> Dica: como o conteúdo é salvo no navegador de cada pessoa, cada apresentador que abrir o
> jogo publicado terá sua própria versão personalizada, guardada localmente. Para compartilhar
> o mesmo conteúdo entre computadores diferentes, use o backup.

## Sugestões simples de melhorias futuras

- Adicionar um cronômetro visível durante cada pergunta.
- Permitir efeitos sonoros ao acertar ou errar.
- Criar um modo "só apresentador" com a resposta sempre visível numa segunda tela.
- Permitir arrastar e soltar para reordenar categorias.
- Adicionar suporte a mais de um tabuleiro (rodada dupla, por exemplo).
