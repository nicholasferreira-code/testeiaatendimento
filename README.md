# Simulador — Atendimento Tibii's Mania

Chat que simula o agente de IA da Tibii's Mania (mesmo prompt mestre configurado na Clint),
rodando com a API gratuita do Google Gemini. Funciona em qualquer navegador, sem precisar
de conta Claude.

## 1. Pegar uma API key gratuita do Gemini

1. Acesse https://aistudio.google.com/apikey
2. Faça login com uma conta Google
3. Clique em "Create API key"
4. Copie a chave gerada (começa com `AIza...`)

O tier gratuito do Gemini (`gemini-2.0-flash`) tem limite generoso de requisições por
minuto/dia — suficiente para testes. Sem cartão de crédito necessário.

## 2. Deploy no Vercel

### Opção A — pelo site (sem usar terminal)
1. Acesse https://vercel.com e crie uma conta (pode ser com GitHub, Google, etc.)
2. No dashboard, clique em **"Add New" → "Project"**
3. Escolha **"Deploy without Git"** ou arraste esta pasta inteira (se a opção de upload
   direto estiver disponível), OU suba esta pasta para um repositório no GitHub e importe
   esse repositório no Vercel (mais comum e recomendado)
4. Antes de finalizar o deploy, vá em **Settings → Environment Variables** e adicione:
   - Nome: `GEMINI_API_KEY`
   - Valor: a chave que você copiou no passo 1
5. Clique em **Deploy**

### Opção B — pelo terminal (se tiver Node instalado)
```bash
npm install -g vercel
cd tibii-mania-simulador   # pasta deste projeto
vercel login
vercel
# na primeira pergunta, aceite criar um novo projeto
vercel env add GEMINI_API_KEY
# cole a chave quando pedir
vercel --prod
```

Ao final, o Vercel te dá uma URL tipo `https://tibii-mania-simulador.vercel.app` —
esse é o link para compartilhar com quem for testar. Funciona em qualquer navegador,
sem precisar estar logado em nada.

## Estrutura do projeto
- `index.html` — a interface de chat
- `api/chat.js` — função serverless que recebe as mensagens e chama o Gemini com o
  prompt mestre da Tibii's Mania embutido
- A chave de API nunca fica exposta no front-end — ela só existe no servidor (Vercel),
  como variável de ambiente

## Importante
- O limite gratuito do Gemini é por projeto/conta Google, então se muita gente testar ao
  mesmo tempo pode bater o limite — nesse caso o simulador mostra uma mensagem de erro
  pedindo para tentar de novo em instantes.
- Se quiser trocar o modelo (ex: `gemini-1.5-flash`), basta editar a URL dentro de
  `api/chat.js`.
