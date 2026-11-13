# Repositório de Mensagens Padronizadas

Ferramenta para guardar e copiar mensagens padronizadas (e-mails, respostas, avisos etc.) com um clique. Abre em branco: cada pessoa cria as próprias seções e mensagens.

> Status: em desenvolvimento. As funcionalidades planejadas abaixo ainda não foram implementadas.

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

## Funcionalidades planejadas

1. **Backup automático a cada edição.** A pessoa escolhe uma vez um arquivo de backup (de preferência numa pasta sincronizada, como a do OneDrive) e a página o sobrescreve a cada alteração, usando a File System Access API (Chrome/Edge). A página não acessa o serviço de nuvem: quem sincroniza é o aplicativo instalado no computador. O botão manual de exportar continua existindo.
2. **Botão de orientação**, uma espécie de README dentro da página: onde as mensagens ficam guardadas, como exportar, como importar (importar substitui tudo) e o passo a passo de quem chega à equipe.

## A testar antes de prometer à equipe

- Se a autorização do arquivo de backup fica realmente "uma vez só" nos navegadores da equipe, ou se o navegador pede reconfirmação a cada sessão.
- Se o recurso funciona com a página aberta direto do disco (`file://`).

## Possibilidade futura (não decidida)

Uma biblioteca da equipe somente leitura, em arquivo JSON, convivendo com as mensagens pessoais. Só faz sentido se a equipe quiser textos comuns; ver o trade-off de os conjuntos divergirem com o tempo.

## Cuidados

- Nunca colocar dados pessoais ou sensíveis nas mensagens: o modelo não é seguro o bastante para isso.
- Backups são arquivos comuns: guardar numa pasta de acesso restrito.
