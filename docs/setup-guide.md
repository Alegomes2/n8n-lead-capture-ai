# Guia de Instalação e Configuração

## 1. Visão geral

Este guia apresenta os procedimentos necessários para importar e configurar o workflow de captação automática de leads com IA.

O projeto utiliza:

- n8n
- HasData API
- Groq API
- Notion API

Cada integração precisa ser configurada com credenciais próprias.

## 2. Pré-requisitos

Antes de começar, é necessário possuir:

- Uma instalação funcional do n8n.
- Uma conta na HasData com acesso à API.
- Uma chave de API da Groq.
- Uma conta no Notion.
- Um banco de dados do Notion preparado para armazenar os leads.

## 3. Clonar o repositório

Abra o terminal e execute:

```bash
git clone https://github.com/Alegomes2/n8n-lead-capture-ai.git
```

Entre na pasta:

```bash
cd n8n-lead-capture-ai
```

## 4. Importar o workflow no n8n

1. Acesse sua instalação do n8n.
2. Abra a opção de importação de workflow.
3. Selecione o arquivo `workflow/lead-capture-workflow.json`.
4. Aguarde a importação.
5. Revise os nós e as conexões.

O arquivo disponibilizado no GitHub é uma versão sanitizada. Portanto, será necessário configurar novamente as credenciais e os parâmetros de integração.

## 5. Configurar as credenciais

### 5.1. HasData

1. Acesse sua conta HasData.
2. Obtenha sua chave de API.
3. No n8n, abra o nó HTTP Request responsável pela consulta ao Google Maps.
4. Configure a autenticação utilizando a credencial Header Auth.
5. Defina o nome do cabeçalho como `x-api-key`.
6. Informe sua chave de API como valor.
7. Salve a credencial.

Não compartilhe sua chave de API publicamente.

### 5.2. Groq AI

1. Acesse a plataforma da Groq.
2. Gere uma chave de API.
3. No n8n, abra a configuração da integração com Groq.
4. Crie ou selecione uma credencial Groq.
5. Informe sua chave de API.
6. Confirme a configuração do modelo `openai/gpt-oss-20b`.

A disponibilidade do modelo depende das condições e limites oferecidos pela plataforma.

### 5.3. Notion

1. Crie uma integração na plataforma Notion.
2. Obtenha o token de integração.
3. No n8n, crie uma credencial Notion.
4. Informe o token de acesso.
5. Abra o banco de dados que será utilizado como CRM.
6. Compartilhe o banco de dados com a integração criada.
7. Selecione o banco de dados nos quatro nós do workflow que realizam consultas ou operações no Notion.

**Importante:** a integração precisa ter as permissões necessárias para consultar e criar registros.

## 6. Preparar o banco de dados do Notion

O banco de dados deve conter as propriedades utilizadas pelo workflow.

Entre os principais campos estão:

- Nome do estabelecimento.
- Nicho.
- Status.
- Site.
- Telefone.
- Cidade/Bairro.
- Avaliações Google.
- Google Maps URL.
- Google Place ID.
- Prioridade.
- Oportunidade.
- Análise IA.

Os nomes e tipos das propriedades precisam corresponder às configurações utilizadas nos nós do n8n.

## 7. Configurar os parâmetros de busca

Revise o nó responsável pela configuração da pesquisa.

Defina:

- Nicho desejado.
- Localização dos estabelecimentos.

Esses parâmetros determinam quais empresas serão pesquisadas pela HasData.

## 8. Revisar o workflow

Antes de executar, confira:

- Se todas as credenciais estão selecionadas.
- Se os quatro nós do Notion apontam para o banco de dados correto.
- Se as propriedades do CRM correspondem aos campos utilizados.
- Se a credencial HasData está configurada corretamente.
- Se a integração Groq está funcionando.
- Se as conexões entre os nós estão preservadas.

## 9. Executar e validar

Recomenda-se realizar os primeiros testes com uma base de dados de teste no Notion.

Durante a validação, verifique:

1. Se a HasData retorna estabelecimentos.
2. Se os dados são processados e padronizados.
3. Se a deduplicação identifica registros existentes.
4. Se a IA retorna prioridade, oportunidade e análise.
5. Se os novos leads são cadastrados corretamente no CRM.

Evite executar testes diretamente em um CRM de produção sem antes avaliar os possíveis efeitos da execução.

## 10. Segurança

- Nunca publique tokens ou chaves de API.
- Utilize as credenciais do próprio n8n.
- Não compartilhe arquivos contendo informações privadas.
- Utilize bancos de dados de teste durante a validação inicial.
- Não inclua dados pessoais ou comerciais de terceiros nos exemplos públicos do repositório.

## 11. Suporte e contribuições

Este projeto faz parte do portfólio de desenvolvimento