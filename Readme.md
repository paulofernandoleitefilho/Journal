Filtro e Cruzamento de Periódicos Científicos (Qualis)

A aplicação automatiza a interseção entre bases de dados de publicações (Journals) e as tabelas de classificação de excelência acadêmica. O objetivo é permitir que pesquisadores e instituições identifiquem veículos de publicação que atendam a critérios específicos de estratificação (A1, A2, B1, etc.) em determinadas áreas de avaliação.

Arquitetura de Dados
O pipeline de processamento segue o modelo ETL (Extract, Transform, Load):

Extração (Ingestion): Consumo de arquivos estruturados (CSV/XLSX) provenientes da Plataforma Sucupira e bases de indexação (Scopus, Web of Science).

Normalização: Tratamento de identificadores únicos, primariamente o ISSN (International Standard Serial Number), garantindo a integridade dos dados através de regex para validação de formato e remoção de duplicatas.

Cruzamento (Joining): Operação de Inner Join entre a base de produção intelectual e a tabela de referência Qualis, utilizando o ISSN como chave primária.

Filtragem Parametrizada: Aplicação de predicados lógicos para selecionar apenas os estratos desejados (Ex: Qualis >= 'A2') e áreas do conhecimento específicas.

Funcionalidades Técnicas
Busca Multicritério: Filtragem por título do periódico, ISSN, estrato Qualis e área de avaliação.

Deduplicação de Registros: Algoritmos de limpeza para tratar variações de ISSN (L-ISSN, P-ISSN, E-ISSN).

Exportação de Resultados: Geração de relatórios técnicos em formatos consumíveis por outras ferramentas de análise (JSON, CSV).

Persistência: Implementação de cache local ou banco de dados relacional para otimizar consultas repetitivas aos dados da Sucupira.

Requisitos de Sistema e Dependências
Para garantir a performance no processamento de grandes volumes de dados de indexação:

Engine de Manipulação: Utilização de bibliotecas de alta performance para manipulação de DataFrames (como pandas em Python ou tidyverse em R).

Validação de Esquema: Verificação de tipos de dados para evitar inconsistências durante o parse dos arquivos da CAPES.