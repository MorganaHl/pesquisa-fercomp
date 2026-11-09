# Pesquisa de Clientes Fercomp — Passo a passo (para leigos)

Este guia liga a pesquisa a uma planilha do Google (tudo **gratuito**). Leva uns
**15 minutos**. Faça na ordem. Se der erro, veja a seção **9. Se der problema**.

Arquivos deste projeto:

- `index.html` — a **pesquisa** que o cliente responde pelo link do WhatsApp.
- `painel.html` — o **painel** da equipe, com senha, para analisar as respostas.
- `config.js` — o **único** arquivo que você edita (link do servidor, senha e links).
- `apps-script/Code.gs` — o **backend** que grava tudo na planilha Google.
- `logo.png` — (opcional) coloque o logo da Fercomp com este nome na pasta.
  Se não colocar, aparece o texto "FERCOMP" em laranja.

> 💡 **Dica:** antes de publicar, abra `painel.html?demo=1` no navegador para ver o
> painel funcionando com 60 respostas fictícias. Nada é gravado; é só demonstração.

---

## 1. Criar a planilha no Google Sheets

1. Entre em <https://sheets.google.com> com a conta Google da Fercomp.
2. Clique em **+ Em branco** para criar uma planilha nova.
3. No topo, onde está escrito "Planilha sem título", troque por: **Pesquisa Fercomp**.
4. Não precisa criar colunas nem abas — o sistema cria sozinho a aba `Respostas`
   com o cabeçalho na primeira resposta.

---

## 2. Colar o código do backend (Apps Script)

1. Com a planilha aberta, vá no menu **Extensões → Apps Script**.
   Abre uma nova aba do navegador com um editor de código.
2. Apague qualquer texto que estiver na caixa (geralmente `function myFunction() {}`).
3. Abra o arquivo `apps-script/Code.gs` deste projeto, **copie tudo** e **cole** na caixa.
4. Clique no ícone de **disquete (Salvar)** ou aperte `Ctrl + S`.
5. Se pedir para dar um nome ao projeto, escreva **Pesquisa Fercomp** e salve.

---

## 3. Definir a senha do painel

Essa senha protege o painel e os dados. A equipe vai usá-la para entrar.

1. Ainda no Apps Script, clique na engrenagem **⚙ Configurações do projeto**
   (ícone na barra da esquerda).
2. Role até **Propriedades do script** e clique em **Adicionar propriedade do script**.
3. Preencha:
   - **Propriedade:** `PAINEL_CHAVE`
   - **Valor:** a senha que você quiser (ex.: `fercomp2026`). Evite senha óbvia.
4. Clique em **Salvar propriedades do script**.

> ⚠️ Guarde essa senha. Ela precisa ser **idêntica** à que você vai colocar no `config.js`.

---

## 4. Implantar como App da Web e copiar a URL

1. No Apps Script, clique no botão azul **Implantar → Nova implantação**.
2. Clique na engrenagem ao lado de "Selecionar tipo" e escolha **App da Web**.
3. Preencha:
   - **Descrição:** Pesquisa (ou qualquer texto).
   - **Executar como:** **Eu** (sua conta).
   - **Quem tem acesso:** **Qualquer pessoa**.
4. Clique em **Implantar**.
5. Vai aparecer um aviso de autorização. Clique em **Autorizar acesso**, escolha a
   conta Google, e se aparecer "O Google não verificou este app", clique em
   **Avançado → Acessar Pesquisa Fercomp (não seguro)** e depois **Permitir**.
   (É seguro — o app é seu.)
6. Copie a **URL do app da Web** que aparece. Ela termina com `/exec`. Exemplo:
   `https://script.google.com/macros/s/AKfy....../exec`

> 🔁 **Toda vez que você mudar o `Code.gs` depois**, precisa fazer
> **Implantar → Gerenciar implantações → (lápis de editar) → Versão: Nova versão → Implantar**,
> senão a mudança não vale. A URL continua a mesma.

---

## 5. Colar a URL e os links no `config.js`

