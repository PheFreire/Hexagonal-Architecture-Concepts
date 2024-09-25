# Arquitetura Hexagonal 

## Termos importantes
- Interfaces ->  Abstração que define a assinatura de um metodo ou estrutura de dados
- Services -> "Interface" que define a assinatura de um metodo
- Dataclasses | DTOs | Models -> "Interface" que define a assinatura de uma estrutura de dados
- Adapters -> Implementação de um "Service"
- Usecases | Fluxos -> Abstração que integra as assinaturas dos "Services" em um fluxo e define a inversão de dependencia para a injeção dos "Adapters"
- Groups | Controllers ->  Abstração que integra e realiza a injeção de dependencia nos "Usecases" 
- Entrypoints -> Abstração responsavel por definir os gatilhos de ativação dos "Controllers"

## Oque é a arquitetura Hexagonal? 

A arquitetura hexagonal é uma arquitetura orientada a dominio ou seja é uma arquitetura onde toda a regra de negocio e designs de codigo: 
- Usecases (Fluxos)
- Controllers (Grupo de fluxos)
- Dataclasses ou DTOs (Interface/Assinaturas de estruturas de dados)
- Services (Interface/Assinaturas de metodos)
são isoladas com tecnicas de modularização dentro de um nucleo chamado "domain" que não possui dependencias.

## Mas, oque são dependencias?
- Dependencia é toda relação obrigatoria indispensavel entre dois processos no qual um deles não consegue realizar sua funcionalidade sem a existecia do outro.

- Podemos abstrair o conceito de dependencia para afirmar que por exemplo: um script que cria uma conexão com um banco de dados usando um framework de ORM, possui uma dependencia direta com o framework de ORM ultilizado portanto, se este framework estiver internamente retornando um erro o script em questão para de funcionar. 

## Inversão de dependencia
- Todo fluxo que não possui como dependencia a sua implementação de forma estatica, mas sim que recebe sua implementação de forma dinamica como parametro possui oque chamamos de inversão de dependencia

- Um fluxo sem inversão de dependencia possui a implementação de suas funcionalidades de forma estatica tornando sua implementação uma dependencia estatica obrigatoriamente ligada ao fluxo  

- Ou seja toda implementação é uma dependencia, o design de software ultilizado para criar o fluxo que ira indicar se a implementação sera uma dependencia estatica e obrigatoria do fluxo ou uma dependencia dinamica que pode ser injetada dinamicamente como parametro do fluxo.


## Dependencias da arquitetura de dominio
- As dependencias de uma arquitetura hexagonal são contidas por meio de tecnicas de modularização nos "entrypoints" e na "infrastructure"

- No caso da criação de gatilhos que iniciam fluxos no sistema como frameworks de RestAPIs que definem rotas de inicialização dos fluxos, frameworks que mapeam um sensores de arduino e inicializam um fluxo ou qualquer outra ferramenta que possa servir como um gatilho de inicialização de um fluxo do programa englobamos nos "entrypoints" 

- Qualquer implementação que possa ser injetada por meio da injeção de dependencia dentro de um fluxo que ultilize a inversão de dependencia englobamos nos "adapters"


## Categorias de Adapters
- Dependendo da responsabilidade e particularidades de cada adapter, eles pertencem a categorias diferentes 

- Provider: Adapter responsavel por manipular alguma ferramenta não nativa da linguagem

- Factory: Adapter responsavel por gerar ou configurar um adapter provider ou uma instancia de uma dataclass 

- Repository: É o adapter que tem como responsabilidade executar o metodo de um adapter provider injetando como entrada deste, parametros estaticos diferentes. Isso é necessario pois existem providers que além de possuir sua implementação como dependencia, possui uma lista estatica e limitada de possiveis parametros de entrada para que algum processo expecifico funcione corretamente        

	- Exemplo: Providers que executam querys no bancos de dados não podem receber apenas uma String qualquer como parametro, suas possiveis entradas são limitadas a receber apenas strings com codigo SQL. Sendo assim podemos ter um repository referente a tabela usuario do banco de dados que possui o metodo "get_user_by_email" e receber como parametro uma string referente a um "email" e o adapter provider que realiza querys dentro do banco de dados  

- Bridges: Adapter que tem como responsabilidade, assim como uma factory retornar um adapter ou instancias de dataclass, mas que diferente da factory dependendo do valor de entrada da bridge, retorna valores diferentes. Ou seja a bridge faz a troca direta de um parametro de entrada (geralmente string) por um outro adapter ou instancia de dataclass
	
	- Exemplo: Adapters de injeção de dependencia que convertem "strings" correspondentes a um adapter por uma instancia do adapter são Bridges

