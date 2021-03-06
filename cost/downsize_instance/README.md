## Downsize Instances Policy Template

### What it does

This Policy Template uses data from the monitoring api to determine is you can decrease the size of your running instance.

### Usage

There are two policy templates required to support this policy, `Downsize Instances Policy Template` and `Downsize Instances Add Tags Policy Template`.
The Downsize Instances Policy Template is used to actually downsize instances. If you chose `Email` from the `Escalation Options`, it will only email you which instances can be downsized.
If you chose `Downsize And Email` from the `Escalation Options`, it will email you a list of servers that were downsized and the size to which were changed. This policy will also resize the instance. This required the instance to be **stopped**.
If a server is marked `N/A`, no action will be taken and only the resize tag will be removed. You will need to manually move that instance to another family type.
**_This policy requires [RightLink 10](http://docs.rightscale.com/rl10/getting_started.html) with monitoring enabled and collecting metrics_**, see [Installation](http://docs.rightscale.com/rl10/about.html)


### Parameters

#### Downsize Instances Policy Template
1. Average free memory percent to allow for downsize - Value: 0-100, -1 disables this metric
2. Maximum free memory percent to allow for downsize - Value: 0-100, -1 disables this metric
3. Maximum cpu idle percent to allow for downsize - Value: 0-100, -1 disables this metric
4. Average cpu idle percent to allow for downsize - Value: 0-100, -1 disables this metric
5. Instance tags used to filter instances that must validate policy. Example: rs_monitoring:resize=1
6. Email address to send escalation emails to - Example: noreply@example.com
7. Escalation Options - Allowed Values: "Email", "Downsize And Email"
8. Days to cooldown between checks of same machine - Number of days to cooldown between checks of the same instance. This drives the `Downsize Instances Add Tags Policy Template`

#### Policy Actions

The following policy actions are taken on any resources found to be out of compliance.

- Downsize instances
- Send an email report

#### Downsize Instances Add Tags Policy Template
1. Instance tags used to filter instances that must validate policy. Example: rs_monitoring:resize=1
2. Email address to send escalation emails to - Example: noreply@example.com

#### Policy Actions

The following policy actions are taken on any resources found to be out of compliance.

- Add or remove tags for downsizing
- Send an email report


### Required Permissions

This policy requires permissions to access RightScale resources (clouds, instances and tags).  Before applying this policy add the following roles to the user applying the policy.  The roles should be applied to all Accounts where the policy will run or the Organization. For more information on modifying roles visit the [Governance Docs](https://docs.rightscale.com/cm/ref/user_roles.html)

- Cloud Management - Observer

### Supported Clouds

- AWS
- Azure
- Google

### Cost

This Policy Template does not launch any instances, and so does not incur any cloud costs.