1. Abra o arquivo `config.js` num editor de texto (Bloco de Notas serve).
2. Troque os valores entre aspas:
   - `APPS_SCRIPT_URL`: cole a URL que termina em `/exec` (passo 4).
   - `PAINEL_CHAVE`: a **mesma** senha do passo 3.
   - `PLANILHA_URL`: o endereço normal da sua planilha (copie da barra do navegador).
   - `WHATSAPP_URL`: o link da bio/WhatsApp da Fercomp (já vem preenchido).
3. Salve o arquivo (mantendo o nome `config.js`).

---

## 6. Publicar a pasta na internet (grátis)

Escolha **uma** das duas opções.

### Opção A — Netlify Drop (mais fácil, arrastar e soltar)

1. Entre em <https://app.netlify.com/drop>.
2. **Arraste a pasta inteira** `pesquisa-fercomp` para a área indicada na tela.
3. Em segundos aparece um endereço tipo `https://nome-aleatorio.netlify.app`.
4. Pronto. Esse é o seu site. (Pode criar conta grátis para guardar o endereço.)

### Opção B — GitHub Pages

1. Crie uma conta em <https://github.com> (grátis).
2. Crie um repositório novo (**New repository**), por exemplo `pesquisa-fercomp`.
3. Envie (upload) todos os arquivos da pasta.
4. Vá em **Settings → Pages**, em "Branch" escolha `main` e `/root`, clique **Save**.
5. Em alguns minutos o site fica no ar em
   `https://SEU-USUARIO.github.io/pesquisa-fercomp/`.

---

## 7. Montar os links para o WhatsApp

Use o endereço do seu site (do passo 6) e acrescente a origem e o vendedor.
Assim você sabe de onde veio cada resposta e quem enviou:

- WhatsApp do Nathan:
  `https://SEU-SITE/index.html?origem=whatsapp&vendedor=nathan`
- WhatsApp da Andreza:
  `https://SEU-SITE/index.html?origem=whatsapp&vendedor=andreza`
- Instagram (sem vendedor):
  `https://SEU-SITE/index.html?origem=instagram`

Vendedores sugeridos: `nathan`, `andreza`, `andrielly`, `hugo`, `lays`, `layane`.
O `origem` pode ser `whatsapp`, `instagram`, `balcao` etc.

O painel da equipe fica em: `https://SEU-SITE/painel.html`

---

## 8. Testar antes de enviar para os clientes

1. Abra o link `index.html?origem=whatsapp&vendedor=nathan` no **seu celular**.
2. Responda a pesquisa até o fim e toque em **Enviar respostas**.
3. Abra a planilha Google: deve aparecer uma linha nova na aba `Respostas`.
4. Abra `painel.html`, digite a senha e veja a resposta aparecer nos números.
5. Deu certo? Pode mandar os links para os clientes. 🎉

---

## 9. Se der problema

- **"Senha incorreta" no painel:** a senha do `config.js` tem que ser idêntica à
  `PAINEL_CHAVE` do Apps Script (maiúsculas/minúsculas contam). Confira os dois.
- **A resposta não aparece na planilha:** confirme que você **implantou** (passo 4) e
  que a `APPS_SCRIPT_URL` no `config.js` termina em `/exec`.
- **Mudei o `Code.gs` e parou de funcionar:** você precisa criar uma **Nova versão**
  em *Gerenciar implantações* (veja o aviso no fim do passo 4).
- **O painel diz "Erro de conexão":** verifique a internet e se a URL está certa.
- **Quero ver o painel sem ter respostas ainda:** abra `painel.html?demo=1`.
- **O logo não aparece:** coloque um arquivo chamado exatamente `logo.png` na pasta,
  ou ignore — o nome "FERCOMP" aparece no lugar.

---

## 10. Mensagem sugerida para o WhatsApp

> Olá! Aqui é a *Fercomp* 👋
> Estamos fazendo uma pesquisa rápida (uns 5 minutinhos) para melhorar nosso
> atendimento e as condições para você. Sua opinião vale muito pra gente!
> Responda por aqui 👉 https://SEU-SITE/index.html?origem=whatsapp&vendedor=nathan
> Obrigado! 🙏

Troque o link pelo do vendedor que está enviando.
