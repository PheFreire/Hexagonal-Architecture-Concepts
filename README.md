Arquitetura Hexagonal: A arquitetura hexagonal é uma arquitetura orientada a núcleo ou seja é uma arquitetura onde toda a regra de negocio: fluxos, estruturas de dados criadas (dataclasses) e assinaturas são isoladas dentro de um núcleo que não possui dependencias.

Mas, oque são dependencias?
Dependencia é toda relação obrigatoria indispensavel entre dois processos no qual um deles não consegue realizar sua funcionalidade sem a existecia do outro.

Um fluxo sem inversão de dependencia possui funcionalidades com implementações estaticas ou seja para que o fluxo funcione a implementação é uma dependencia.
Para um fluxo com inversão de dependencia, a dependencia para de ser a implementação expecifica de uma funcionalidade e passa a se tornar a implementação de alguma funcionalidade que siga os requesitos de uma assinatura especificada.
Ou seja toda implementação é uma dependencia, o design de codigo do fluxo que vai indicar se ela é uma dependencia exclusiva e obrigatoria do fluxo ou uma dependencia dinamica que pode ser injetada no fluxo.
De um jeito ou de outro implementações são dependencia e ponto final.

Um sistema que possui um nucleo sem dependencias é um modelo de desenvolvimento onde seu design possui apenas: estruturas de dados, interfaces e fluxos, estes fluxos desenvolvidos com o principio de inversão de dependencia, não possuem uma dependencia interna, ao invés disso recebem como entrada instancias de interfaces e estas sim possuem dependencias.

Na infraestrutura por outro lado recebemos apenas e unicamente dependencias, ou seja dentro da infrastructura colocamos, migrations, databases, configurações de chamadas de APIs externas, configurações de filas e principalmente acima de tudo: adaptadores de interfaces.

Em um fluxo seus processos internos podem ser categorizados baseados em seu comportamento:

- Provider: 
	Processo que controla dependencias para realizar seu comportamento

- Factory: 
	Processo que tem como objetivo gerar um provider ou uma model

- Repository: 
	Processo de injeção de parametros em outros processos de forma dinamica, onde cada instancia de um mesmo repository injeta parametros diferentes para lidar com processos no qual não apenas os types de seus parametros são dependencias, mas a informação contida desses parametros também. 

	-- Exemplo: Instancias de processos providers de bancos de dados não devem receber apenas uma String como parametro para executar uma query e sim uma String com codigo SQL.

	-- PS: Os repositories recebem como parametro uma instancia de interface.

- Bridges: 
	Processo que possui fluxo de HashMap interno para retorno de instancia de interfaces e dataclasses
	
	-- Exemplo: Ferramentas de injeção de dependencia costuma funcionar através de bridges

Interfaces -> Serviços (Services)
instancias de interfaces -> adaptadores (Adapters)
Dataclasses ou estruturas de dados -> Modelos (Models)
Fluxos -> Casos de uso (Usecases)
Grupos de fluxos -> Controladores (Controllers)
Pontos de entrada http -> Rotas (Routes)
