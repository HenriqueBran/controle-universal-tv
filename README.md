# Controle TV — versão de uma tela

## O que funciona de verdade

Os botões enviam comandos reais para **Samsung Tizen** (WebSocket 8002) e **LG webOS** (WebSocket 3000/3001), nos modelos que aceitam os respectivos protocolos. É necessário confirmar o pareamento na TV. Nem todas as teclas existem em todos os modelos. Ligar uma TV totalmente desligada pode exigir Wake-on-LAN, que não está implementado.

**A Vercel hospeda apenas a interface.** Por motivos de rede, uma página pública na Vercel não consegue, sozinha, descobrir ou controlar TVs privadas na sua rede. A ponte local resolve isso em um computador com Node.js. Navegadores podem bloquear chamadas HTTPS → localhost ou exigir permissões de rede local. Por isso, **o endereço confiável para controle real é http://127.0.0.1:8765**, no próprio computador com a ponte em execução. No celular, a versão Vercel não controla diretamente por esta arquitetura. Para permitir chamadas de uma origem web específica, pode-se configurar `ALLOWED_ORIGIN=https://seu-projeto.vercel.app` ao iniciar a ponte, mas o navegador pode bloquear chamadas HTTPS para a rede local, e isso não resolve a restrição geral.

## Instalação (Windows, macOS, Linux)

1. Instale Node.js 20 ou 22 LTS no computador ligado ao mesmo Wi-Fi da TV.
2. Extraia o ZIP completo. Abra o terminal na pasta `bridge`.
3. Execute `npm install` e depois `npm start`.
4. No **mesmo computador**, abra `http://127.0.0.1:8765`.
5. Clique na engrenagem, informe marca, IP e nome da TV, salve e aceite o pedido na TV.
6. Pressione os botões. O sistema não tem modo de simulação.

Para descobrir o IP, abra as configurações de rede da TV. Prefira reservar o IP no roteador. Samsung: habilite aceitar controle remoto por dispositivos na TV. LG: confirme o diálogo de pareamento.

## Vercel

Os arquivos `index.html`, `style.css`, `src.js` e `vercel.json` devem ficar **na raiz do GitHub**. O projeto deve utilizar `Framework Preset: Other` e sem build nem output customizados. O `vercel.json` usa `@vercel/static` explicitamente para evitar o erro de ponto de entrada. A pasta `bridge` **não** vira uma função na Vercel.

## Limitações e segurança

- Testado por validações locais de sintaxe e endpoints, mas o pareamento não foi validado em TVs físicas reais.
- A ponte escuta **apenas** `127.0.0.1`, sem expor acesso remoto. Não faça port forwarding da porta 8765.
- O arquivo `bridge/.sessions.json`, criado durante o pareamento, guarda credenciais de TV e está protegido pelo `.gitignore`; **nunca publique esse arquivo**.
- Roku não foi implementado: a documentação atual restringe comandos ECP de plataformas de terceiros.
- Android/Google TV precisa de outra integração e não está implementado nesta versão.
- Em LG, o botão de silenciar aplica mute, em vez de alternar. O Play/Pause envia Play, pois a API do modelo pode não ter toggle.
