---
layout: "aws"
page_title: "AWS: aws_api_gateway_v2_stage"
sidebar_current: "docs-aws-resource-api-gateway-v2-stage"
description: |-
  Manages an Amazon API Gateway Version 2 stage.
---

# Resource: aws_api_gateway_v2_stage

Manages an Amazon API Gateway Version 2 stage.
More information can be found in the [Amazon API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api.html).

## Example Usage

### Basic

```hcl
resource "aws_api_gateway_v2_stage" "example" {
  api_id     = "${aws_api_gateway_v2_api.example.id}"
  name       = "example-stage"
}
```

## Argument Reference

The following arguments are supported:

* `api_id` - (Required) The API identifier.
* `name` - (Required) The name of the stage.
* `access_log_settings` - (Optional) Settings for logging access in this stage.
Use the [`aws_api_gateway_account`](/docs/providers/aws/r/api_gateway_account.html) resource to configure [permissions for CloudWatch Logging](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html#set-up-access-logging-permissions).
* `client_certificate_id` - (Optional) The identifier of a client certificate for the stage. Use the [`aws_api_gateway_client_certificate`](/docs/providers/aws/r/api_gateway_client_certificate.html) resource to configure a client certificate.
* `default_route_settings` - (Optional) The default route settings for the stage.
* `deployment_id` - (Optional) The deployment identifier of the stage. Use the `aws_api_gateway_v2_deployment` resource to configure a deployment.
* `description` - (Optional) The description for the stage.
* `route_settings` - (Optional) Route settings for the stage.
* `stage_variables` - (Optional) A map that defines the stage variables for the stage.
* `tags` - (Optional) A mapping of tags to assign to the stage.

The `access_log_settings` object supports the following:

* `destination_arn` - (Required) The ARN of the CloudWatch Logs log group to receive access logs. Any trailing `:*` is trimmed from the ARN.
* `format` - (Required) A single line [format](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-logging.html#apigateway-cloudwatch-log-formats) of the access logs of data, as specified by [selected $context variables](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-logging.html).

The `default_route_settings` object supports the following:

* `data_trace_enabled` - (Optional) Whether data trace logging is enabled for the default route. Affects the log entries pushed to Amazon CloudWatch Logs.
Defaults to `false`.
* `detailed_metrics_enabled` - (Optional) Whether detailed metrics are enabled for the default route. Defaults to `false`.
* `logging_level` - (Optional) The logging level for the default route. Affects the log entries pushed to Amazon CloudWatch Logs.
Valid values: `ERROR`, `INFO`, `OFF`. Defaults to `OFF`.
* `throttling_burst_limit` - (Optional) The throttling burst limit for the default route. Defaults to `5000` messages.
* `throttling_rate_limit` - (Optional) The throttling rate limit for the default route. Defaults to `10000` messages per second.

The `route_settings` object supports the following:

* `route_key` - (Required) Route key.
* `data_trace_enabled` - (Optional) Whether data trace logging is enabled for the default route. Affects the log entries pushed to Amazon CloudWatch Logs.
* `detailed_metrics_enabled` - (Optional) Whether detailed metrics are enabled for the default route.
* `logging_level` - (Optional) The logging level for the default route. Affects the log entries pushed to Amazon CloudWatch Logs.
* `throttling_burst_limit` - (Optional) The throttling burst limit for the default route.
* `throttling_rate_limit` - (Optional) The throttling rate limit for the default route.

## Attribute Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The stage identifier.
* `arn` - The ARN of the stage.
* `execution_arn` - The execution ARN to be used in [`lambda_permission`](/docs/providers/aws/r/lambda_permission.html)'s `source_arn`
  when allowing API Gateway to invoke a Lambda function,
  e.g. `arn:aws:execute-api:eu-west-2:123456789012:z4675bid1j/example-stage`
* `invoke_url` - The URL to invoke the API pointing to the stage,
  e.g. `wss://z4675bid1j.execute-api.eu-west-2.amazonaws.com/example-stage`

## Import

`aws_api_gateway_v2_stage` can be imported by using the API identifier and stage name, e.g.

```
$ terraform import aws_api_gateway_v2_stage.example aabbccddee/example-stage
```
