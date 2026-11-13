# Controle TV — descoberta automática

Interface web em **uma tela** para Samsung Tizen e LG webOS compatíveis. O visitante **não informa IP nem marca**: a ponte local procura aparelhos automaticamente. Se houver mais de uma TV, aparece o seletor.

## Vercel

Envie `index.html`, `style.css`, `src.js` e `vercel.json` à raiz do repositório. Selecione **Other**, sem build e sem output customizado. O ZIP é estático e não executa funções de servidor na Vercel.

## Controlar TVs de verdade (limitação importante)

**Estar na mesma rede Wi-Fi não basta para um site da Vercel descobrir a televisão.** O navegador impede a varredura automática da LAN. Por isso é preciso executar **uma ponte Node.js no computador da mesma rede**. No computador, instale Node.js 18+, abra a pasta `bridge` e execute:

```bash
npm install
npm start
```

Então acesse `http://127.0.0.1:8765` **no mesmo computador**. A ponte serve o painel localmente e realiza a descoberta SSDP; caso o multicast não funcione, tenta identificar TVs Samsung na sub-rede /24. Para acessar a interface hospedada na Vercel a partir desse computador, defina `ALLOWED_ORIGIN=https://SEU-PROJETO.vercel.app` ao iniciar a ponte. O sistema **não oferece uso direto pelo celular em toda rede**: para isso seria necessária outra solução de ponte autenticada e acessível ao celular. Não expor a ponte sem autenticação à rede nem à internet.

A busca só identifica **Samsung e LG compatíveis**. Para algumas TVs, autorize o pareamento no aparelho. O sucesso depende de modelo, configurações da TV, firewall e rede; ligar uma TV totalmente desligada nem sempre é possível. A implementação não foi testada com uma TV física.

## Segurança

A ponte escuta apenas `127.0.0.1`; não a publique na Vercel ou em um endereço público. Antes de usar o painel da Vercel, configure a origem permitida conforme descrito acima. Nenhum comando é simulado: se a conexão falhar o painel exibirá erro.
