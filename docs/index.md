# Continuous Intelligence

This site provides documentation for this project.
Use the navigation to explore module-specific materials.

## How-To Guide

Many instructions are common to all our projects.

See
[⭐ **Workflow: Apply Example**](https://denisecase.github.io/pro-analytics-02/workflow-b-apply-example-project/)
to get these projects running on your machine.

## Project Documentation Pages (docs/)

- **Home** - this documentation landing page
- **Project Instructions** - instructions specific to this module
- **Glossary** - project terms and concepts

## Custom Project

### Dataset
added more data to the data set.

### Signals
Error Rate = errors / requests
Avg Latency = total_latency_ms / requests
System State based on thresholds

### Experiments
Lowering the max error rate threshold from 0.05 to 0.005 and the max average latency from 40.0 to 20.0 resulted in the system state changing from stable to degraded. This indicates that while the system metrics were previously within acceptable limits, they now exceed the stricter thresholds, triggering a degraded state.


### Results
Resulted the same but some of the caculations were different becasue of the extra data.

### Interpretation
The system performs fine under normal thresholds but struggles under stricter ones, meaning it may need optimization for high-performance scenarios.
## Additional Resources

- [Suggested Datasets](https://denisecase.github.io/pro-analytics-02/reference/datasets/cintel/)
