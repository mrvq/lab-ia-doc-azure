
# 🧾 Laboratório Azure – Ingestão e Indexação de Documentos com IA

## 🎯 Objetivo

Este laboratório teve como finalidade aplicar técnicas de **organização e mineração de informação** por meio de **ingestão de documentos**, **indexação com IA** e **exploração de dados estruturados**. A proposta é compreender como extrair valor de grandes volumes de informação usando ferramentas modernas da Microsoft Azure.

---

## 🛠️ Tecnologias e Recursos Utilizados

- **Azure AI Search (antigo Cognitive Search)**
- **Azure Form Recognizer (Document Intelligence)**
- **Azure Blob Storage**
- **Azure OpenAI Service (opcional, para análise avançada)**

---

## 🔍 Etapas Desenvolvidas

### 1. Ingestão de Documentos

Nesta etapa, os documentos brutos (PDFs, imagens, DOCXs) foram enviados para um contêiner do **Azure Blob Storage**.

#### Ferramentas utilizadas:
- Azure Storage Account + Container Blob
- Azure Form Recognizer (Document Intelligence)

#### Passos:
1. Criar um recurso de Storage Account no portal Azure.
2. Fazer upload dos arquivos no contêiner criado.
3. Usar o **Form Recognizer** para extrair conteúdo dos documentos.
4. Armazenar os arquivos de saída (JSON) para indexação.

#### Dicas:
- Organize os documentos por tipo de conteúdo.
- Use `Document - Layout` para extração de texto + estrutura.

---

### 2. Criação de Índices Inteligentes

Com os documentos extraídos, a próxima etapa foi a criação de um **índice de busca inteligente** usando **Azure AI Search**.

#### Ferramentas utilizadas:
- Azure Cognitive Search (AI Search)
- Enrichment Skillsets (OCR, extração de entidade, idioma)

#### Passos:
1. Criar um novo recurso de Azure Search no portal.
2. Configurar a **origem de dados** apontando para o Blob Storage.
3. Definir um **índice** com os campos desejados (ex: título, data, conteúdo).
4. Aplicar **skills cognitivas** para enriquecer os dados automaticamente.
5. Indexar e revisar os dados no portal Azure.

#### Dicas:
- Ative OCR para documentos com imagens.
- Use NER (Named Entity Recognition) para extrair nomes, datas e locais.
- Mantenha o índice sincronizado com o Blob.

---

### 3. Exploração e Consulta

Depois da indexação, é possível explorar os dados usando consultas simples ou avançadas (incluindo IA generativa com Azure OpenAI).

#### Ferramentas utilizadas:
- Azure Portal (Query Explorer)
- Interface de busca (opcional via app customizado)
- Azure OpenAI (para complemento inteligente)

#### Passos:
1. Acessar a seção "Search Explorer" no portal Azure.
2. Realizar buscas por termos, frases e filtros.
3. Observar os campos retornados: `_score`, `content`, `metadata`.
4. (Opcional) Criar um app frontend que consome esse índice via API REST.

#### Dicas:
- Use operadores: `search=palavra AND data ge 2023-01-01`.
- Combine IA com busca tradicional para mais contexto.
- Teste visualizações com ferramentas como Power BI ou dashboards web.

---

## 💡 Insights Obtidos

- A automação da indexação acelera a organização de documentos em massa.
- As **cognitive skills** permitem enriquecer os dados com IA (extração de entidades, idioma, sentimentos).
- As ferramentas da Azure são altamente integráveis e escaláveis.
- Com poucos cliques, é possível montar uma **base de conhecimento navegável e interativa**.

---

## ✅ Conclusão

Este laboratório demonstrou como a Microsoft Azure pode ser usada para transformar documentos brutos em **bases de conhecimento consultáveis**, otimizando a extração de valor em processos documentais e corporativos.

---

📅 **Data**: Maio de 2025  
👤 **Autor**: Marcio

# Ingestão de Documentos com IA no Azure

A **ingestão de documentos** no Azure envolve a importação de arquivos de diferentes formatos (PDF, DOCX, imagens, etc.) para serem processados e analisados utilizando ferramentas de IA da plataforma. O Azure oferece serviços como **Azure Cognitive Services** e **Azure Blob Storage**, que permitem armazenar e ingerir documentos para análise e indexação.

## Passos para Ingestão de Documentos no Azure

1. **Armazenamento no Azure Blob Storage**:
   O primeiro passo é armazenar seus documentos no Azure Blob Storage, que é uma solução escalável de armazenamento de objetos.
   
   - Crie uma conta de armazenamento no Azure.
   - Crie um contêiner dentro da conta de armazenamento para organizar os documentos.

