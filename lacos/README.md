# Laços — agenda de relacionamento com clientes

Página única (HTML, CSS e JavaScript sem dependências) publicada como artefato no claude.ai.

Artefato publicado: https://claude.ai/code/artifact/f9223076-63c8-41a6-828f-b0d13e54029f

## O que faz

- Lista de clientes com **cadência de contato** (a cada 7, 15, 30, 45, 60 ou 90 dias).
- Coluna **"Hoje"**: quem está em atraso, quem é para hoje, próximos 7 dias e datas especiais (aniversário, audiência, vencimentos) nos próximos 30 dias.
- **Registro de conversa** com data, canal, o que foi conversado, o que o advogado prometeu, o que o cliente ficou de fazer e por onde começar da próxima vez.
- **Vínculo com o Plaud**: busca gravações pelo nome do cliente e traz o resumo automático para o registro.
- Campo **"Lado pessoal"** e **datas que importam** por cliente.

## Armazenamento

- Publicada pelo claude.ai com a capacidade `db`: os dados ficam em base compartilhada com a equipe do escritório (organização).
- Aberta fora do claude.ai, a página funciona com armazenamento local do navegador (aviso exibido no topo).

## Integração com o Plaud

Declarada via capacidade `mcp` com o conector **Plaud** e as ferramentas `list_files` e `get_note`.
Cada usuário usa as próprias credenciais do conector; a página nunca vê tokens.

## Modelo de dados

- `clientes/{id}`: nome, empresa, assunto, cadenciaDias, canal, status, telefone, email, pessoal, datasImportantes[], ultimoContato, proximoContato, ultimaConversa.
- `clientes/{id}/conversas/{id}`: data, canal, resumo, prometi, prometeu, proximoAssunto, plaud {id, nome, inicio, duracao}.
