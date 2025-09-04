Perfeito 😎 então vou montar uma versão final, completa e visual do README, pronta para vídeo tutorial, já em Markdown puro.
Inclui:

Badges/botões clicáveis para WhatsApp e copiar número

Espaço para imagens/GIF

Estrutura limpa para Termux ou Node.js

Exemplo de conexão baseado na documentação oficial do Baileys

Avisos e dependências


Segue pronto:


---

🤖 Bot WhatsApp com Baileys

Este projeto mostra como criar uma conexão simples com WhatsApp usando @whiskeysockets/baileys em Node.js.

Perfeito para estudos, tutoriais ou testes no Termux ou servidores Node.js.


---

📲 Contato do Desenvolvedor


Número: +55 27 99815-8753

 (clique no botão direito → copiar)


---

🖼️ Demonstração / Imagens

> Substitua pelos links reais das suas imagens ou GIFs







---

📑 Sumário

Instalação

Rodar o Bot

Estrutura do Projeto

Exemplo de Conexão

Dependências

Avisos



---

📦 Instalação

1. Instale Node.js (Termux ou servidor Linux/Windows).


2. Crie uma pasta para o projeto e entre nela:



mkdir bot-whatsapp
cd bot-whatsapp

3. Crie o package.json (ou use npm init -y)


4. Instale as dependências:



npm install @whiskeysockets/baileys qrcode-terminal


---

▶️ Rodar o Bot

Crie um arquivo index.js e cole o código de conexão.
Depois rode:

node index.js

O terminal exibirá um QR Code para escanear pelo WhatsApp.


---

📂 Estrutura do Projeto

bot-whatsapp/
├─ index.js        # Conexão principal do bot
├─ package.json    # Dependências e scripts
├─ .auth_info/     # Sessão salva automaticamente
└─ node_modules/   # Pacotes instalados


---

🔗 Exemplo de Conexão (index.js)

import makeWASocket, { useMultiFileAuthState } from '@whiskeysockets/baileys'
import qrcode from 'qrcode-terminal'

async function connectToWhatsApp() {
  const { state, saveCreds } = await useMultiFileAuthState('.auth_info')
  const sock = makeWASocket({ auth: state })

  sock.ev.on('connection.update', ({ qr, connection }) => {
    if (qr) qrcode.generate(qr, { small: true })
    if (connection === 'open') console.log('✅ Bot conectado ao WhatsApp!')
    if (connection === 'close') console.log('❌ Conexão encerrada, tentando reconectar...')
  })

  sock.ev.on('creds.update', saveCreds)
}

connectToWhatsApp()

> Clique no bloco para copiar rapidamente o código.




---

📦 Dependências Principais

@whiskeysockets/baileys → Conexão com WhatsApp Web

qrcode-terminal → Exibe QR Code no terminal


npm install @whiskeysockets/baileys qrcode-terminal


---

⚠️ Avisos

Use apenas para estudos/testes.

Nunca compartilhe a pasta .auth_info (contém sessão do WhatsApp).

Evite violar os Termos de Serviço do WhatsApp.

