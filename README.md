# MVC - LedTech/Dell
- <b> Nome do Projeto: </b> DellAware
- <b> Descrição: </b> Trata-se de uma aplicação web que será desenvolvida para a empresa Dell Technologies voltada a resolver o problema das pausas na linha de produção. Para tanto, disponibilizar-se-á, por meio da ação dos administradores, os manuais necessários para a linha de produção individualmente a cada montador da fábrica. Além disso, os montadores terão a chance de checar os manuais que já leram e os administradores verão o desempenho dos montadores em relação a leitura dos manuais.
- <b> Arquitetura: </b> MVC (Model-View-Controller)
- <b> Ferramenta de Diagramação: </b> draw.io
## Modelos (Models):

&nbsp;&nbsp;&nbsp;&nbsp; O modelo deste projeto é composto de três entidades principais: administradores, montadores e manuais. O primeiro é composto pelos seguintes atributos: CPF (chave-primária), nome, equipe, senha. Já o segundo é composto pelos seguintes atributos: CPF (chave-primária), nome, equipe, senha. Enquanto isso, o último é composto pelos seguintes atributos: id (chave primária), nome, ultima_atualizacao, URL. <br>
&nbsp;&nbsp;&nbsp;&nbsp; Entre si, esses atributos estabelecem o relacionamento de "leitura", segundo o seguinte modelo conceitual:

<div align="center">
<sub>Figura 1 - Modelo conceitual</sub> <br>
  
<img width="720" alt="modelo-conceitural-bd" src="https://github.com/Lucas-nepomuceno/arquitetura_mvc/assets/158762017/75fc6f73-9db1-49f5-bad4-4ea6e6f0b7de">

<sup>Material produzido pelos autores (2024)</sup>
</div>

&nbsp;&nbsp;&nbsp;&nbsp; Porém, para facilitar a aplicação, optou-se por transformar o relacionamento "leitura" em uma tabela por associação. Isso é aconselhável dado a cardinalidade entre as tabelas e o relacionamento (muitos para muitos). Portanto, transformou-se leitura em uma tabela cujos atributos são: id_delegacao (chave primária), CPF_administrador (chave estrangeira), CPF_montador (chave estrangeira), id_manual (chave estrangeira), finalizado. 

## Controladores (Controllers):

&nbsp;&nbsp;&nbsp;&nbsp; Nesta aplicação, os usuários serão divididos em administradores e montadores. Os administradores têm acesso aos seguintes controladores:
- Adicionar_manual: adiciona um manual à lista de manuais
  - Parâmetros de entrada: nome, data, URL
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela "manuais"
  - View: altera o repositório de manuais, adicionando um manual

- Atualizar_manual: atualiza um manual já criado
  - Parâmetros de entrada: id_manual, data, URL, descricao
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para alterar um registro da tabela "manuais"
  - View: altera o repositório de manuais, atualizando-o; adiciona uma descrição da atualização aos funcionários que tinham o manual na sua lista de leitura e altera o dashboard do funcionário atualizando a leitura
  
- Delegar: delega uma leitura a um montador
  - Parâmetros de entrada: CPF_administrador, CPF_montador, id_manual
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela "leitura"
  - View: altera o dashboard do montador, adicionando a leitura; altera a dashboard do administrador com novas informações

- Ver_funcionario: possibilita a visualização dos dados de um funcionário
  - Parâmetros de entrada: CPF_montador
  - Parâmetros de saída: nome_montador, equipe
  - Ações: Pedir ao model para consultar os dados de um montador sob o registro CPF_montador
  - View: Abre uma aba com os dados do funcionário 
 
&nbsp;&nbsp;&nbsp;&nbsp; Já os montadores têm acesso aos seguintes controllers:
- Checar: dá um "check" no manual
  - Parâmetros de entrada: id_delegação
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para alterar o registro sob id_delegacao da tabela leitura, setando o atributo finalizado como verdadeiro
  - View: altera a dashboard do funcionário, "riscando" a tarefa da lista; altera o dashboard do administrador com novas informações
  
- Ler: possibilita a leitura do manual
  - Parâmetros de entrada: id_delegação, id_manual
  - Parâmetros de saída: URL
  - Ações: Pedir ao model para consultar a URL sob o registro id_manual
  - View: N/A

