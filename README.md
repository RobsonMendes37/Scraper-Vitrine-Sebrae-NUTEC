# Web Scraper — Vitrine Sebrae Startups

Script em Python para extração, validação e exportação de dados da plataforma Vitrine Sebrae Startups. O fluxo extrai os registros das empresas cadastradas, filtra a integridade dos dados e salva os resultados no Google Drive e Google Sheets.

## Funcionalidades

- **Coleta Concorrente:** Utiliza `ThreadPoolExecutor` para acelerar a paginação e a raspagem de dados (+1.000 páginas e +13.000 registros).
- **Validação de Registros:** Classifica as startups entre dados válidos (com canais de contato ativos) e dados incompletos.
- **Exportação para Nuvem:** Integração com APIs do Google Workspace (`gspread` e Google Drive API) para geração de planilhas e backups em CSV.
- **Log de Execução:** Geração de arquivo `relatorio.txt` com métricas de completude, contagem de registros e erros de requisição.
- **Resiliência:** Tratamento de timeouts, erros de conexão HTTP e retries automáticos.

<img width="914" height="502" alt="Execução do Scraper" src="https://github.com/user-attachments/assets/c83dddb5-d889-4096-bc21-ac6495a858b5" />

## Esquema dos Dados Coletados

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `name` | String | Nome cadastrado da empresa ou projeto |
| `type` | String | Categoria (`Startup` ou `Projeto Inovador`) |
| `city` / `state` | String | Município e Estado (UF) |
| `siteUrl` | String | URL do site oficial |
| `email` | String | E-mail de contato cadastrado |
| `phone` | String | Telefone de contato |
| `maturity_pt` | String | Fase de maturidade do negócio |
| `segment_pt` | String | Setor/mercado de atuação |
| `description_pt`| Text | Descrição do modelo de negócio |
| `imageUrl` | String | Link da imagem/logotipo |

<img width="1733" height="1024" alt="Visualização dos Dados" src="https://github.com/user-attachments/assets/c22b2c3c-48f7-4486-b076-6da7e76968b3" />

## Estrutura dos Arquivos de Saída

Os arquivos gerados são armazenados na pasta configurada no Google Drive:

- `COMPLETO.csv`: Todos os registros capturados na execução.
- `DADOS_VALIDOS.csv`: Registros que possuem nome e pelo menos um meio de contato (site, e-mail ou telefone).
- `DADOS_INVALIDOS.csv`: Registros sem os campos essenciais de contato.
- `Dashboard_Startups_Sebrae`: Planilha Google sincronizada com os dados válidos.
- `relatorio.txt`: Log com total de registros processados, campos ausentes e status final.
- `ERROS.csv`: (Opcional) Log de requisições que atingiram o limite de tentativas sem sucesso.

## Execução no Google Colab

1. **Dependências (Célula 1):** Instale e carregue as bibliotecas necessárias (`pandas`, `requests`, `gspread`).
2. **Autenticação (Célula 2):** Realize o login na conta Google e defina o identificador da pasta de destino:
   ```python
   CLIENTE_FOLDER_ID = "SEU_ID_DE_PASTA_NO_DRIVE"
   ```
3. **Instanciação (Células 3 e 4):** Execute os métodos auxiliares e a classe `SebraeScraper`.
4. **Coleta (Célula 5):** Defina o intervalo de páginas desejado ou utilize `end_page=None` para varrer todas as páginas:
   ```python
   scraper.run(start_page=1, end_page=None)
   ```
5. **Persistência (Célula 6):** Exporte os arquivos CSV, gere o `relatorio.txt` e sincronize com o Google Sheets.
6. **Prévia (Célula 7):** Opcionalmente, visualize os DataFrames gerados diretamente no notebook.

## Requisitos

- Python 3.8+
- Bibliotecas: `requests`, `pandas`, `gspread`, `google-auth`
