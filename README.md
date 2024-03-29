# Desafio de Projeto - Bootcamp Santander 2023

## Processando e Transformando Dados com Power BI

- Relatório de Categorização da base de dados de teste Azure Company

![Página 1 do relatório](relatorio-azure-company.png)
![Página 2 do relatório](relatorio-azure-company-2.png)

### Descrição do Desafio

- [x] Criação de uma instância na Azure para MySQL

- [x] Criar o Banco de dados com base disponível no github

- [x] Integração do Power BI com MySQL no Azure

- [x] Verificar problemas na base a fim de realizar a transformação dos dados

### Diretrizes para transformação dos dados

1. Verifique os cabeçalhos e tipos de dados
2. Modifique os valores monetários para o tipo double preciso
3. Verifique a existência dos nulos e analise a remoção
4. Os employees com nulos em Super_ssn podem ser os gerentes. Verifique se há algum colaborador sem gerente
5. Verifique se há algum departamento sem gerente
6. Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas
7. Verifique o número de horas dos projetos
8. Separar colunas complexas
9. Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela employee. Fique atento, essa informação influencia no tipo de junção
10. Neste processo elimine as colunas desnecessárias.
11. Realize a junção dos colaboradores e respectivos nomes dos gerentes . Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no processo.
12. Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores
13. Mescle os nomes de departamentos e localização. Isso fará que cada combinação departamento-local seja único. Isso irá auxiliar na criação do modelo estrela em um módulo futuro.
14. Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir.
15. Agrupe os dados a fim de saber quantos colaboradores existem por gerente
16. Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela

### Resolução do Desafio

#### Limpeza dos dados

##### Power Bi

- [x] Neste processo elimine as colunas desnecessárias.
- Remoção das colunas, ao carregar os dados para o PowerBI estas foram criadas a partir dos relacionamentos entre si de algumas tabelas, sendo que para este contexto em específico, as mesmas não serão necessárias.
  - Tabela azure_company departament  
    - azure_company.dept_locations;
    - azure_company.employee;
    - azure_company.project
  - Tabela azure_company dependent
    - azure_company.employee;
  - Tabela azure_company dept_locations
    - azure_company.departmant
  - Tabela azure_company project
    - azure_company.departament;
    - azure_company.works_on
  - Tabela azure_company employee
    - azure_company.departament (Ssn);
    - azure_company.dependent;
    - azure_company.employee (Ssn);
    - azure_company.employee (Super_ssn);
    - azure_company.works_on
  - Tabela azure_company.works_on
    - azure_company.employee;
    - azure_company.project

- [x] Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela

#### MySQL WorchBench

- As transformações estão no arquivo limpeza de dados [explorando a base azure_company](limpeza-dados.md).