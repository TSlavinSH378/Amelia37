{% version "3.x" %}
Amelia's ability to detect intent makes her more than an FAQ engine matching common words and phrases to pre-defined answers. While Amelia can deliver FAQs, she includes a diverse set of decision-making dialog systems to analyze utterances, evaluate inputs, then generate scored results to help determine her responses. These dialog systems help Amelia understand intent, especially when classifiers are used to generate many possible utterance variations tied to a specific intent and goal.
Training Amelia is a mix of providing data for Amelia to determine user intent and defining process flows for her to follow based on how conversations might evolve.
For example, to handle conversations about password resets, training Amelia involves creating possible utterances and other data related to how people ask to reset a password and specific steps Amelia should take to reset a password. Possible utterances are collected along with chats and other data then used to train Amelia by creating a conceptual model she uses to recognize password reset requests. Business Process Networks (BPNs) are used to define steps for her to take to reset a password.
The specific elements used to train Amelia include annotated models, entities (slot goals in Amelia V2), intents (goals in Amelia V2), BPNs, classifiers, and FAQs.
-   **Classifiers** connect many possible user utterances to one or more goals and FAQ questions and answers.
-   Pre-existing chat conversations, classifiers, and other data sources are used to create **annotated models** to train Amelia.
-   **Entities** capture key data Amelia needs to complete her tasks and can be referenced in one or more BPNs.
-   **Intents** can connect specific user phrases and responses from Amelia to confirm entities or call a BPN.
-   **BPNs** are process flows used to define how Amelia completes all or part of a user-requested task.
{% /version %}
