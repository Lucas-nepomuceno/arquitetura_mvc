# MVC - LedTech/Dell
- <b> Nome do Projeto: </b> DellAware
- <b> Descrição: </b> Trata-se de uma aplicação web que será desenvolvida para a empresa Dell Technologies voltada a resolver o problema das pausas na linha de produção. Para tanto, disponibilizar-se-á, por meio da ação dos administradores, os manuais necessários para a linha de produção individualmente a cada montador da fábrica. Além disso, os montadores terão a chance de checar os manuais que já leram e os administradores verão o desempenho dos montadores em relação a leitura dos manuais.
- <b> Arquitetura: </b> MVC (Model-View-Controller)
- <b> Ferramenta de Diagramação: </b> draw.io
## Modelos (Models):

&nbsp;&nbsp;&nbsp;&nbsp; O modelo deste projeto é composto de três entidades principais: administradores, montadores e manuais. O primeiro é composto pelos seguintes atributos: CPF (chave-primária); nome; equipe. Já o segundo é composto pelos seguintes atributos: CPF (chave-primária); nome; equipe. Enquanto isso, o último é composto pelos seguintes atributos: id (chave primária), nome, ultima_atualizacao, URL. <br>
&nbsp;&nbsp;&nbsp;&nbsp; Entre si, esses atributos estabelecem o relacionamento de "leitura", segundo o seguinte modelo conceitual:

<div align="center">
<sub>Figura 1 - Modelo conceitual</sub> <br>
  
<img width="720" alt="modelo-conceitural-bd" src="https://github.com/Lucas-nepomuceno/arquitetura_mvc/assets/158762017/75fc6f73-9db1-49f5-bad4-4ea6e6f0b7de">

<sup>Material produzido pelos autores (2024)</sup>
</div>

&nbsp;&nbsp;&nbsp;&nbsp; Para facilitar a aplicação, optou-se por transformar o relacionamento "leitura" em uma tabela por associação. Isso é aconselhável dado a cardinalidade entre as tabelas e o relacionamento (muitos para muitos). Portanto, transformou-se leitura em uma tabela cujos atributos são: id_delegacao (chave primária), CPF_administrador (chave estrangeira), CPF_montador (chave estrangeira), id_manual (chave estrangeira). 

## Controladores (Controllers):
Liste os controladores do seu projeto e suas responsabilidades.
Descreva as ações (methods) de cada controlador e seus parâmetros de entrada e saída.
Explique como os controladores interagem com os modelos e views.
## Views (Views):
Liste as views do seu projeto e sua função.
## Infraestrutura:
Descreva os componentes de infraestrutura do seu projeto, como bancos de dados, APIs externas e outras dependências.
Explique como a infraestrutura se integra à arquitetura MVC.
Justifique as escolhas feitas e como elas impactam o projeto.
## Implicações da Arquitetura:
Descreva as implicações da arquitetura em termos de escalabilidade, manutenção, testabilidade e outros aspectos importantes.
