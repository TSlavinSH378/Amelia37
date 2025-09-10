The 3.7.x version of Amelia includes significant improvements and additions from earlier versions. Consult the [release notes](Release%20Notes) and documentation for details about all changes.
## General
-   Amelia is compatible with Safari (v10), Firefox (v57 Quantum), and Microsoft Edge (v42.17134) AM3-6082, 6089, 6117
-   [Amelia is embedded into the administration pages](Amelia-Basics_11939353.html#AmeliaBasics-AmeliaFlyout) AM3-6463, 6088
## BPNs
-   [New Ask task properties to Suppress cancel on Ask tasks, Domain switch, and define backjump behaviors](BPN-Tasks_11939422.html#BPNTasks-AskTaskProperties) AM3-7150
-   [Backjumps to handle conversation changes instead of stochastic BPNs](BPN-Tasks_11939422.html#BPNTasks-Backjumps) AM3-7181
-   [Undeploy BPNs regardless of dependency order](Process-Memory-Interfaces_11939361.html#ProcessMemoryInterfaces-BPNPropertiesBar) AM3-5944
-   [New annotation tool for BPN Ask and Say tasks, slot questions, and response pool entries](Annotate%20Amelia%20Utterances) AM3-3796, 4734, 4758, 5196, 5195, 5280, 8070
-   [Update and replace Tabular Data table content](Script-Tasks_11939477.html#ScriptTasks-TabularData) AM3-5828, 6681
-   [Copy resource URLs to the clipboard in the Content Manager](BPN-Tasks_11939422.html#BPNTasks-ContentManager) AM3-5018
-   **API allows queries for integration flows and related properties to build a UI AM3-6921**
-   [Amelia can switch to different domains based on conversations if BPNs are set to allow domain switching](BPN-Tasks_11939422.html#BPNTasks-DomainSwitching) AM3-6106
-   [Redesign BPN Properties Bar](Process-Memory-Interfaces_11939361.html#ProcessMemoryInterfaces-BPNPropertiesBar) AM3-7580
## Training
-   Create grammars AM3-4533
-   [Export entities in TSV format and bulk delete spanless entities](Entities-List_11939584.html#EntitiesList-SpanlessEntities) AM3-7072
-   Display last modified data and user in intents and entities AM3-7008
-   Apply preprocessors to control ELMo sensitivity for DNN training AM3-5976
-   Cancel DNN training if needed AM3-7005
-   Display training time estimates and parameters for DNN training AM3-6913, 6158
-   Journey Analytics added to the Analytic Memory AM3-5406, 6897, 6689
-   Improved Clarification Question Answer (CQA) to handle one word responses AM3-5780
-   [Export training corpus in reader-friendly format](Annotate_11939620.html#Annotate-ExportUtterancesTSV) AM3-5939
-   **Added an NLU test pipeline to compare training model performance across model versions AM3-6392, 6553**
-   Amelia learns intents and entities and creates training models based on imported utterances AM3-6396
-   Person datum type extracts titles and name suffixes AM3-5054
-   Added an Expiration Date datum type AM3-5711
-   Improved support for decimal and integer datums AM3-6996
## Integrations
-   [Create and use integration flow templates](Create-an-Integration-Flow_11939847.html#CreateanIntegrationFlow-IntegrationTemplates) AM3-6131
-   [BPN Script tasks can execute integration flows](Integration%20Service) AM3-7731
## Custom User Interface
-   [Individual users can edit and publish individual UI bundles](Deploy%20and%20Publish%20UI%20Bundles) AM3-5464
## Agents/Supervisors
-   **Browser tab notification for agents when Amelia tab doesn't have focus AM3-5567**
## System
-   **Cancel and Go Back dialog acts added to response pools AM3-7114, 7116**
