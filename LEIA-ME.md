# Controle de Descarregamento — App

Este pacote contém o app redesenhado, já pronto para funcionar como
**aplicativo instalável** (PWA) e para ser transformado em um **.apk** real.

Arquivos:
- `index.html` — o app (interface, cadastros e relatório em PDF)
- `manifest.json` — identidade do app (nome, ícone, cores) para instalação
- `service-worker.js` — permite o app funcionar **offline**
- `icons/` — ícones do app em PNG

Os dados (produtos, revendas, parceiros, cargas) ficam salvos **no próprio
aparelho** (localStorage), sem precisar de internet ou servidor.

---

## 1. Testar agora, sem instalar nada

Abra o arquivo `index.html` direto no navegador do celular ou computador.
Tudo funciona, exceto o "Instalar app" (que só aparece quando os arquivos
estão publicados em um endereço https://).

---

## 2. Instalar como app no celular (sem virar .apk)

Isso já deixa o app com ícone na tela e tela cheia, sem barra do navegador:

1. Publique a pasta em um endereço https:// gratuito. As opções mais
   simples, sem precisar programar:
   - **Netlify Drop**: https://app.netlify.com/drop — arraste a pasta e
     pronto, gera um link.
   - **GitHub Pages**: suba os arquivos em um repositório e ative o Pages
     nas configurações.
   - **Vercel**: https://vercel.com/new — importar pasta/projeto.
2. Abra o link gerado no Chrome do Android (ou Safari do iPhone).
3. Android: toque no botão **"Instalar"** que aparece no topo do app, ou
   no menu **⋮ → Adicionar à tela inicial**.
   iPhone: toque em **Compartilhar → Adicionar à Tela de Início**.
4. Pronto — o app abre como aplicativo normal, com ícone próprio.

---

## 3. Gerar um arquivo .apk de verdade

Um `.apk` é o instalador do Android. A forma mais simples de gerar um,
sem programar nada, é usando o **PWABuilder** (ferramenta gratuita da
Microsoft, feita exatamente para transformar sites/PWA em apps):

1. Publique a pasta como no passo 2 acima (precisa de um link https://).
2. Acesse **https://www.pwabuilder.com**.
3. Cole o link do seu app e clique em **Start**.
4. O PWABuilder confere o `manifest.json` e o `service-worker.js`
   automaticamente (ambos já estão prontos aqui).
5. Clique em **Package for stores → Android**.
6. Baixe o pacote gerado (vem com o `.apk` pronto para instalar, ou
   `.aab` caso queira publicar na Google Play).
7. Transfira o `.apk` para o celular e instale (o Android pode pedir para
   liberar "instalar de fontes desconhecidas" na primeira vez).

Se quiser publicar na **Google Play Store** oficialmente, o mesmo pacote
`.aab` do PWABuilder serve para o cadastro no Google Play Console
(existe uma taxa única de registro de desenvolvedor, cobrada pelo Google,
não pelo PWABuilder).

---

## Revisão desta versão — bugs corrigidos e botão de limpeza

**Bugs corrigidos:**
- O relatório em PDF ignorava por completo os itens de uma carga cujo
  produto tinha sido excluído do cadastro depois de lançada a carga —
  isso fazia o total de unidades do relatório ficar menor do que o total
  mostrado na tela principal (Cargas). Agora o relatório conta esses itens
  como "Produto excluído", batendo com os totais da tela.
- Nome da empresa, CNPJ, telefone, nomes de revenda/parceiro/produto e
  número da nota fiscal agora são tratados com segurança ao montar o
  relatório em PDF, evitando que caracteres especiais (como `<` ou `&`)
  quebrem a formatação da página impressa.

**Novo: botão de limpeza dos registros**
- Na aba **Empresa**, seção "Zona de risco": botão **"Limpar todos os
  registros de carga"**. Apaga só as cargas lançadas (pede confirmação
  duas vezes); os cadastros de produtos, revendas e parceiros não são
  apagados.

**O que já foi melhorado nas versões anteriores**

**Layout / UX:**
- Identidade visual mais sólida (verde profundo + laranja de destaque),
  ícones em SVG no lugar de emojis, tipografia com mais hierarquia.
- Resumo rápido no topo (nº de cargas, unidades e frete total).
- Cartão de carga agora mostra quantidade e valor do frete direto na
  lista, sem precisar abrir nada.
- Filtro por período (data inicial/final), usado tanto na tela quanto no
  relatório.
- Prévia do total (quantidade e frete) enquanto você monta a carga.
- Confirmação antes de excluir, avisos quando falta cadastrar produto ou
  revenda antes de lançar uma carga, mensagens de "salvo com sucesso".
- Parceiro/ajudante deixou de ser obrigatório (opção "Nenhum").
- Valores em Real formatados corretamente (R$ 1.105,00), lista de cargas
  ordenada da mais recente para a mais antiga.

**Relatório em PDF:**
- Cabeçalho com o período do relatório (ou "todos os registros").
- Caixas de destaque com total de cargas, unidades e frete do período.
- Tabelas com formatação monetária correta e visual mais limpo,
  preparado para impressão (não corta linha no meio ao imprimir).

**Virou app instalável:**
- Manifesto + ícones + funcionamento offline (service worker).
- Botão de instalação nativo quando o navegador permite.
- Pronto para gerar `.apk`/`.aab` pelo PWABuilder, sem precisar programar
  nada em Android/Kotlin/Java.
