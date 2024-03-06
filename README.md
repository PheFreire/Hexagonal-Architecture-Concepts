Arquitetura Hexagonal: A arquitetura hexagonal é uma arquitetura orientada a núcleo ou seja é uma arquitetura onde toda a regra de negocio: fluxos, estruturas de dados criadas (dataclasses) e assinaturas são isoladas dentro de um núcleo que não possui dependencias.

Mas, oque são dependencias?
Dependencia é toda relação obrigatoria indispensavel entre dois processos no qual um deles não consegue realizar sua funcionalidade sem a existecia do outro.

Um fluxo sem inversão de dependencia possui funcionalidades com implementações estaticas ou seja para que o fluxo funcione a implementação é uma dependencia.
Para um fluxo com inversão de dependencia, a dependencia para de ser a implementação expecifica de uma funcionalidade e passa a se tornar a implementação de alguma funcionalidade que siga os requesitos de uma assinatura especificada.
Ou seja toda implementação é uma dependencia, o design de codigo do fluxo que vai indicar se ela é uma dependencia exclusiva e obrigatoria do fluxo ou uma dependencia dinamica que pode ser injetada no fluxo.
De um jeito ou de outro implementações são dependencia e ponto final.

Um sistema que possui um nucleo sem dependencias é um modelo de desenvolvimento onde seu design possui apenas: estruturas de dados, interfaces e fluxos desenvolvidos através do principio de inversão de dependencia, ou seja, que recebem como parametro um adapter com uma implementação de forma que elas recebem uma dependencia mas que não possuem uma dependencia interna.

Na infraestrutura por outro lado recebemos apenas e unicamente dependencias, ou seja dentro da infrastructura colocamos, migrations, databases, configurações de chamadas de APIs externas, configurações de filas e principalmente acima de tudo: adaptadores de interfaces.

Services -> Interfaces
Models -> Estruturas de dados
Fluxos -> Usecases
Adaptadores -> Adapters
Groups -> Controllers
Routes -> Pontos de entrada dentro dos entrypoits http