2. **Uso do Azure Cognitive Services**:
   Com o **Azure Cognitive Services**, é possível realizar a análise e extração de informações dos documentos. Por exemplo, o **Azure Form Recognizer** pode extrair dados de formulários e tabelas, enquanto o **Azure Computer Vision** pode processar documentos de imagem e PDF.

### Exemplo de Ingestão com Azure Form Recognizer:

```python
from azure.ai.formrecognizer import FormRecognizerClient
from azure.core.credentials import AzureKeyCredential

# Definir as credenciais e o endpoint
endpoint = "https://<seu-endpoint>.cognitiveservices.azure.com/"
key = "<sua-chave>"

# Conectar ao Form Recognizer
form_recognizer_client = FormRecognizerClient(endpoint, AzureKeyCredential(key))

# Carregar o documento (pode ser um PDF ou imagem armazenado no Blob Storage)
with open("documento.pdf", "rb") as f:
    poller = form_recognizer_client.begin_recognize_content(f)
    result = poller.result()

# Exibir resultados da extração
for page in result:
    for table in page.tables:
        print(table)


---

### 02_indexacao.md

```markdown
# Indexação de Documentos com IA no Azure

A **indexação de documentos** no Azure permite que você organize e consulte grandes volumes de documentos de forma eficiente. O **Azure Cognitive Search** é uma ferramenta poderosa para criar um índice de documentos e aplicar modelos de IA para melhorar a busca e a análise.

## Passos para Indexação de Documentos no Azure

1. **Criando um Serviço de Azure Cognitive Search**:
   - Crie um **Serviço de Pesquisa** no portal do Azure.
   - Configure um índice com campos relevantes para os documentos que deseja indexar (por exemplo, título, autor, data de criação, conteúdo).

2. **Importação de Documentos para o Índice**:
   - Você pode usar o **Azure Blob Storage** como fonte de dados e configurar o **Azure Cognitive Search** para indexar os documentos armazenados.

3. **Uso de IA na Indexação**:
   O Azure Cognitive Search também pode aplicar modelos de IA como OCR (Reconhecimento Óptico de Caracteres) e extração de entidades para melhorar a indexação e permitir buscas mais precisas.

### Exemplo de Indexação com Azure Cognitive Search:

```python
from azure.search.documents import SearchClient
from azure.search.documents.models import IndexingParameters, IndexAction
from azure.core.credentials import AzureKeyCredential

# Definir credenciais e endpoint
search_endpoint = "https://<seu-endpoint>.search.windows.net"
index_name = "documentos"
api_key = "<sua-chave>"

# Conectar ao cliente de pesquisa
client = SearchClient(endpoint=search_endpoint, index_name=index_name, credential=AzureKeyCredential(api_key))

# Definir os documentos a serem indexados
documentos = [
    {"id": "1", "titulo": "Relatório de Vendas", "conteudo": "Texto extraído do relatório de vendas..."},
    {"id": "2", "titulo": "Contrato de Compra", "conteudo": "Texto extraído do contrato..."}
]

# Indexar documentos
result = client.upload_documents(documents=documentos)
print("Documentos indexados com sucesso")


---

### 03_exploracao.md

```markdown
# Exploração de Documentos Indexados com IA no Azure

Após a ingestão e indexação dos documentos, a **exploração dos dados** se torna fundamental para realizar buscas eficientes e obter insights valiosos. O **Azure Cognitive Search** oferece funcionalidades avançadas de consulta e análise dos documentos indexados, utilizando IA para melhorar a relevância e a precisão das respostas.

## Passos para Exploração de Documentos Indexados

1. **Consultas Simples e Avançadas**:
   O Azure Cognitive Search oferece a capacidade de fazer consultas simples de texto completo, bem como consultas mais avançadas com filtragem, ordenação e facetamento.

2. **Uso de IA nas Consultas**:
   Ao realizar uma consulta, o Azure pode aplicar técnicas de IA como **Pesquisa Semântica** para melhorar a precisão dos resultados, considerando o contexto e a intenção do usuário.

3. **Análise de Dados**:
   Com a integração de IA, você pode realizar tarefas como **extração de entidades** (nomes, datas, locais) e **classificação de documentos** para entender melhor o conteúdo dos documentos.

### Exemplo de Consulta com Azure Cognitive Search:

```python
from azure.search.documents import SearchClient
from azure.core.credentials import AzureKeyCredential

# Definir credenciais e endpoint
search_endpoint = "https://<seu-endpoint>.search.windows.net"
index_name = "documentos"
api_key = "<sua-chave>"

# Conectar ao cliente de pesquisa
client = SearchClient(endpoint=search_endpoint, index_name=index_name, credential=AzureKeyCredential(api_key))

# Realizar uma consulta simples
resposta = client.search("relatório de vendas")

# Exibir resultados da consulta
for doc in resposta:
    print(f"ID: {doc['id']}, Título: {doc['titulo']}")

