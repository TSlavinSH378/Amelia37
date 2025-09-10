-   [Arbitration](#ApplicationConfigurationProperties-Arbitration)
-   [BPN](#ApplicationConfigurationProperties-BPN)
-   [Episodic](#ApplicationConfigurationProperties-Episodic)
-   [Humanization](#ApplicationConfigurationProperties-Humanization)
This page describes the application configuration properties organized by subsystem.
# Arbitration

| Module | Name | Default | Applicable Values | Description |
| ----|----|----|----|----|
| amelia-engine-service | amelia.engine.subsystem-timeouts-ms.direct-escalation

\| 5000 \| unit in milliseconds \| Timeout for direct escalation \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.logic-net
\| 5000 \| unit in milliseconds \| Timeout for logic net \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.bpn
\| 300000 \| unit in milliseconds \| Timeout for BPN \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.deep-dm
\| 5000 \| unit in milliseconds \| Timeout for Episodic \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.semnet-faq
\| 5000 \| unit in milliseconds \| Timeout for Semnet FAQ \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.semnet
\| 5000 \| unit in milliseconds \| Timeout for Semnet \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.semnet-document
\| 5000 \| unit in milliseconds \| Timeout for Semnet Document \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.inbound-positive-response
\| 5000 \| unit in milliseconds \| Timeout for inbound positive response \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.chit-chat
\| 5000 \| unit in milliseconds \| Timeout for chit chat \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.social-talk
\| 5000 \| unit in milliseconds \| Timeout for social talk \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.acknowledge-default
\| 5000 \| unit in milliseconds \| Timeout for acknowledge default \| \| amelia-engine-service \|
    amelia.engine.subsystem-timeouts-ms.dont-know-default
\| 5000 \| unit in milliseconds \| Timeout for don't know acknowledge default \| \| amelia-engine-service \|
    amelia.engine.max-message-processing-secs
\| 9000 \| unit in seconds \| Maximum time allocated for processing a request \| \| amelia-engine-service \|
    amelia.context.wait-limit
\| 2 \| Integer \>= 0 \| Number of times Amelia will wait for a context change before asking if the user wants to continue their current context \| \| amelia-engine-service \|
    amelia.context.stuck-limit
\| 2 \| Integer \>= 0 \| Number of times Amelia will tolerate unhandled user utterance before escalating. \| \| amelia-engine-service \|
    amelia.goal-slot-process.max-sentences
\| 3 \| Integer \| maximum sentences a goal or slot processing will take place \| \| amelia-engine-service \|
    event.domain-updated.replication-wait.sleep-interval-millis
\| 1000 \| \| \| \| amelia-engine-service \|
    event.domain-updated.replication-wait.wait-intervals
\| 6000 \| \| \| \| amelia-engine-service \|
    amelia.conversation.keep-alive.seconds
\| 3600 \| unit in seconds \|
    How long an acking session will be kept alive without an inbound utterance
\| \| amelia-engine-service \|
    amelia.conversation.ack-timeout.seconds
\| 60 \| unit in seconds \| How long allow an ack response to come back assuming that the session is dead \| \| amelia-engine-service \|
    amelia.conversation.ack-frequency.seconds
\| 180 \| unit in seconds \| Roughly how often to send acks . Must be greater than
    amelia.job.check-sessions-frequency.seconds
\| \| amelia-engine-service \|
    amelia.job.check-sessions-frequency.seconds
\| 30 \| \|
\|
# BPN

| Module | Name | Default | Applicable Values | Description |
| ----|----|----|----|----|
| amelia-admin-web | amelia.bpn_admin_service.validation.rules.ask_task.enabled

\| true \| true, false \| Enable/Disable validation on ask task, including both slot based ask and response based ask \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.dynamic_task_name.enabled
\| true \| true, false \| Enable/Disable validation on all user task whose name contains expression like "${expression_body}" \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.edge_basic.enabled
\| true \| true, false \| Enable/Disable validation on all edges for basic check \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.edge_expression
\| true \| true, false \| Enable/Disable validation on all edges expression check \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.escalate_task.enabled
\| true \| true, false \| Enable/Disable validation on escalate task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.model_element.enabled
\| true \| true, false \| Enable/Disable validation on all task model element check \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.model_type.enabled
\| true \| true, false \| Enable/Disable validation on model type check, namely 'Deterministic', 'Stochastic' and 'Headless' \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.present_task.enabled
\| true \| true, false \| Enable/Disable validation on present task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.request_task.enabled
\| true \| true, false \| Enable/Disable validation on request task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.run_integration_flow.enabled
\| true \| true, false \| Enable/Disable validation on 'run the integration flow' task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.run_workflow.enabled
\| true \| true, false \| Enable/Disable validation on 'run the workflow' task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.say_task.enabled
\| true \| true, false \| Enable/Disable validation on say task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.send_task.enabled
\| true \| true, false \| Enable/Disable validation on send task, including both 'send the integration messge' and 'send form for' tasks \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.set_task.enabled
\| true \| true, false \| Enable/Disable validation on set task \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.task_expression
\| true \| true, false \| Enable/Disable validation on all user task whose name contains expression like "${expression_body}" \| \| amelia-admin-web \|
    amelia.bpn_admin_service.validation.rules.unset_task.enabled
\| true \| true, false \| Enable/Disable validation on unset task \| \| amelia-tabular-service \|
    amelia.tabular.data.directory
\|
    #{systemProperties
    ['java.io.tmpdir']}
    /tabularData
\| any location in system where the tabular data resides \| any location in system where the tabular data resides \| \| amelia-tabular-service \|
    max_upload_file_size
\|
    20971520L
\|
maximum file size
    20971520L
\| File size of the tabular services \| \| amelia-tabular-service \|
    max_tables_in_cache
\| 20 \| maximum tables in cache 20 \| Number of tables in cache \| \| amelia-bpn-engine \|
    amelia.bpn.max-consecutive-task-execution-attempts
\| 2 \| 1-10 \| Maximum number of attempts at executing an ask task before Amelia escalates. \| \|
amelia-admin-web
amelia-engine-service
\|
    amelia.bpn.groovy.sandbox.enabled
\| true \| true, false \| Whether or not security is enabled for Groovy script tasks and libraries. \| \| amelia-admin-web \| amelia.bpn_admin_service.validation.rules.script_task_validation.enabled \| true \| true, false \| enable/disable validation of scripts for errors in script task \| \| amelia-admin-web \| amelia.bpn_admin_service.validation.rules.script_task_syntax_validation.enabled \| true \| true, false \| enable/disable validation of scripts for errors in script task \| \| amelia-engine-service \|
    amelia.bpn.learning.record
\| true \| true, false \| Whether or not learned BPN models are being recorded during a conversation. Setting this property to false is equivalent to disabling BPN learning and disables a Close Conversation popup that can appear when BPN learning is enabled. \| \|
amelia-engine-service
amelia-user-web
amelia-admin-web
\|
amelia.cm.object.chunk.size
\| 2097152 \| unit in bytes \| Content management object chunk size for streaming \| \| amelia-engine-service \| amelia.file.maxsize \| 209715200 \| unit in bytes \| Maximum upload/download file size of the "cmService" \| \| amelia-engine-service \| amelia.download.url.prefix \| /Amelia/api/cm \| URL of amelia-user-web plus "api/cm" (relative URL of CM api) \| URL prefix to get a CM resource \| \| amelia-user-web \| amelia.cm.object.chunk.streaming.timeout \| 2 \| unit in minutes \| Waiting timeout of a CM object chink streaming \| \| amelia-admin-web \| amelia.bpn_admin_service.validation.rules.script_task_syntax_validation.enabled \| true \| true, false \| enable/disable validation of scripts for errors in script task \|
# Episodic

| Module | Name | Default | Application values | Decription |
| ----|----|----|----|----|
| amelia-model-server | model.serving.service.cache.size

\| 100 \| 1-100 \| Number of models (ThoughtVector and CLSTM ) that are served at a time \| \| amelia-model-server \|
    model.serving.service.cache.expire.after.access
\| 60 \| 1-60 \| \| \| amelia-model-server \|
    model.serving.service.newest.version.update.frequency
\| 10 \| Time in seconds \| Interval at which the new model is uploaded in cache after it is deployed \| \| amelia-model-server \|
    model.serving.service.cache.refresh.frequency
\| 60000 \| Time in milliseconds \| Cache refresh frequency \|
# Humanization

| Module | Name | Default | Application Values | Description |
| ----|----|----|----|----|
| amelia-humanization-core | amelia.humanization.hand-flick-nvbg-enabled

\| true \| true, false \|
    Enables/Disable for hand gesture 
\| \|
amelia-humanization-core
\|
    amelia.humanization.punctuation-nvbg-enabled
\| true \| true, false \|
    Enables/Disable for eye brow gesture for clauses that ends with ! and ?
\| \|
amelia-humanization-admin-service
\|
    amelia.humanization.admin.resource.reload_period.minutes
\| 5 \| Time in minutes \| Time for reloading humanization resource in minutes \| \|
amelia-humanization-core
\|
    amelia.humanization.prosody-enabled
\| true \| true \| Enables/Disable the prosody (pitch, loudness etc) of voice \| \|
amelia-humanization-core
\|
    amelia.humanization_resource.reload_period
\| 60 \| Time in seconds \| Time for loading and update humanization resources in every domain \| \|
amelia-humanization-core
\|
    amelia.humanization_resource.test_mode
\| false \| true, false \| Enable/Disable to indicate whether it is running in test mode to avoid reloading \| \|
amelia-humanization-core
\|
    amelia.humanization.question-nvbg-enabled
\| true \| true, false \| Enable/Disable for hand gesture for questions \| \|
amelia-humanization-core
\|
    amelia.humanization.smile-nvbg-enabled
\| true \| true, false \| Enable/Disable for smile or head nod \| \|
amelia-humanization-core
\|
    amelia.humanization.hand-point-nvbg-enabled
\| true \| true, false \| Enable/Disable for handgestures for poiting \| \|
amelia-humanization-core
\|
    amelia.humanization.head-nod-nvbg-enabled
\| true \| true, false \| Enable/Disable for head nod on words. phrases or sentences \| \|
amelia-humanization-core
\|
    amelia.humanization.head-sweep-nvbg-enabled
\| true \| true, false \| Enable/Disable for head sweep on words. phrases or sentences \| \|
amelia-humanization-core
\|
    amelia.humanization.affective-facial-expression-nvbg-enabled
\| true \| true, false \| Enable/Disable for facial expression \| \|
amelia-humanization-core
\|
    amelia.humanization.faceshift-reset-nvbg-enabled
\| true \| true, false \| Enable/Disable for facial expression reset \| \|
amelia-humanization-core
\|
    amelia.humanization.negation-nvbg-enabled
\| true \| true, false \| Enable/Disable for negation hand gesture \| \|
amelia-humanization-core
\|
    amelia.humanization.blink-nvbg-enabled
\| true \| true, false \| Enable/Disable for blinks \| \|
amelia-humanization-core
\|
    amelia.humanization.confusion-nvbg-enabled
\| true \| true, false \| Enable/Disable for confusion gesture \| \|
amelia-humanization-core
\|
    amelia.humanization.brow-nvbg-enabled
\| true \| true, false \| Enable/Disable for eye brow raise for Negation, Affirmation, Question, Greeting etc \| \|
amelia-humanization-core
\|
    amelia.humanization.head-shake-nvbg-enabled
\| true \| true, false \| Enable/Disable Head shakes to BML object \| \|
amelia-humanization-core
\|
    amelia.humanization.comparison-nvbg-enabled
\| true \| true, false \| Enable/Disable Hand gesture for comparision \| \|
amelia-humanization-core
\|
    amelia.humanization.gaze-nvbg-enabled
\| true \| true, false \| Enable/Disable Gaze behavior \| \|
amelia-humanization-core
\|
    amelia.humanization.idle-face-nvbg-enabled
\| true \| true, false \| Enable/Disable Idle behavior \| \|
amelia-humanization-core
\|
    amelia.humanization.head-movement-nvbg-enabled
\| true \| true, false \| Enable/Disable for head movement for Contrast, Response_Request, Word Search,Interjection, Question, Pointing \| \|
amelia-humanization-core
\|
    amelia.humanization.hand-iconic-nvbg-enabled
\| true \| true, false \|
Enable/Disable for
    A nonverbal behavior generator which generates 
    iconic hand gestures based on the following rules:
    (1) If OBJECT, show a hand flick (beat) gesture on word.(2) If ACTION, show a hand flick (beat) gesture on word.
\| \|
amelia-humanization-core
\|
    amelia.humanization.contrast-nvbg-enabled
\| tue \| true, false \| Enable/Disable for hand constrast gestures when we have have two part constrasts
\| \|
amelia-humanization-positive-response
\|
    amelia.humanization.emoticon-enabled
\| true \| true,false \| Enable/Disable for emoticon \| \|
amelia-humanization-positive-response
\|
    amelia.humanization.rule-based-positive-response-enabled
\| true \| true/false \| Enable/Disable for rule based psotive response \| \|
amelia-humanization-positive-response
\|
    amelia.humanization.escalation.enabled
\| true \| true/false \| Enable/Disable for human escalation \| \|
amelia-humanization-positive-response
\|
    amelia.humanization.escalation.low-satisfaction-threshold
\| -0.60 \| negative decimal \| Mentions the threshold for low satisfaction \|
