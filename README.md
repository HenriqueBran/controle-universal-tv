# Controle Universal TV — Vercel (versão estática corrigida)

Esta versão é **100% estática** (HTML/CSS/JS). Não usa Node.js, Vite, funções serverless, `npm install`, nem `npm run build` no deploy. Não depende de APIs da Vercel para carregar.

## IMPORTANTE: substituir todos os arquivos antigos

No repositório do GitHub, na **mesma branch configurada como produção pela Vercel**:

1. **Exclua os arquivos antigos do repositório**, incluindo `package.json`, `package-lock.json`, `pacote (1).json`, `server.js`, `env.example`, `baixar`, pastas `api`, `bridge`, `dist` etc. (se existirem). Essa versão publica somente arquivos estáticos.
2. Adicione os **cinco arquivos da raiz deste ZIP** diretamente na **raiz do repositório**: `index.html`, `src.js`, `style.css`, `vercel.json`, `README.md`. Não envie a pasta que os contém.
3. Faça commit. Confira se a branch de produção está usando esse commit.
4. Na Vercel > Project > Settings > Build and Deployment, escolha **Other**, deixe Build Command desativado/vazio e Output Directory sem substituição. Root Directory `./`.
5. Confira em Settings se não há overrides antigos de Functions, Output ou Build. Faça Redeploy do novo commit **sem cache**.

## Como testar

- O endereço público deve apresentar a interface de controle imediatamente.
- Selecione **Smart TV de demonstração** e experimente os botões: a última ação muda.
- A lista **Minhas TVs** permite cadastrar TVs, mas o cadastro é apenas visual. Nenhuma TV física será controlada sem integração de rede local.

## Limitação importante

A Vercel não tem acesso direto à sua rede Wi-Fi ou à televisão. Esta distribuição foi preparada para publicar e testar **a interface** sem erro 500 de função. Para comandos reais, será necessário adicionar uma ponte local autenticada ou uma integração compatível com a marca, desenvolvida e testada separadamente. Esta distribuição **não inclui** a ponte Node.js das versões anteriores.


## Configuração Vercel – entrada explícita
A versão desta pasta usa `builds` explícitos em `vercel.json` para publicar index.html, src.js e style.css com `@vercel/static`. No projeto Vercel, configure Root Directory `./`, Framework Other; desative Overrides de Build Command e Output Directory. Confirme branch `main` e novo deploy do commit após substituir os cinco arquivos. Para um projeto novo, importe esta raiz sem criar subpasta.
