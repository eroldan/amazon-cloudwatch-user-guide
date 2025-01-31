# Creating a CloudWatch alarm based on a metric math expression<a name="Create-alarm-on-metric-math-expression"></a>

To create an alarm based on a metric math expression, choose one or more CloudWatch metrics to use in the expression\. Then, specify the expression, threshold, and evaluation periods\.

You can't create an alarm based on the **SEARCH** expression\. This is because search expressions return multiple time series, and an alarm based on a math expression can watch only one time series\.

**To create an alarm based on a math expression**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Alarms**, **All alarms**\.

1. Choose **Create alarm**\.

1. Choose **Select Metric**\.

1. \(Optional\) If you have enabled cross\-account functionality in the CloudWatch console and the current account is a monitoring account, under **Search Metrics** choose choose a different AWS account that contains the metric that you want the alarm to watch\. For more information, see [Cross\-account cross\-Region CloudWatch console](Cross-Account-Cross-Region.md)\.

   You can create cross\-account alarms, but not cross\-Region alarms\.

1. Choose **Select Metric** and do one of the following:
   + Choose the service namespace that contains a specific metric\. Continue choosing options as they appear to narrow the choices\. When a list of metrics appears, select the check box next to the right metric\.
   + In the search box, enter the name of a metric, dimension, or resource ID and press Enter\. Choose one of the results and continue until a list of metrics appears\. Select the check box next to the right metric\. 

   \(Optional\) To add another metric to use in the math expression, under **All metrics**, choose **All**, find the specific metric, and then select the check box next to it\. You can add up to 10 metrics\.

1. Choose **Graphed metrics**\. For each metric added, do the following:

   1. Under **Statistic**, choose one of the statistics or predefined percentiles, or specify a custom percentile \(for example, **p95\.45**\)\.

   1. Under **Period**, choose the evaluation period for the alarm\. When evaluating the alarm, each period is aggregated into one data point\.

      You can also choose whether the y\-axis legend appears on the left or right while you're creating the alarm\. This preference is used only while you're creating the alarm\.

1. Choose **Add a math expression**\. A new row appears for the expression\.

1. On the new row, under the **Details** column, enter the math expression and press Enter\. For information about the functions and syntax that you can use, see [Metric math syntax and functions](using-metric-math.md#metric-math-syntax)\.

   To use a metric or the result of another expression as part of the formula for this expression, use the value shown in the **Id** column: for example, **m1\+m2** or **e1\-MIN\(e1\)**\.

   You can change the value of **Id**\. It can include numbers, letters, and underscores, and it must start with a lowercase letter\. Changing the value of **Id** to a more meaningful name can also make the alarm graph easier to understand\. 

1. \(Optional\) Add more math expressions, using both metrics and the results of other math expressions in the formulas of the new math expressions\.

1. When you have the expression to use for the alarm, clear the check boxes to the left of every other expression and every metric on the page\. Only the check box next to the expression to use for the alarm should be selected\. The expression that you choose for the alarm must produce a single time series and show only one line on the graph\. Then choose **Select metric**\.

   The **Specify metric and conditions** page appears, showing a graph and other information about the math expression that you have selected\.

1. For **Whenever *expression* is**, specify whether the expression must be greater than, less than, or equal to the threshold\. Under **than\.\.\.**, specify the threshold value\.

1. Choose **Additional configuration**\. For **Datapoints to alarm**, specify how many evaluation periods \(data points\) must be in the `ALARM` state to trigger the alarm\. If the two values here match, you create an alarm that goes to `ALARM` state if that many consecutive periods are breaching\.

   To create an M out of N alarm, specify a lower number for the first value than you specify for the second value\. For more information, see [Evaluating an alarm](AlarmThatSendsEmail.md#alarm-evaluation)\.

1. For **Missing data treatment**, choose how to have the alarm behave when some data points are missing\. For more information, see [Configuring how CloudWatch alarms treat missing data](AlarmThatSendsEmail.md#alarms-and-missing-data)\.

1. Choose **Next**\.

1. Under **Notification**, select an SNS topic to notify when the alarm is in `ALARM` state, `OK` state, or `INSUFFICIENT_DATA` state\.

   To have the alarm send multiple notifications for the same alarm state or for different alarm states, choose **Add notification**\.

   To have the alarm not send notifications, choose **Remove**\.

1. To have the alarm perform Auto Scaling, EC2, or Systems Manager actions, choose the appropriate button and choose the alarm state and action to perform\. Alarms can perform Systems Manager actions only when they go into ALARM state\. For more information about Systems Manager actions, see see [ Configuring CloudWatch to create OpsItems from alarms](https://docs.aws.amazon.com/systems-manager/latest/userguide/OpsCenter-create-OpsItems-from-CloudWatch-Alarms.html) and [ Incident creation](https://docs.aws.amazon.com/incident-manager/latest/userguide/incident-creation.html)\.
**Note**  
To create an alarm that performs an SSM Incident Manager action, you must have certain permissions\. For more information, see [ Identity\-based policy examples for AWS Systems Manager Incident Manager](https://docs.aws.amazon.com/incident-manager/latest/userguide/security_iam_id-based-policy-examples.html)\.

1. When finished, choose **Next**\.

1. Enter a name and description for the alarm\. The name must contain only ASCII characters\. Then choose **Next**\.

1. Under **Preview and create**, confirm that the information and conditions are what you want, then choose **Create alarm**\.

You can also add alarms to a dashboard\. For more information, see [Add an alarm widget to a CloudWatch dashboard](add_remove_alarm_dashboard.md)\. 