&nbsp;&nbsp;&nbsp;&nbsp; Além disso, ambos os usuários terão acesso ao seguinte controller:
- Logar: permite logar na aplicação
  - Parâmetros de entrada: CPF e senha
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para consultar o registro do CPF e checar a senha nas tabelas "montadores" e "administradores"
  - View: atualiza a view, redirecionando o usuário a seu respectivo dashboard

## Views (Views):

&nbsp;&nbsp;&nbsp;&nbsp; As views, ou seja, as interfaces as quais os usuários irão interagir são:
- Login: permitirá o usuário logar na aplicação;
- Dashboard do administrador: permitirá o administrador delegar manuais da lista de leitura de seus funcionários e ver o desempenho deles;
- Dashboard do montador: permitirá o montador ver sua lista de leitura, checar as leituras já feitas e acessar os manuais;
- Repositório de manuais: permitirá ao administrador adicionar e atualizar manuais

## Infraestrutura:

&nbsp;&nbsp;&nbsp;&nbsp; Neste projeto, utilizamos o PostgreSQL como banco de dados, o Sails.js como framework e o HTML5 e CSS3 para a construção da UI. Essas tecnologias se relacionam à arquitetura MVC da seguinte forma:
- HTML5 e CSS3: View
- Sails.js: Controller/model
- PostgreSQL: Server

&nbsp;&nbsp;&nbsp;&nbsp; Isso foi feito levando em consideração as tecnologias disponibilizadas pela instituição e a trilha de aprendizagem do módulo. Preferiu-se, também, o uso de tecnologias "open source", como o Sails.js. Com relação ao impacto no projeto, a integração das tecnologias escolhidas à arquitetura MVC proporciona uma estrutura robusta para o projeto. O uso do framework Sails.js agiliza o desenvolvimento ao oferecer funcionalidades predefinidas para lidar com a lógica de negócios e interação com o banco de dados. Além disso, a adoção de tecnologias de código aberto reduz os custos e aumenta a flexibilidade do projeto, permitindo adaptações conforme necessário. Essas decisões combinadas promovem uma implementação eficiente e adaptável, alinhada às exigências do projeto e as habilidades da equipe.

## Implicações da Arquitetura:

&nbsp;&nbsp;&nbsp;&nbsp; A arquitetura Model-View-Controller (MVC) traz implicações importantes para o projeto "DellAware" da LedTech/Dell em termos de escalabilidade, manutenção, testabilidade e colaboração entre equipes de desenvolvimento. Com a separação clara de responsabilidades entre Model, View e Controller, o projeto se torna mais escalável. É possível escalar diferentes partes do sistema independentemente umas das outras, respondendo de forma eficiente a mudanças na demanda ou no volume de dados. De forma semelhante, em relação à manutenção, a divisão em três componentes distintos simplifica as atualizações e correções de bugs. As alterações podem ser feitas em cada componente de forma independente, sem afetar diretamente as outras partes do sistema. Isso torna o processo de desenvolvimento mais ágil e menos propenso a introduzir novos problemas. <br>
&nbsp;&nbsp;&nbsp;&nbsp; A testabilidade também é beneficiada pela arquitetura MVC. Cada componente pode ser testado de forma isolada, garantindo que eles estejam funcionando corretamente e interagindo entre si da maneira esperada. Isso facilita a detecção e correção de erros durante o processo de desenvolvimento, garantindo a qualidade do software final. Além disso, a adoção do padrão MVC facilita a colaboração entre equipes de desenvolvimento. Com responsabilidades claramente definidas para cada componente, as equipes podem trabalhar de forma mais eficiente e coordenada, focando em suas áreas de especialização e contribuindo para o projeto de maneira mais eficaz. <br>
&nbsp;&nbsp;&nbsp;&nbsp; Em resumo, a arquitetura MVC proporciona uma estrutura sólida para o desenvolvimento do projeto "DellAware", oferecendo benefícios significativos em termos de escalabilidade, manutenção, testabilidade e colaboração entre equipes de desenvolvimento. Isso contribui para a criação de um software robusto, flexível e de alta qualidade.
