# projeto_bimaster
# Otimização da programação de serviços de manutenção em uma plataforma de petróleo, incorporando critérios de segurança e simultaneidade entre tarefas incompatíveis.

#### Aluno: Edson Dias da Costa (https://github.com/edsondcosta).

#### Orientador(/a/es/as): Felipe Borges  e/ou  Ana Carolina Abreu (OP).
#### Co-orientador(/a/es/as): Anderson Nascimento (BI)

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- Repositório do Projeto: https://github.com/edsondcosta/projeto_bimaster.git
---

### Resumo

- O PRESENTE PROJETO apresenta um modelo de otimização da programação de serviços de manutenção planejados em uma plataforma de petróleo, para sua realização nos turnos de trabalho subsequentes. O modelo tem com objetivo maximizar o emprego da mão de obra disponível a bordo da plataforma, incorporando critérios de segurança e simultaneidade entre tarefas incompatíveis de serem realizadas em proximidade no mesmo intervalo de tempo.

- Plataformas marítimas de produção são instalações de processo compactas, responsáveis pela elevação e processamento primário de hidrocarbonetos a elevadas vazões e pressões. Equipes de operação e manutenção convivem para manter a planta em condições de segurança e eficiência dentro dos limites estabelecidos no projeto. Tais equipes desempenham diversas atividades e operações simultâneas para atingir o objetivo de produzir com segurança. Exemplos: manobras de partida e parada de equipamentos de processo, geração de energia, controle de estabilidade, trabalhos de manutenção e reparo, operações com embarcações, movimentação de cargas, abastecimento de produtos químicos, pousos e decolagens de helicópteros, entre outras. 
- Concomitante com as tarefas operacionais, em cada plataforma diariamente são realizadas diversas atividades para manutenção e reparo, que podem envolver serviços a quente (ex: solda elétrica), abertura de equipamentos que operam com óleo ou gás inflamável, trabalhos elétricos, trabalhos em altura, trabalhos sobre o mar, operações de mergulho, entre outros.

- Trabalhos e Operações Simultâneas: Duas ou mais atividades ou tarefas com potencial interferência entre elas, ocorrendo ao mesmo tempo e no mesmo lugar, resultando em riscos adicionais.

- O modelo de otimização proposto parte de um Banco de Dados criado pelo autor, com tabelas de serviços, equipamentos e características de serviços, simulando a extração das informações a partir de sistemas transacionais de uma plataforma de petróleo. 
- A psrtir dessas informações o presente projeto irá estabelecer critérios de distância segura entre as tarefas com características de simultaneidade e eliminar sobreposição de horários das tarefas que não atendem aos critérios, seguindo um passo a passo (algoritmo) que será apresentado a seguir.



---

### O problema a ser otimizado:
- Grande número de tarefas de manutenção planejadas diariamente, que podem possuir características que impedem sua realização em proximidade no mesmo intervalo de tempo. Como realizar a programação dessa demanda, de forma a maximizar o emprego da mão de obra disponível, respeitando os critérios de segurança e simultaneidade ?

### Condições antes da otimização:
- A programação dos trabalhos de manutenção da plataforma é realizada de maneira manual pelos planejadores, utilizando sistemas e planilhas sem recursos de otimização. 
- Por conta da forma manual de realização da programação e das restrições de simultaneidade, a alocação da mão de obra das equipes de manutenção sempre fica abaixo do HH disponível.
- Diariamente é realizada uma reunião de avaliação da simultaneidade com toda a liderança da plataforma. Por conta da forma manual de realização, essa reunião consome grande HH para discussão e reprogramação dos trabalhos identificados como incompatíveis para realização simultânea.
- Falhas na avaliação de simultaneidade podem ocorrer, sendo identificadas somente no momento de execução dos trabalhos. Quando essa condição ocorre, por questões de segurança é exigida a paralização de pelos menos um dos trabalhos incompatíveis, gerando ociosidade para a mão de obra alocada nestes trabalhos e desperdício de HH.

---

### A solução proposta 
- Estabelecer critérios de distância segura entre as tarefas com características de simultaneidade e eliminar sobreposição de horários das tarefas que não atendem aos critérios.

### Passo a passo da solução (algoritmo)
1. Convencionar matriz de simultaneidade com distancias seguras para cada par de características de tarefas incompatíveis de serem realizadas em proximidade no mesmo intervalo de tempo;
2. Identificar as coordenadas x, y, z de cada equipamento da plataforma onde são realizados as tarefas de manutenção;
3. Calcular a distância entre cada par equipamentos, com base em suas coordenadas utilizando a fórmula da distância entre dois pontos;
4. Separar a relação de tarefas de manutenção planejadas para um dia, com seus horários de realização previstos;
5. Identificar a distância entre cada par de tarefas, com base nos equipamentos onde serão executadas;
6. Identificar as características de cada tarefa de manutenção; 
	Nota: Tarefas que não possuam características com impacto na simultaneidade, não irão entrar na análise nem no otimizador, pois podem ser programadas para qualquer horário.
7. Buscar na matriz de simultaneidade as distancias seguras convencionadas para cada par de características das tarefas planejadas para o dia selecionado;
8. Comparar a distância real entre as tarefas (passo 5) e a distância de segurança de suas características (passo 7);
9. Identificar a sobreposição de horários das tarefas programadas para o dia, com base em seus horários de início e fim previstos, utilizando fórmula de sobreposição de horários;
10. Identificar as tarefas com distancia real menor que a distancia segura de suas características (passo 8);
11. Identificar as tarefas que possuam simultaneamente as duas condições: a) sobreposição de horários (passo 9); b) distancia real menor que a distancia segura (passo 10); 
12. Utilizar otimizador para escolher novos horários de início, eliminando a sobreposição de horários dos pares de tarefas com distancia real menor que a distancia segura estabelecida para as suas características.
    Restrição de precedência: Dentro de um mesmo serviço, as etapas devem respeitar a sequencia definida na planilha. Exemplo: a etapa com ID 1202202 somente deve    iniciar após o fim da etapa com ID 1202201, e assim sucessivamente.
    As etapas de um serviço não possuem restrição de precedência com etapas de outros serviços, mas devem atender as restrições de simultaneidade se os serviços forem incompatíveis conforme Matriz de Simultaneidade.



### Regras e Restrições

- As etapas programadas dentro de um mesmo serviço são sequenciais, não podemos ter inversão na ordem dos horários;
- Os serviços e etapas programadas de serviços diferentes podem ter sua sequência de execução alterada;
- ...

---

### Dúvidas e Pendências
- ...

---

Matrícula: 201.190.263

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
