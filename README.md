🤖 Bot WhatsApp com Baileys

Este projeto mostra como criar uma conexão completa com WhatsApp usando @whiskeysockets/baileys em Node.js.

Perfeito para estudos, tutoriais ou testes no Termux, Linux ou Windows.


---

📲 Contato do Desenvolvedor


 (clique com botão direito → copiar)

Número: +55 27 99815-8753


---

🖼️ Demonstração


Exemplo de QR Code para escanear pelo WhatsApp




---

📦 Instalação

No terminal, instale as dependências:

npm install @whiskeysockets/baileys qrcode-terminal


---

▶️ Rodar o Bot Diretamente

Execute direto sem criar arquivos:

node -e "
import makeWASocket, { useMultiFileAuthState } from '@whiskeysockets/baileys';
import qrcode from 'qrcode-terminal';

(async () => {
  const { state, saveCreds } = await useMultiFileAuthState('.auth_info');
  const sock = makeWASocket({ auth: state });

  sock.ev.on('connection.update', ({ qr, connection }) => {
    if (qr) qrcode.generate(qr, { small: true });
    if (connection === 'open') console.log('✅ Bot conectado ao WhatsApp!');
    if (connection === 'close') console.log('❌ Conexão encerrada, tentando reconectar...');
  });

  sock.ev.on('creds.update', saveCreds);
})();
"

> Escaneie o QR Code exibido no terminal → Bot conectado ✅




---

🔗 Código Completo com Explicação

import makeWASocket, { useMultiFileAuthState } from '@whiskeysockets/baileys';
import qrcode from 'qrcode-terminal';

async function connectToWhatsApp() {
  // 1. Cria o estado de autenticação e salva sessão
  const { state, saveCreds } = await useMultiFileAuthState('.auth_info');
  
  // 2. Inicializa a conexão com WhatsApp Web
  const sock = makeWASocket({ auth: state });

  // 3. Monitora atualizações de conexão
  sock.ev.on('connection.update', ({ qr, connection }) => {
    if (qr) qrcode.generate(qr, { small: true }); // Mostra QR Code
    if (connection === 'open') console.log('✅ Bot conectado ao WhatsApp!');
    if (connection === 'close') console.log('❌ Conexão encerrada, tentando reconectar...');
  });

  // 4. Salva credenciais automaticamente
  sock.ev.on('creds.update', saveCreds);
}

// Executa a função
connectToWhatsApp();

✅ Como funciona:

1. useMultiFileAuthState('.auth_info') → Cria pasta .auth_info para salvar sessão.


2. makeWASocket({ auth: state }) → Inicializa o bot com WhatsApp Web.


3. sock.ev.on('connection.update', …) → Monitora QR Code, conexão aberta/fechada.


4. qrcode.generate(qr, { small: true }) → Mostra QR Code no terminal.


5. sock.ev.on('creds.update', saveCreds) → Atualiza credenciais automaticamente.



> Esse código já deixa o bot pronto para enviar/receber mensagens futuramente.




---

📦 Dependências

@whiskeysockets/baileys → Conexão com WhatsApp Web

qrcode-terminal → Exibe QR Code no terminal


Instale com:

npm install @whiskeysockets/baileys qrcode-terminal


---

⚠️ Avisos

Use apenas para estudos/testes.

Nunca compartilhe a pasta .auth_info.

Respeite os Termos de Serviço do WhatsApp.


