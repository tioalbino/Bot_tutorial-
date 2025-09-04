
<h1>🤖 Bot WhatsApp com Baileys</h1>
<p>Exemplo de bot do WhatsApp usando <a href="https://www.npmjs.com/package/@whiskeysockets/baileys" target="_blank">@whiskeysockets/baileys</a> em Node.js. Tudo em um único arquivo, pronto para copiar e rodar direto.</p>

<section>
<h2>📲 Contato do Desenvolvedor</h2>
<a href="https://wa.me/5527998158753" class="badge whatsapp">💬 WhatsApp</a>
<a href="#" class="badge copy">📋 Copiar Número</a>
<p>Número: +55 27 99815-8753</p>
</section>

<section>
<h2>🖼️ Demonstração</h2>
<img src="https://media.giphy.com/media/3oEjI6SIIHBdRxXI40/giphy.gif" alt="QR Code Animado">
<p>Exemplo de QR Code para escanear pelo WhatsApp</p>
<img src="https://via.placeholder.com/400x200.png?text=Bot+WhatsApp" alt="Exemplo do Bot">
</section>

<section>
<h2>📦 Instalação</h2>
<pre><code>npm install @whiskeysockets/baileys qrcode-terminal</code></pre>
<p>Tudo roda direto, sem pastas extras.</p>
</section>

<section>
<h2>Conexão de Exemplo</h2>
<pre><code>import makeWASocket, { useMultiFileAuthState } from '@whiskeysockets/baileys';
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

connectToWhatsApp();</code></pre>
</section>

<section>
<h2>📝 Explicação do Código</h2>
<table>
<tr><th>Parte</th><th>Função</th></tr>
<tr><td>useMultiFileAuthState('.auth_info')</td><td>Cria sessão do WhatsApp dentro do próprio arquivo, sem pastas extras</td></tr>
<tr><td>makeWASocket({ auth: state })</td><td>Inicializa o bot com WhatsApp Web</td></tr>
<tr><td>sock.ev.on('connection.update', …)</td><td>Monitora QR Code, conexão aberta/fechada</td></tr>
<tr><td>qrcode.generate(qr, { small: true })</td><td>Mostra QR Code no terminal</td></tr>
<tr><td>sock.ev.on('creds.update', saveCreds)</td><td>Salva credenciais automaticamente</td></tr>
<tr><td>sock.ev.on('messages.upsert', …)</td><td>Recebe mensagens do WhatsApp</td></tr>
</table>
</section>



<section>
<h2>📦 Dependências</h2>
<ul>
<li>@whiskeysockets/baileys → conexão com WhatsApp Web</li>
<li>qrcode-terminal → exibe QR Code no terminal</li>
</ul>
<pre><code>npm install @whiskeysockets/baileys qrcode-terminal</code></pre>
</section>

<section>
<h2>⚠️ Avisos</h2>
<ul>
<li>Use apenas para estudos/testes</li>
<li>Nunca compartilhe o QR Code ou credenciais</li>
<li>Respeite os Termos de Serviço do WhatsApp</li>
</ul>
</section>

<section>
<h2>💡 Próximos Passos</h2>
<ul>
<li>Adicionar respostas automáticas</li>
<li>Criar comandos customizados</li>
<li>Salvar logs e estatísticas de mensagens</li>
<li>Implementar envio de mídia e imagens</li>
</ul>
</section>

</body>
</html>import qrcode from 'qrcode-terminal';

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


