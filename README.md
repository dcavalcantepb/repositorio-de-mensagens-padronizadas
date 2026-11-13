# Repositório de Mensagens Padronizadas

Ferramenta para guardar e copiar mensagens padronizadas (e-mails, respostas, avisos etc.) com um clique. Abre em branco: cada pessoa cria as próprias seções e mensagens.

> Status: em uso. Backup manual com download automático ao concluir a edição, e botão de ajuda (?) dentro da página.

## Estrutura

- `index.html`: marcação da página
- `css/style.css`: visual (tokens de cor e tema claro/escuro em `:root`)
- `js/app.js`: lógica (seções, textos, cópia, busca, backup, tema)
- `favicon.*` e `apple-touch-icon.png`: ícone da página (emoji 📋)

Página estática (HTML + CSS + JS puro, sem build).

## Armazenamento

Os dados ficam no `localStorage` do navegador, com chaves próprias (`mensagens-padronizadas:v1` e `mensagens-padronizadas:backup`). Como o `localStorage` é separado por endereço, e não por pasta, as chaves próprias evitam que outro site publicado no mesmo domínio leia ou sobrescreva as mensagens. A chave `tema` é compartilhada de propósito, para a preferência de tema valer em todos os sites.

## Ideia central

- Cada pessoa tem o **próprio conjunto de mensagens**, guardado no navegador dela.
- O **backup** (arquivo JSON) é o meio de transferência: quem chega à equipe importa o backup de um colega e passa a ter o seu próprio conjunto, que pode ajustar e exportar.
- Modelo simples, de propósito. Não há servidor nem login.

## Backup

- Ao clicar em **Concluir edição**, se houve alteração desde o último backup, a página baixa sozinha o arquivo `.json`. Sem alteração, não baixa nada.
- **Exportar backup** gera o arquivo a qualquer momento; **Importar backup** substitui tudo pelo conteúdo do arquivo.
- Uma faixa no rodapé avisa quando há alterações sem backup.
- A página não escolhe a pasta: o navegador salva em Downloads (ou pergunta, conforme a configuração). A pessoa deve mover o arquivo para um local seguro, de preferência uma pasta sincronizada.
- O botão **?** no topo abre a orientação de uso (onde os dados ficam, como exportar e importar, passo a passo de quem chega à equipe).

## Decisão: sem backup automático em arquivo

Foi testada a gravação automática num arquivo escolhido uma vez (File System Access API, Chrome). A permissão volta a ser pedida ao reabrir a aba, então o ganho sobre o backup manual não compensa a complexidade. Descartado.

## Possibilidade futura (não decidida)

Uma biblioteca da equipe somente leitura, em arquivo JSON, convivendo com as mensagens pessoais. Só faz sentido se a equipe quiser textos comuns; ver o trade-off de os conjuntos divergirem com o tempo.

## Cuidados

- Nunca colocar dados pessoais ou sensíveis nas mensagens: o modelo não é seguro o bastante para isso.
- Backups são arquivos comuns: guardar numa pasta de acesso restrito.
