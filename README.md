Web Scraper Vitrine Sebrae Startups
📊 Sobre o Projeto

Este projeto é um Web Scraper desenvolvido para extrair dados estruturados de todas as startups cadastradas na plataforma Vitrine Sebrae Startups.

Objetivo: Automatizar a coleta, validação e armazenamento de dados das startups, exportando-os diretamente para o Google Drive e planilhas dinâmicas no Google Sheets.
🚀 Funcionalidades

    Extração Concorrente: Utiliza múltiplas threads (ThreadPoolExecutor) para uma raspagem de dados rápida e eficiente, processando mais de 1.000 páginas e 13.000+ startups em minutos.
    Sincronização na Nuvem: Integração nativa com a API do Google Drive e Google Sheets para salvar backups CSV e alimentar dashboards automaticamente.
    Tratamento de Dados Inteligente: Valida as informações extraídas e as separa automaticamente em dados completos, válidos e incompletos.
    Geração de Relatórios: Cria um relatório relatorio.txt formatado e visual detalhando os resultados da coleta, taxas de erro e campos faltantes.
    Tolerância a Falhas: Sistema automático de repetição (retries) e tratamento de erros de servidor para garantir estabilidade durante longas execuções.

📦 Dados Extraídos

Os seguintes campos são coletados de cada startup:

    name (Nome da empresa)
    type (Startup ou Projeto Inovador)
    city / state (Localização)
    siteUrl (Website oficial)
    email (E-mail de contato)
    phone (Telefone de contato)
    maturity_pt (Estágio de maturidade)
    segment_pt (Segmento/Categoria)
    description_pt (Descrição completa)
    imageUrl (URL da logomarca)

📁 Arquivos Gerados

Ao final da execução, o script salva os seguintes arquivos na pasta destino do Google Drive:

    COMPLETO.csv: Todas as startups raspadas no processo.
    DADOS_VALIDOS.csv: Startups que contêm pelo menos um canal de contato e nome válido.
    DADOS_INVALIDOS.csv: Startups com dados essenciais faltando.
    relatorio.txt: Relatório em formato de texto (histórico mantido).
    ERROS.csv: (Opcional) Gerado apenas se houver falhas críticas de requisição.
    Planilha Google (Dashboard_Startups_Sebrae): Planilha sincronizada e atualizada em tempo real.

🛠️ Como Utilizar no Google Colab

    Instalação de Dependências (Célula 1): Execute para instalar e carregar as bibliotecas (Pandas, Requests, Gspread, etc).
    Autenticação (Célula 2): Faça login com sua conta do Google para liberar o acesso de escrita no Google Drive e Google Sheets. Configure a variável CLIENTE_FOLDER_ID para a pasta desejada.
    Carregar as Funções (Células 3 e 4): Execute as células contendo os métodos auxiliares e a classe base do scraper SebraeScraper.
    Iniciar Coleta (Célula 5): Defina o número de páginas ou deixe end_page=None para raspar a vitrine inteira.
    Salvar Dados (Célula 6): Dispara a exportação dos CSVs, geração do relatório .txt e a sincronização com o Google Sheets.
    Prévia (Célula 7): Célula opcional para visualizar os dataframes gerados diretamente na interface do Colab.


<img width="1733" height="1024" alt="image" src="https://github.com/user-attachments/assets/c22b2c3c-48f7-4486-b076-6da7e76968b3" />


