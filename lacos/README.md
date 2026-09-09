# Laços — agenda de relacionamento com clientes

Página única (HTML, CSS e JavaScript sem dependências) publicada como artefato no claude.ai.

Artefato publicado: https://claude.ai/code/artifact/f9223076-63c8-41a6-828f-b0d13e54029f

## O que faz

- Lista de clientes com **cadência de contato** (a cada 7, 15, 30, 45, 60 ou 90 dias).
- Coluna **"Hoje"**: quem está em atraso, quem é para hoje, próximos 7 dias e datas especiais (aniversário, audiência, vencimentos) nos próximos 30 dias.
- **Registro de conversa** com data, canal, o que foi conversado, o que o advogado prometeu, o que o cliente ficou de fazer e por onde começar da próxima vez.
- **Vínculo com o Plaud**: busca gravações pelo nome do cliente e traz o resumo automático para o registro.
- Campo **"Lado pessoal"** e **datas que importam** por cliente.
- **Responsável** por cliente, com filtro por pessoa da equipe (lembrado no navegador).
- **Lembrete no Google Calendar**: cria um evento às 9h na data do próximo contato (e o substitui quando a data muda).
- **Mensagem ao cliente**: após cada conversa registrada, a página redige um texto curto e em linguagem simples para enviar por WhatsApp (via capacidade `sample`; sem ela, usa um modelo fixo).
- **E-mail matinal** (rotina no claude.ai, dias úteis às 7h30, fuso de São Paulo) com quem está em atraso, hoje, próximos 7 dias e datas especiais.

## Armazenamento

- Publicada pelo claude.ai com a capacidade `db`: os dados ficam em base compartilhada com a equipe do escritório (organização).
- Aberta fora do claude.ai, a página funciona com armazenamento local do navegador (aviso exibido no topo).

## Integração com o Plaud

Declarada via capacidade `mcp` com os conectores **Plaud** (`list_files`, `get_note`) e **Google Calendar** (`create_event`, `delete_event`).
A busca no Plaud procura primeiro no título da gravação e, a pedido, dentro dos resumos dos últimos 60 dias.
Cada usuário usa as próprias credenciais do conector; a página nunca vê tokens.

## Modelo de dados

- `clientes/{id}`: nome, empresa, responsavel, assunto, cadenciaDias, canal, status, telefone, email, pessoal, datasImportantes[], ultimoContato, proximoContato, ultimaConversa, agendaEvento {id, link, data}.
- `clientes/{id}/conversas/{id}`: data, canal, resumo, prometi, prometeu, proximoAssunto, plaud {id, nome, inicio, duracao}.
