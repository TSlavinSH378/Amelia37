{% version "3.x" %}
Amelia’s administrative interface provides access to conversation data. Most clients use external systems to satisfy compliance and retention requirements. For example, a full conversation log in a CRM or ITSM ticket where Amelia includes a Pre-Close BPN to ensure the ticket is always up to date. Whenever the conversation UI is not from Amelia, conversation data is by default available in the system the user interacts with. For example, a LivePerson implementation or using Amelia's SDKs and APIs to converse through Skype for Business.
The Java SDK (and soon the REST API) also can retrieve chat data to integrate with third party archiving solutions. IPsoft can provide a sample Java application to retrieve chat data for a specific time period.
> [!warning]  
>
> Metrics and other data stored in Amelia V3 is significantly less than Amelia V2 because execution data is no longer stored long-term in Amelia's database.

If encrypted user utterances stored in Amelia's databases are a problem, utterances can be blanked out after a chat log export is successful. For example, chat data could be exported every hour and, after ensuring conversation data is safely in the archiving solution, user utterances and other relevant data stored in Amelia could be replaced with blanks. This would prevent retrieval from Amelia while maintaining Amelia's statistics. IPsoft can discuss this and other strategies as needed.
{% /version %}
