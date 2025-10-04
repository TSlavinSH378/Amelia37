{% version "3.x" %}
-   <a href="#SemnetConfiguration-ThresholdforSemnet" data-idon'tknow"response"="">Threshold for Semnet "I don't know" response</a>
-   <a href="#SemnetConfiguration-ThresholdforDocumentQA" data-idon'tknow"response"="">Threshold for Document QA "I don't know" response</a>
-   <a href="#SemnetConfiguration-ThresholdforFAQ" data-idon'tknow"response"="">Threshold for FAQ "I don't know" response</a>
Table. Semnet Configuration Properties

| Property | Default Setting | Description |
| ----|----|----|
| Whether to return short answer | Selected/True | Can be toggled to return either the short answer or the entire relevant fact |
| Threshold for Semnet "I don't know" response | 0.6 | Minimum entailment score for semnet to respond with the answer it computes. Reduce this if you get frequent "I don't know" responses from semnet responder. |
| Number of lucene results in Document QA | 5 | The number of results that Lucene retrieves from the index. Increase this if you get frequent; "I don't know" responses from document QA responder. |
| Threshold for paragram in Document QA | 0.65 | Minimum paragram similarity score for document QA to respond with the answer it computes.;Reduce this if you get frequent "I don't know" responses from document QA responder. |
| Threshold for paragram in tables in;Document QA | 0.6 | Minimum paragram similarity score for document QA to respond with the answer it computes if the answer is in a table.;Reduce this if you get frequent "I don't know" responses from document QA responder when the expected answer is in table. |
| Threshold for Document QA "I don't know" response | 0.45 | Minimum entailment score for document to respond with the answer it computes. Reduce this if you get frequent "I don't know" responses from document QA responder. |
| Threshold for FAQ "I don't know" response | 0.6 | Minimum entailment score for FAQ to respond with the answer it computes. Reduce this if you get frequent "I don't know" responses from FAQ responder. |
| Number of lucene results in FAQ responder | 10 | The number of results that Lucene retrieves from the index. Increase this if you get frequent; "I don't know" responses from document FAQ responder. |
| Low threshold for entailment score in FAQ responder | 0.6 | Minimum bidaf similarity score for FAQ responder to respond with the answer it computes.;Reduce this if you get frequent "I don't know" responses from FAQ responder. |
| High threshold for entailment score in FAQ responder | 0.8 | Minimum entailment similarity score for FAQ responder to respond with the answer it computes.;Reduce this if you get frequent "I don't know" responses from FAQ responder. |
| Low threshold for paragram similarity in FAQ responder | 0.6 | Minimum paragram similarity score for FAQ responder to respond with the answer it computes.;Reduce this if you get frequent "I don't know" responses from FAQ responder. |
| High threshold for paragram similarity in FAQ responder | 0.8 | Answer computed by the FAQ responder is returned directly without rechecking with bidaf and entailment score if the paragram score is above this threshold. |
| Number of cluster size in FAQ responder | 1 | If the number of questions present in the cluster is greater than this threshold then the answer corresponding the cluster is returned. |
| Knn threshold for paragram similarity in FAQ responder | 0.7 | Minimum paragram similarity score for a document to be a part of the cluster.;Reduce the score if you get frequent "I don't know" responses from FAQ responder. |
| Threshold on entailment score for highest sum match | 0.9 | Paragram similarity score and entailment similarity score are added and the document with highest sum is returned if the entailment score of the document is greater than this threshold. Reduce the score if you get;frequent "I don't know" responses from FAQ responder. Very low value for this threshold will make the FAQ responder return answers for all the queries including casual chats and common queries. |

{% /version %}
