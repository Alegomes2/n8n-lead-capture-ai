# Explicação do Workflow

## 1. Objetivo

O workflow automatiza a captação e qualificação de potenciais clientes a partir de estabelecimentos encontrados no Google Maps.

Seu objetivo é reduzir o trabalho manual de pesquisa, organização e análise de leads, registrando os novos contatos em um CRM no Notion.

## 2. Etapas do processamento

### 2.1. Configuração da busca

O workflow utiliza parâmetros configuráveis para definir o nicho de mercado e a localização dos estabelecimentos que serão pesquisados.

Esses parâmetros são utilizados na consulta à API da HasData.

### 2.2. Captura de estabelecimentos

A integração com a HasData realiza uma requisição HTTP para:

`https://api.hasdata.com/scrape/google-maps/search`

A resposta contém os resultados encontrados no Google Maps, incluindo informações comerciais dos estabelecimentos.

### 2.3. Processamento dos resultados

Os resultados são separados para que cada estabelecimento seja processado individualmente.

Essa etapa permite executar as verificações e operações de CRM de forma independente para cada lead.

### 2.4. Padronização dos dados

O nó **Padronizar Dados do Lead** organiza as informações recebidas em campos padronizados.

Principais campos:

| Campo | Informação |
|---|---|
| `leadNome` | Nome do estabelecimento |
| `leadCategoria` | Categoria comercial |
| `leadSite` | Website |
| `leadTelefone` | Telefone |
| `leadEndereco` | Endereço |
| `leadAvaliacao` | Avaliação no Google |
| `leadQtdAvaliacoes` | Quantidade de avaliações |
| `leadPlaceId` | Google Place ID |
| `leadGoogleMaps` | Link do estabelecimento no Google Maps |
| `leadNicho` | Nicho utilizado na pesquisa |

A padronização facilita o uso dos dados nas próximas etapas.

## 3. Deduplicação de leads

Antes de criar um registro no CRM, o workflow verifica se o estabelecimento já está cadastrado.

A estratégia utiliza três possibilidades de identificação.

### 3.1. Verificação por Google Place ID

O nó **Possui Google Place ID?** verifica se o estabelecimento possui esse identificador.

Quando disponível, o workflow consulta o Notion para procurar um registro com o mesmo Place ID.

Se encontrar um registro, o lead não é cadastrado novamente.

Se não encontrar, o fluxo continua para as verificações alternativas.

### 3.2. Verificação por telefone

Quando não há Google Place ID, ou quando a busca por esse identificador não encontra um registro, o fluxo verifica a disponibilidade de telefone.

Se houver telefone, consulta o CRM para verificar se já existe um lead com o mesmo número.

### 3.3. Verificação por nome

Quando não há telefone disponível, o workflow utiliza o nome do estabelecimento como alternativa de identificação.

Essa etapa funciona como uma última tentativa de localizar um registro existente.

**Importante:** a ver