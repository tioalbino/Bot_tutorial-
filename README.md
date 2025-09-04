Perfeito! Transformei todo o seu conteúdo em Markdown puro, sem repetições, sem HTML, mantendo a mesma pegada didática e direta para copiar e rodar. Aqui está o resultado:

# 🤖 Bot WhatsApp com Baileys

Exemplo de bot do WhatsApp usando [@whiskeysockets/baileys](https://www.npmjs.com/package/@whiskeysockets/baileys) em Node.js.  
Tudo em um único arquivo, pronto para copiar e rodar direto.

---

## 📲 Contato do Desenvolvedor

- [💬 WhatsApp](https://wa.me/5527998158753)  
- Número: +55 27 99815-8753

---

## 🖼️ Demonstração

QR Code animado para escanear pelo WhatsApp:

![QR Code Animado](https://media.giphy.com/media/3oEjI6SIIHBdRxXI40/giphy.gif)

Exemplo do Bot:

![Exemplo do Bot](https://via.placeholder.com/400x200.png?text=Bot+WhatsApp)

---

## 📦 Instalação

```bash
npm install @whiskeysockets/baileys qrcode-terminal

Tudo roda direto, sem pastas extras.


---

🔧 Conexão de Exemplo

import makeWASocket, { useMultiFileAuthState } from '@whiskeysockets/baileys';
import qrcode from 'qrcode-terminal';

async function connectToWhatsApp() {
  const { state, saveCreds } = await useMultiFileAuthState('.auth_info');
  const sock = makeWASocket({ auth: state });

  sock.ev.on('connection.update', ({ qr, connection }) => {
    if (qr) qrcode.generate(qr, { small: true });
    if (connection === 'open') console.log('✅ Bot conectado ao WhatsApp!');
    if (connection === 'close') console.log('❌ Conexão encerrada, tentando reconectar...');
  });

  sock.ev.on('creds.update', saveCreds);

  sock.ev.on('messages.upsert', ({ messages, type }) => {
    if (type === 'notify') {
      messages.forEach(msg => {
        if (!msg.key.fromMe) {
          console.log(`📩 Mensagem recebida de ${msg.key.remoteJid}: ${msg.message?.conversation}`);
        }
      });
    }
  });
}

connectToWhatsApp();

> Escaneie o QR Code exibido no terminal → Bot conectado ✅




---

📝 Explicação do Código

Parte	Função

useMultiFileAuthState('.auth_info')	Cria sessão do WhatsApp sem pastas extras
makeWASocket({ auth: state })	Inicializa o bot com WhatsApp Web
sock.ev.on('connection.update', …)	Monitora QR Code e conexão aberta/fechada
qrcode.generate(qr, { small: true })	Mostra QR Code no terminal
sock.ev.on('creds.update', saveCreds)	Salva credenciais automaticamente
sock.ev.on('messages.upsert', …)	Recebe mensagens do WhatsApp


> Esse código já deixa o bot pronto para enviar/receber mensagens futuramente.




---

📦 Dependências

@whiskeysockets/baileys → Conexão com WhatsApp Web

qrcode-terminal → Exibe QR Code no terminal


Instale com:

npm install @whiskeysockets/baileys qrcode-terminal


---

⚠️ Avisos

Use apenas para estudos/testes

Nunca compartilhe a pasta .auth_info

Respeite os Termos de Serviço do WhatsApp



---

💡 Próximos Passos

Adicionar respostas automáticas

Criar comandos customizados

Salvar logs e estatísticas de mensagens

Implementar envio de mídia e imagens

