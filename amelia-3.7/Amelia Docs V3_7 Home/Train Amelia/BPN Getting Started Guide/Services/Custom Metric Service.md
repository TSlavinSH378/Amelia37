{% version "3.x" %}
Allows BPN Script tasks to save conversation level custom metrics.  Custom metrics can be saved, updated, deleted and retrieved from any BPN throughout the conversation.  
The metrics will be persisted and included in the export report, available from the Export Conversations tab in the Admin UI on the Metrics page.
The service is exposed to script tasks by the name:  customMetricService 
Available since: 3.5.4
# Operations
## upsertMetric
    void upsertMetric(String name, String value)
Save or update a custom metric value for the conversation.

| Parameter | Definition |
| ----|----|
| name | The name of the metric |
| value | The value of the metric |

## deleteMetric
    void deleteMetric(String name)
Delete a previously saved custom metric value.

| Parameter | Definition |
| ----|----|
| name | The name of the metric |

## getMetric
    String getMetric(String name)
Retrieve a previously saved custom metric value. Returns the metric value or null if it does not exist.

| Parameter | Definition |
| ----|----|
| name | The name of the metric |

## getAllMetrics
`Map<String, String> getAllMetrics()`
Returns a map of all custom metrics currently saved for the current conversation.
# Examples
    def trained_performance = transientVariableService.getVariable("trained_performance")
    customMetricService.upsertMetric("trained_performance", trained_performance.toString())
    customMetricService.upsertMetric("resolution", "1")
    customMetricService.upsertMetric("path", "positive path")
    transientVariableService.addVariable("goals",0)
    def goals = transientVariableService.getVariable("goals")
    customMetricService.upsertMetric("goals", goals.toString())
{% /version %}
