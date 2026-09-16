# Método Aprovado — Ferramentas com IA

Este pacote tem tudo pronto: o site (`public/index.html`) e um servidor pequeno
(`server.js`) que guarda sua chave da API da Anthropic em segredo e faz as
chamadas de IA por trás dos panos. É esse servidor que resolve o erro que
acontecia ao abrir o HTML sozinho no navegador.

## 1. Pegue sua chave da API da Anthropic

1. Crie uma conta em https://console.anthropic.com
2. Vá em **API Keys** e gere uma nova chave (começa com `sk-ant-...`)
3. Guarde essa chave — ela é secreta, nunca coloque ela dentro do HTML

## 2. Rodar localmente (para testar antes de vender)

Você precisa ter o [Node.js](https://nodejs.org) instalado (versão 18 ou mais nova).

```bash
cd metodo-aprovado-backend
npm install
cp .env.example .env
```

Abra o arquivo `.env` e cole sua chave:

```
ANTHROPIC_API_KEY=sk-ant-sua-chave-aqui
```

Depois rode:

```bash
npm start
```

Abra `http://localhost:3000` no navegador — as três ferramentas (redação,
questões, cronograma) devem funcionar normalmente.

## 3. Colocar no ar de verdade (para vender)

A forma mais simples e gratuita para começar é o **Render.com**:

1. Crie uma conta em https://render.com
2. Clique em **New +** → **Web Service**
3. Envie esta pasta (ou suba num repositório do GitHub e conecte)
4. Configure:
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Em **Environment Variables**, adicione:
   - `ANTHROPIC_API_KEY` = sua chave
6. Clique em **Deploy**

O Render vai te dar uma URL pública (algo como
`https://metodo-aprovado.onrender.com`) — é esse link que você usa como
"área do aluno" depois que a pessoa comprar pela Kiwify.

Alternativas que também funcionam do mesmo jeito: **Railway**, **Vercel**
(usando Serverless Functions) ou uma VPS própria.

## Sobre custo

Cada chamada de IA (correção de redação, questão gerada, cronograma) consome
créditos da sua conta na Anthropic, cobrados por uso — não é de graça por
aluno. Vale a pena acompanhar o consumo no painel da Anthropic
(https://console.anthropic.com) enquanto o número de alunos crescer, para
ajustar o preço da sua ferramenta de acordo com esse custo.

## Segurança

- A chave da API fica só no servidor (variável de ambiente), nunca no HTML
  público — por isso ninguém consegue roubar sua chave olhando o código da
  página.
- Se quiser, dá pra adicionar um limite de uso por aluno mais na frente
  (ex: X correções de redação por mês) para controlar custo — isso exigiria
  um sistema de login, que não está incluído neste pacote.
