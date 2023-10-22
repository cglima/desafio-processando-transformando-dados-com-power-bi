# Transformando os dados no mySQL
- [x] Os employees com nulos em Super_ssn podem ser os gerentes.Verifique se há algum colaborador sem gerente ```sql
select *
from employee
where Super_ssn is NULL;

select *
from employee as gerente join employee as empregado on empregado.Super_ssn = gerente.Ssn
order by gerente.Ssn ;
``` - [x] Verifique se há algum departamento sem gerente ```sql
select *
from departament;
``` - [x] Verifique o número de horas dos projetos ```sql
select Pname, sum(Hours) as Total_horas
from project join works_on
group by Pname;
``` - [x] Separar colunas complexas ```sql
select
    SUBSTRING_INDEX(Address, '-', 1) as Rua,
    SUBSTRING_INDEX(SUBSTRING_INDEX(Address, '-', -2), '-', 1) as Cidade,
    SUBSTRING_INDEX(Address, '-', -1) as Estado
from employee;
``` - [x] Mesclar consultas employee e departament para criar uma tabela employee com o nome dos departamentos associados aos colaboradores.A mescla terá como base a tabela employee.Fique atento,
essa informação influencia no tipo de junção ```sql
select * from employee;
select * from departament;

select concat(Fname, " ", Minit, " ", Lname) as Nome_colaborador, Dname
from employee join departament on Dno = Dnumber;
``` - [x] Realize a junção dos colaboradores e respectivos nomes dos gerentes.Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI.Caso utilize SQL,
especifique no README a query utilizada no processo.```sql
select gerente.Fname as Gerente,  empregado.Fname as Empregado
from employee as gerente join employee as empregado on empregado.Super_ssn = gerente.Ssn;

select gerente.Ssn, gerente.Fname as Gerente, empregado.Ssn, empregado.Fname as Empregado
from employee as gerente join employee as empregado on empregado.Super_ssn = gerente.Ssn
order by gerente.Ssn;
``` - [x] Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores ```sql
select concat(Fname, " ", Minit, " ", Lname) as Nome_colaboradores
 from employee;
``` - [x] Mescle os nomes de departamentos e localização.Isso fará que cada combinação departamento - local seja único.Isso irá auxiliar na criação do modelo estrela em um módulo futuro.```sql
select concat(d.Dname, ' - ', dl.Dlocation) as "departamento-local"
from departament as d
join dept_locations as dl on d.Dnumber = dl.Dnumber;
``` - [x] Explique por que,
neste caso supracitado,
podemos apenas utilizar o mesclar e não o atribuir.- A mesclagem e a atribuição têm significados distintos no contexto do banco de dados e consultas SQL.Quando falamos em mesclagem,
estaos combinando valores de diferentes colunas em uma única coluna para exibição.A mescla é feita apenas para visualizar os resultados de maneira concatenada,
sem modificar os valores originais das colunas nas tabelas do banco de dados.Em poucas palavras,
o processo de mesclagem não altera os valores armazenados nas tabelas,
apenas cria uma visualização temporária dos dados combinados.Em contra partida,
o processo de atribuição em banco de dados refere - se a atualizações e alterações diretas nos valores das colunas nas tabelas.Isto,
implica uma alteração nos valores originais das colunas nas taberlas por valores que foram atribuídos.- Portanto,
no contexto da pergunta,
sobre mesclagem de nomes de departamento e localização,
não há necessidade de atribuição,
uma vez que o objetivo é exibir os valores mesclados sem modificar os dados originais das tabelas.A atribuição seria necessária se estivéssemos atualizando os valores das colunas em uma tabela com novos dados.- [x] Agrupe os dados a fim de saber quantos colaboradores existem por gerente ```sql
select concat(gerente.Fname, " ", gerente.Minit, " ", gerente.Lname) as Gerente, count(empregado.Fname) as Empregado
from employee as gerente join employee as empregado on empregado.Super_ssn = gerente.Ssn
group by gerente.Ssn, gerente.Fname
order by gerente.Ssn;
```