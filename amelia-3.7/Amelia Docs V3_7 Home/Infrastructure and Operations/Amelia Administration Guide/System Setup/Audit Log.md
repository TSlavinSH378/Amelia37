A wide range of Amelia events can be searched and viewed individually and by event type. To view audit log events for a domain, the user must have the ADMIN_AUDIT_EVENT authority assigned to their user account. For events not connected to a domain, the ADMIN_AUDIT_EVENT authority must be assigned from a group with global authority.
To view events, click the System Settings link on the left side of Amelia's administration pages then click the Audit Log link to display a searchable list of events.
To display details about an audit log event, click the ![](attachments/11940281/28480544.png) icon to the right of any entry in the Event Data column.
![](https://docs.ipsoft.com/download/attachments/25464238/amelia_audit_log_workspace-4.0.jpg)
Figure. Audit Log Entries Workspace
Table. Audit Log Entry Definitions

| Entry | Definition |
| ----|----|
| AUDIT_DATA_CLEANUP | Data cleaned from Amelia database. Event Data displays deletionDate and rowsDeleted. |
| AUTHENTICATION_FAILURE | Authentication failed. Event Data displays Type and failure Message. |
| AUTHENTICATION_POLICY_CREATED | An authentication policy was created. Event Data displays entity with policy details and elements. |
| AUTHENTICATION_POLICY_UPDATED | An authentication policy was updated.; |
| AUTHENTICATION_SUCCESS | User logged in successfully. No Event Data displayed. |
| AUTHENTICATION_SYSTEM_CREATED | An authentication system was created. Event Data displays entity with authentication system details. |
| AUTHENTICATION_SYSTEM_UPDATED | An authentication system was updated. Event Data displays entity with authentication system details. |
| AUTHORIZATION_FAILURE | User failed to log in successfully. Event Data displays Source, Type, and Message. |
| BPN_MODEL_CREATED | A BPN model has been created. Event Data displays entity with details about the BPN. |
| BPN_MODEL_DELETED | A BPN model has been deleted.;Event Data displays entity with details about the BPN. |
| BPN_MODEL_REVISION_CREATED | A BPN model has been revised. Event Data displays entity with details about the BPN revisions. |
| BPN_MODEL_REVISION_DELETED | A BPN model revision has been deleted. |
| BPN_MODEL_REVISION_UPDATED | A BPN model revision has been updated. Event Data displays entity with before and after details about the BPN revision. |
| BPN_MODEL_UPDATED | A BPN model has been updated.;Event Data displays entity with before and after details about the BPN update. |
| BPN_PATH_CREATED | A BPN file folder path has been created. Event Data displays entity with details about the BPN file path. |
| BPN_PATH_DELETED | A BPN file folder path has been deleted. Event Data displays entity with details about the BPN file path. |
| BPN_PATH_UPDATED | A BPN file folder path has been updated. Event Data displays entity with before and after details about the BPN file path. |
| CLASSIFIER_REVISION_APPROVED | A classifier revision has been approved. |
| CLASSIFIER_REVISION_CREATED | A classifier revision has been created. Event Data displays encoderModel with details about the classifier. |
| CLASSIFIER_REVISION_DELETED | A classifier revision has been deleted. |
| CM_BUCKET_CREATED | A bucket folder has been created in the Process Memory > Content Manager. Event Data displays entity with details about the bucket. |
| CM_BUCKET_DELETED | A bucket folder has been deleted in the Process Memory > Content Manager. Event Data displays entity with details about the bucket. |
| CM_BUCKET_UPDATED | A bucket folder has been updated in the Process Memory > Content Manager. Event Data displays entity with before and after details about the bucket. |
| CM_RESOURCE_CREATED | A resource has been created in the Process Memory > Content Manager. Event Data displays entity with details about the resource. |
| CM_RESOURCE_DELETED | A resource has been deleted in the Process Memory > Content Manager. Event Data displays entity with details about the resource. |
| CM_RESOURCE_UPDATED | A resource has been updated in the Process Memory > Content Manager. Event Data displays entity with before and after details about the resource. |
| CONTACT_POINT_DELETED | No longer in use |
| CONTACT_POINT_UPDATED | No longer in use |
| CONTACT_PREFERENCE_DELETED | No longer in use |
| CONTACT_PREFERENCE_UPDATED | No longer in use |
| CONVERSATION_SUMMARY_CLEANUP | The conversation summary cleanup job has been requested by a user. This is also logged by the service once the job completes. In the first case, the information logged is the requester. In the latter it is the outcome of the job (how many rows deleted.) Event Data displays ElapsedTime and TotalSummariesCleaned. |
| CONVERSATION_SUMMARY_EXPORT_DELETED | A conversation export report has been deleted. Event Data displays Report ID and Deleted By. |
| CONVERSATION_SUMMARY_EXPORT_DOWNLOADED | A conversation export report has been downloaded. Event Data displays Downloaded By email address and Report ID. |
| CONVERSATION_SUMMARY_EXPORT_REQUEST | A conversation export report has been requested. Event Data displays Domains, Time Zone, Format, Report ID, From, To, Requested By email address. |
| CORPUS_REVISION_CREATED | A revision to an existing Corpus has been created. Event Data displays revisionId, corpusId, Documents, Name. |
| CORPUS_REVISION_DELETED | No longer in use |
| DOCUMENT_CREATED | A document has been created in the Amelia Trainer > Annotate workspace. Event Data displays entity with details about the document. |
| DOCUMENT_DELETED | A document has been deleted in the Amelia Trainer > Annotate workspace. Event Data displays entity with details about the document |
| DOCUMENT_REVISION_CREATED | A document has been revised in the Amelia Trainer > Annotate workspace. Event Data displays entity with details about the document revision. |
| DOCUMENT_REVISION_DELETED | A revised document has been deleted in the Amelia Trainer > Annotate workspace. Event Data displays entity with details about the deleted document. |
| DOCUMENT_UPDATED | A document has been created in the Amelia Trainer > Annotate workspace. Event Data displays DocumentId. |
| DOMAIN_CREATED | A domain has been created. Event Data displays entity with details about the domain. |
| DOMAIN_UPDATED | A domain has been updated. Event Data displays entity with before and after details about the domain update. |
| ENTITY_DURATION_SUMMARY_CLEANUP | An entity duration summary cleanup has been performed. Event Data displays deletionDate, rowsDeleted, daysRetained, and durationType. |
| ESCALATION_QUEUE_AGENT_UPDATED | An agent assigned to an Escalation Team has changed their status. Event Data displays escalation team, escalation queue, agent id, agent email. |
| ESCALATION_QUEUE_CREATED | An escalation queue has been created.;Event Data displays entity with details about the escalation queue. |
| ESCALATION_QUEUE_DELETED | An escalation queue has been deleted.;Event Data displays entity with details about the escalation queue. |
| ESCALATION_QUEUE_SUPERVISOR_UPDATED | The Exclusive Supervisor Group setting has been updated. |
| ESCALATION_QUEUE_TEAMS_UPDATED | One or more teams have been assigned or removed from an escalation queue. |
| ESCALATION_QUEUE_UPDATED | An escalation queue has been updated.; |
| ESCALATION_TEAM_CREATED | An escalation team has been created.;Event Data displays entity with details about the escalation team. |
| ESCALATION_TEAM_DELETED | An escalation team has been deleted.;Event Data displays entity with details about the escalation team. |
| ESCALATION_TEAM_UPDATED | An escalation team record has been updated.;Event Data displays entity with before and after details about the escalation team. |
| FAQS_DELETED | An FAQ file has been deleted.;Event Data displays Files Deleted. |
| FAQS_DOWNLOADED | An FAQ file has been downloaded.; |
| FAQS_UPLOADED | An FAQ file has been uploaded.;Event Data displays Files Uploaded. |
| FAQ_PAIR_DELETED | An FAQ question and answer pair has been deleted.;Event Data displays entity with details about the FAQ pair. |
| FAQ_PAIR_UPDATED | An FAQ question and answer pair has been updated.;Event Data displays entity with before and after details about the FAQ pair. |
| FAQ_QUESTION_ANSWER_UPDATED | No longer in use |
| GOAL_CREATED | A goal has been created.;Event Data displays intent with before and after details about the goal. |
| GOAL_DELETED | A goal has been deleted.;Event Data displays entity with before and after details about the goal. |
| GOAL_UPDATED | A goal has been updated.;Event Data displays entity with before and after details about the goal. |
| GRAMMAR_ADDED | A grammar has been created.;Event Data displays entity with details about the grammar. |
| GRAMMAR_DELETED | A grammar has been deleted.;Event Data displays entity with details about the grammar. |
| GRAMMAR_TEST_CASE_UPDATED | A grammar test case has been updated.;Event Data displays entity with details about the grammar test case. |
| GRAMMAR_UPDATED | A grammar has been updated.;Event Data displays entity with details about the grammar. |
| HUMANIZATION_RESOURCE_FILE_UPDATED | A new file has been uploaded to the Affective Memory > Humanization > Resources workspace. |
| ONE_DESK_INSTANCE_CREATED | A connection to 1Desk has been created. |
| ONE_DESK_INSTANCE_DELETED | A connection to 1Desk has been deleted. |
| ONE_DESK_INSTANCE_UPDATED | A connection to 1Desk has been updated. |
| ONE_RPA_INSTANCE_CREATED | A connection to 1RPA has been created. |
| ONE_RPA_INSTANCE_DELETED | A connection to 1RPA has been deleted. |
| ONE_RPA_INSTANCE_UPDATED | A connection to 1RPA has been updated. |
| ONE_STORE_INSTANCE_CREATED | A connection to 1Store has been created. |
| ONE_STORE_INSTANCE_DELETED | A connection to 1Store has been deleted. |
| ONE_STORE_INSTANCE_UPDATED | A connection to 1Store has been updated. |
| RESPONSEGROUP_CREATED | A response pool group has been created. Event Data displays entity with details about the response pool group. |
| RESPONSEGROUP_DELETED | A response pool group has been deleted. Event Data displays entity with details about the response pool group. |
| RESPONSEGROUP_UPDATED | A response pool group has been updated. Event Data displays entity with details about the response pool group. |
| RESPONSEPOOLENTRY_CREATED | A response pool entry has been created. Event Data displays entity with details about the response pool entry. |
| RESPONSEPOOLENTRY_DELETED | A response pool entry has been deleted. Event Data displays entity with details about the response pool entry. |
| RESPONSEPOOLENTRY_UPDATED | A response pool entry has been updated. Event Data displays entity with before and after details about the response pool entry. |
| RESPONSEPOOL_CREATED | A response pool has been created. Event Data displays entity with details about the response pool. |
| RESPONSEPOOL_DELETED | A response pool has been deleted. Event Data displays entity with details about the response pool. |
| RESPONSEPOOL_UPDATED | A response pool has been updated. Event Data displays entity with before and after details about the response pool. |
| ROLE_CREATED | A role has been created. Event Data displays entity with details about the role. |
| ROLE_DELETED | A;role has been deleted. Event Data displays entity with details about the role. |
| ROLE_UPDATED | A;role has been updated. Event Data displays entity with before and after details about the role. |
| SCRIPT_LIBRARY_CREATED | A script library has been created. Event Data displays entity with details about the script library. |
| SCRIPT_LIBRARY_DELETED | A;script library has been deleted. Event Data displays entity with details about the script library. |
| SCRIPT_LIBRARY_UPDATED | A;script library has been updated. Event Data displays entity with before and after details about the script library. |
| SCRIPT_PATH_CREATED | A;script folder path has been created. Event Data displays entity with details about the script folder path. |
| SCRIPT_PATH_DELETED | A;script folder path has been deleted. Event Data displays entity with details about the script folder path. |
| SCRIPT_PATH_UPDATED | A;script folder path has been updated. Event Data displays entity with before and after details about the script folder path. |
| SESSION_DESTROYED | All logoffs trigger this audit log entry. Event Data displays session, session_last_access, and session_created. |
| SLOT_CREATED | A slot has been created. Event Data displays entity with details about the slot. |
| SLOT_DELETED | A;slot has been deleted. Event Data displays entity with details about the slot. |
| SLOT_QUESTION_DELETED | A;slot question as been deleted. Event Data displays entity with details about the slot question. |
| SLOT_QUESTION_UPDATED | A;slot question as been updated. Event Data displays entity with details about the slot question. |
| SLOT_UPDATED | A;slot has been updated. Event Data displays entity with details about the slot. |
| SLOT_UTTERANCE_DELETED | A slot utterance has been deleted.;Event Data displays entity with details about the slot utterance. |
| SLOT_UTTERANCE_UPDATED | A slot utterance has been updated.;Event Data displays entity with details about the slot utterance. |
| TABULAR_DATA_COLUMN_CREATED | A column has been added to a tabular data file. Event Data displays entity with details about the column. |
| TABULAR_DATA_COLUMN_UPDATED | A column has been updated in a tabular data file. Event Data displays entity with details about the column. |
| TABULAR_DATA_CREATED | A tabular data file has been created. Event Data displays entity with details about the tabular data file. |
| TABULAR_DATA_DELETED | A;tabular data file has been deleted. Event Data displays entity with details about the tabular data file. |
| TABULAR_DATA_UPDATED | A;tabular data file has been updated. Event Data displays entity with before and after details about the tabular data file. |
| USER_CREATED | A user record has been created. Event Data displays entity with details about the user record. |
| USER_DELETED | A user record has been deleted. Event Data displays entity with details about the user record. |
| USER_EXPIRED | A user record has expired. Event Data displays entity with details about the user record. |
| USER_GROUP_CREATED | A user group has been created. Event Data displays entity with details about the user group. |
| USER_GROUP_DELETED | A user group has been deleted. Event Data displays entity with details about the user group. |
| USER_GROUP_MEMBERS_UPDATED | The members of a user group have been updated. Event Data displays entity with details about the user group. |
| USER_GROUP_UPDATED | A;user group has been updated. Event Data displays entity with before and after details about the user group. |
| USER_MEMBERS_UPDATE | Groups assigned to a user have updated. Event Data displays removedUserGroupIds, addedUserGroupIds, userName, and userId. |
| USER_PASSWORD_UPDATED | The password for a user record has been updated. Event Data displays user. |
| USER_PASSWORD_UPDATE_AUTHENTICATION_FALURE | A user attempting to change their password did not supply their correct current password. Event Data displays user email address. |
| USER_REACTIVATED | A user record has been reactivated. |
| USER_UNLOCKED | A user record has been unlocked. |
| USER_UPDATED | A user record has been updated.;Event Data displays entity with before and after details about the user. |

**More System Settings**
-   [Authentication Systems](Authentication%20Systems)
-   [Authentication Policies](Authentication%20Policies)
-   [Escalation Teams](Escalation%20Teams)
-   [Escalation Queues](Escalation%20Queues)
-   [Domains](Domains)
-   [Groups](Groups)
-   [Users](Users)
-   [Roles](Roles)
-   [Custom UI Bundles](Custom%20UI%20Bundles)
-   [Audit Log](Audit%20Log)
-   [Facial Recognition](Facial%20Recognition)
-   [Response Pools](Response%20Pools)
-   [1Rpa Instances](1Rpa%20Instances)
