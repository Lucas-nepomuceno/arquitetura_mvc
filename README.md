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

&nbsp;&nbsp;&nbsp;&nbsp; Para facilitar a aplicação, optou-se por transformar o relacionamento "leitura" em uma tabela por associação. Isso é aconselhável dado a cardinalidade entre as tabelas e o relacionamento (muitos para muitos). Portanto, transformou-se leitura em uma tabela cujos atributos são: id_delegacao (chave primária), CPF_administrador (chave estrangeira), CPF_montador (chave estrangeira), id_manual (chave estrangeira), finalizado. 

## Controladores (Controllers):

&nbsp;&nbsp;&nbsp;&nbsp; Nesta aplicação, os usuários serão divididos em administradores e montadores. Os administradores têm acesso aos seguintes controladores:
- Adicionar_manual: adicionar um manual à lista de manuais
  - Parâmetros de entrada: nome, data, URL
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela "manuais"
  - View: altera o repositório de manuais, adicionando um manual

- Atualizar_manual: atualiza um manual já criado
  - Parâmetros de entrada: id_manual, data, URL, descricao
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para alterar um registro da tabela "manuais"
  - View: altera o repositório de manuais, atualizando-o; adiciona uma descrição da atualização aos funcionários que tinham o manual na sua lista de leitura e altera o dashboard do funcionário atualizando a leitura
  
- Delegar: delegar uma leitura a um montador
  - Parâmetros de entrada: CPF_administrador, CPF_montador, id_manual
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para adicionar um registro a tabela "leitura"
  - View: altera o dashboard do funcionário, adicionando a leitura; altera a dashboard do administrador

- Retirar: retirar uma leitura a um montador
  -  Parâmetros de entrada: id_delegacao
  -  Parâmetros de saída: N/A
  -  Ações: Pedir ao model para retirar um registro da tabela "leitura"
  -  View: altera o dashboard do funcionário, retirando a leitura; altera a dashboard do administrador
 
&nbsp;&nbsp;&nbsp;&nbsp; Já os montadores têm acesso aos seguintes controllers:
- Checar: dá um "check" no manual
  - Parâmetros de entrada: id_delegação
  - Parâmetros de saída: N/A
  - Ações: Pedir ao model para alterar o registro sob id_delegacao da tabela leitura, setando o atributo finalizado como verdadeiro
  - View: altera a dashboard do funcionário, "riscando" a tarefa da lista; altera o dashboard do administrador
  
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
- Dashboard do administrador: permitirá o administrador delegar e retirar manuais da lista de leitura de seus funcionários e ver o desempenho deles;
- Dashboard do montador: permitirá o montador ver sua lista de leitura, checar as leituras já feitas e acessar os manuais;
- Repositório de manuais: permitirá ao administrador adicionar e atualizar manuais

## Infraestrutura:
Descreva os componentes de infraestrutura do seu projeto, como bancos de dados, APIs externas e outras dependências.
Explique como a infraestrutura se integra à arquitetura MVC.
Justifique as escolhas feitas e como elas impactam o projeto.
## Implicações da Arquitetura:
Descreva as implicações da arquitetura em termos de escalabilidade, manutenção, testabilidade e outros aspectos importantes.
