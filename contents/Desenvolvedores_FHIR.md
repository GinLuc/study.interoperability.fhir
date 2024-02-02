# Desenvolvimento em FHIR

Do ponto de vista de desenvolvimento, FHIR foi desenvolvido para prover uma estrutura de informação de modo fornecer suporte em sistemas clínicos. Sua especificação garante amplamente o uso das práticas em RESTFul para permitir seu provisionamento em sistemas clínicos integrados entre uma larga escala de times e organizações.

O escopo do FHIR é amplo e diverso, projetado para uso global e em uma gama alta de arquiteturas e cenários, cobrindo desde aspectos clínicos humanos até veterinários: cuidado clínico, saúde pública, triagens clínicas e até aspectos financeiros e administrativos. 

## *Framework*

FHIR é baseado em estruturas denominadas *Resources*, ou Recursos, para o tráfego de informações. Elas são uma representação em nível de instância de uma entidade presente no ambiente clínico, sendo todos os Recursos tendo as seguintes características em comum (para representação visual, veja o tópico [Composição de um Recurso](./Introducao_FHIR#composicao-recurso)):
* Uma identificação única de Recurso: usualmente uma URL que define onde o Recurso é encontrado;
* um conjunto de metadados;
* um sumário com informações do Recurso em formato XHTML;
* um conjunto de elementos de dados previamente definidos, diferenciando-os de acordo com o Recurso;
* uma *framework* extensiva para suportar as variações dos sistemas clínicos;

Os Recursos são representados nos formatos XML, JSON ou RDF, sendo presentes [145 tipos diferentes na versão R4](http://hl7.org/fhir/R4/resourcelist.html) de especificação do protocolo.

**OBS.:** esta especificação descreve um conjunto de Recursos, ou seja, um conjunto de tipo de Recursos que descreve o conjunto das instâncias de Recursos que podem ser trafegadas. Ás vezes, o termo "Recurso" é utilizado sem esclarecer explicitamente se está sendo abordado seus tipos ou as instâncias propriamente ditas, sendo o contexto de uso deixando isso claro. 

### Examplo de Instância de um Recurso

Exemplo de como um Recurso do tipo *Patient* é trafegado na rede, no formato JSON:
```
{
	"resourceType": "Patient",
	"id" : "23434",
	"meta" : {
		"versionId" : "12",
		"lastUpdated" : "2014-08-18T15:43:30Z"
	}
	"text": {
		"status": "generated",
		"div": "<!-- Snipped for Brevity -->"
	},
	"extension": [
		{
		  "url": "http://example.org/consent#trials",
		  "valueCode": "renal"
		}
	],
	"identifier": [
		{
		  "use": "usual",
		  "label": "MRN",
		  "system": "http://www.goodhealth.org/identifiers/mrn",
		  "value": "123456"
		}
	],
	"name": [
		{
		  "family": [
			"Levin"
		  ],
		  "given": [
			"Henry"
		  ],
		  "suffix": [
			"The 7th"
		  ]
		}
	],
	"gender": {
		"text": "Male"
	},
	"birthDate": "1932-09-24",
	"active": true
}
```

Como falado anteriormente, cada instância de um Recurso (registro de dado) consiste em: 
1. **resourceType** (obrigatório): define o tipo de Recurso em questão;
2. **id**: id desta instância de Recurso, sendo sempre presente durante o tráfego de dados, exceto durante a operação de criação (ver tópico [Criação de Registros]());
3. **meta** (geralmente presente, porém opcional): representado pelo Recurso [Metadata](http://hl7.org/fhir/R4/resource.html#meta), nele apresenta todos os tipos de metadados relacionados à instância em questão;
4. **text**(recomendado, porém opcional): informações descritivas em formato XHTML da instância;
5. **extension**(puramente opcional): conjunto de [Extensions](http://hl7.org/fhir/R4/extensibility.html) para prover a capacidade de extensão de um recurso;
6. **data**(puramente opcional): conjunto dos elementos de dados onde são inseridos os dados relacionados ao Recurso.


### URLs e Identificadores
Todos os recursos possuem uma URL que os identificam (seus tipos) e especifica da onde estão sendo acessados. Essa URL não é representada dentro do recurso, sendo utilizada em uso contextual, e mudada conforme surgem cópias dos recursos (perfis), ou por qualquer outra mudança em desenvolvimento/segurança. Se a URL for acessada via API RESTful, então a estrutura dela fica `[base]/[resourceType]/[id]`, sendo o `resourceType` e o `id` adquiridos de dentro do recurso.

