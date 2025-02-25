# CIS Landing Zone With Standalone Default VCN Template

This example shows how to deploy a CIS compliant landing zone using [OCI Core Landing Zone](../../) configuration. 

In this template, a single default three-tier VCN is deployed. Additionally, the following services are enabled:
  - [Connector Hub](https://docs.oracle.com/en-us/iaas/Content/connector-hub/overview.htm), for logging consolidation. Collected logs are sent to an OCI stream.
  - A [Security Zone](https://docs.oracle.com/en-us/iaas/security-zone/using/security-zones.htm) is created for the deployment. The Security Zone target is the landing zone top (enclosing) compartment.
  - [Vulnerability Scanning Service](https://docs.oracle.com/en-us/iaas/scanning/using/overview.htm#scanning_overview) is configured to scan Compute instances that are eventually deployed in the landing zone.
  - A basic [Budget](https://docs.oracle.com/en-us/iaas/Content/Billing/Concepts/budgetsoverview.htm#Budgets_Overview) is created.

Please see other [templates](../../templates/) available for CIS compliant landing zones with custom configurations.

This template can be deployed using OCI Resource Manager Service (RMS) or Terraform CLI:

## OCI RMS Deployment

By clicking the button below, you are redirected to an OCI RMS Stack with variables pre-assigned for deployment. 

[![Deploy_To_OCI](../../images/DeployToOCI.svg)](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/andrecorreaneto/v3testing/archive/refs/heads/misc.zip&zipUrlVariables={"service_label":"defvcn","network_admin_email_endpoints":"email.address@example.com","security_admin_email_endpoints":"email.address@example.com","add_tt_vcn_1":true,"enable_service_connector":true,"activate_service_connector":true,"service_connector_target_kind":"streaming","enable_security_zones":true,"vss_create":true,"create_budget":true})

You are required to review/adjust the following variable settings:
 - Make sure to pick an OCI region for deployment.
 - Provide real email addresses for *Network Admin Email Endpoints* and *Security Admin Email Endpoints* fields. 
 - Uncheck *Enable Cloud Guard Service* option in case it is already enabled in your tenancy.

With the stack created, perform a Plan, followed by an Apply using RMS UI.

## Terraform CLI Deployment

1. Rename file *main.tf.template* to *main.tf*. 
2. Provide/review the variable assignments in *main.tf*.
3. In this folder, execute the typical Terraform workflow:
    - $ terraform init
    - $ terraform plan
    - $ terraform apply