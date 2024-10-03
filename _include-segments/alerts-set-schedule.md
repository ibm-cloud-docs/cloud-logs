## Set a schedule and what log content to include
{: step}
{: #alerts-config-6}


Complete the following steps:

1. In the *Schedule* section, set a Schedule to control when this alert is enabled. You can choose specific days and times.

2. In the *Notification Content* section, define whether you want to include a sample log line or only some fields in the event that is triggered.

    Choose specific JSON keys to include in the alert notification, or leave this blank to include the full log text in the alert message:

    - Option 1: Leave blank to include one log line that matches the filtering conditions of the alert.

    - Option 2: Specify JSON keys to include selected fields in the format of key:value pairs. Notice that to be able to add fields, your log records must be in JSON format.

    - Option 3: Specify a  JSON path as the filter.
    
