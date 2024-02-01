# Introdução ao FHIR

* O que é FHIR?
	* *Fast Healthcare Interoperability Resources*, sendo uma *framework* de padrão para o tráfego de dados via cliente-servidor, com alto foco na implementação, desenvolvido pela HL7.
	* Contém as melhores *features* das *frameworks* HL7's [v2 ![](http://hl7.org/fhir/R4/external.png)](http://www.hl7.org/implement/standards/product_brief.cfm?product_id=185) , [HL7 v3 ![](http://hl7.org/fhir/R4/external.png)](https://www.hl7.org/implement/standards/product_brief.cfm?product_id=186) e [CDA](http://www.hl7.org/implement/standards/product_brief.cfm?product_id=7)
	* Suas soluções são compostas por um conjunto de componentes denominados Recursos (*Resources*), os quais podem ser integrados a fim de formar sistemas (denominados como Sistemas de Interoperabilidade) que resolvem problemas clínicos e administrativos reais com baixo custo operacional. 
	* Pode ser usado para várias aplicações: aplicativos *mobiles*, comunicações em nuvem, compartilhamento de dados baseado em *Eletronic Health Record*(EHR), comunicação de servidores em grandes provedores *healthcare*, entre outros. 
* Por que FHIR é melhor?
	* Alto foco em implementação, onde torna-se mais fácil de implementá-lo
	* Múltiplas bibliotecas de implementação, com diversos exemplos disponíveis para rápido desenvolvimento
	* Sua especificação é completamente gratuita para uso
	* Conceito de "Interoperabilidade fora-da-caixa": os recursos base podem ser usado como são, mas também podem ser adaptados quanto necessários através de perfis (*Profiles*), extensões (*Extensions*), terminologias (*Terminologies*), etc.
	* Graças ao processo de desenvolvimento evolucionário com o HL7 v2 e CDA, eles são capazes de coexistir e apoiar um ao outro.
	* Fortemente fundado nos padrões *Web*: XML, JSON, HTTP, OAuth, etc.
	* Possui suporte para arquiteturas RESTful (transferência contínua de dados usando mensagens ou documentos) e arquiteturas baseadas em serviços (*service-based architectures*)
	* Especificações concisas e de fácil entendimento
	* Possui um componente de descrição dentro das especificações (*human-readable serialization format*) de modo que facilita o entendimento por parte dos desenvolvedores 
	* **Em desenvolvimento:** análise baseada em ontologias com mapeamento formal para correções semânticas
* Flexibilidade/Adaptação
	* Um dos grandes desafios para padrões em saúde é lidar com a vasta variabilidade causada pelos diversos processos clínicos: ao longo do tempo, são adicionados campos e opções são adicionados à especificação, gradualmente aumentando custo e complexidade para as implementações resultantes.
		* Uma alternativa é utilizar extensões customizadas, porém cria-se problemas para a implementação também (ex.: deve-se garantir que o sistema seja capaz de pegar este dado, bem como que tal extensão esteja em todos os sistemas, além deve-se verificar se, a cada nova atualização, a extensão ainda está contemplada)
	* o FHIR resolve este problema através da definição de uma *framework* simples para extensão dos recursos existentes e descrição dos seus usos chamado *Profiles* (processo de perfilização dos modelos). 
		* Todos os sistemas são capazes de ler recursos, mas as aplicações podem adicionar mais controle e significado com o uso dos perfis, principalmente que muitos estabelecimentos de saúde requerem diversas definições internas

## Composição de um Recurso
 
 ![Exemplo de registro de Paciente](./images/patient_resource_example.png)
* ***"Resource Identity & Metadata:"*** parte referente aos dados de identificação  (atributo *id*) e metadados do recurso usado.
* ***"Human Readable Summary:"*** parte referente à descrição narrativa do recurso, para entendimento dos desenvolvedores, no formato HTML.
* ***"Extension with URL to definition:"*** parte onde é inserida uma extensão ao modelo (ver tópico **Extensões em FHIR**)
* ***"Standard Data:"*** Parte referente aos dados em formato padronizados a serem trafegados (ver tópico **Estrutura de Dados em FHIR**)

## Referências

* [FHIR R4 Official Documentation](http://hl7.org/fhir/R4/index.html)
* [EHR e EMR: O que você precisa saber sobre os registros eletrônicos de saúde](https://prontuarioverde.com.br/blog/medicina/ehr-e-emr/)