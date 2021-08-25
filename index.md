---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: post
---

## Links and blog posts and stuff

### [Connect to OpenStack MariaDB using PyMySQL](https://parko.id.au/2019/06/28/connect-to-openstack-mariadb-using-pymysql/)
Many of OpenStack’s containerised services do not include a MySQL client, despite heavily relying on the MariaDB/Galera cluster. Instead, the services use the PyMySQL and SQLAlchemy python modules for this interaction.

Given that peeking into the database is a pretty common operation when troubleshooting issues in OpenStack, the lack of a MySQL client is a bit of a pain point. Yes, you can always jump on to one of the controllers, grab a shell in the Galera container, and have at it, but this may not be beneficial if you suspect a network or connectivity related issue.

Thankfully it is quite simple to just utilise PyMySQL directly.

[Continue reading](https://parko.id.au/2019/06/28/connect-to-openstack-mariadb-using-pymysql/)

### [openstack overcloud deploy: plan-environment.yaml not found](https://parko.id.au/2019/03/22/openstack-overcloud-deploy-plan-environment-yaml-not-found/)
For one reason or another, I sometimes run into the following error when trying to deploy an OpenStack TripleO overcloud in my lab:

```
ClientException: Object GET failed: https://192.0.2.2:13808/v1
  /AUTH_1a5df8c242d848e8b01b974a72afcf8c
  /overcloud/plan-environment.yaml 404 Not Found
```

This usually occurs after impatiently cancelling an overcloud deployment – strongly not recommended of course. The overcloud plan, which is stored in a Swift container, is left missing one or more objects.

Given that Mistral (OpenStack’s workflow service) is meant to first delete the existing plan before continuing, it’s an odd error. The solution, it turns out, is not quite as straight forward as manually deleting the plan.

[Continue reading](https://parko.id.au/2019/03/22/openstack-overcloud-deploy-plan-environment-yaml-not-found/)

### [Enable SSL for an Oslo WSGI service](https://parko.id.au/2019/03/18/enable-ssl-for-an-oslo-wsgi-service/)
I recently needed to deploy a REST-based web service for use as a DynamicJSON vendordata provider to OpenStack’s nova metadata service. I settled on Oslo’s WSGI server, mainly due to the fact that the Oslo project’s goal is to provide standard libraries for all OpenStack projects. Plus it made incorporating authentication via Keystone middleware that much easier.

Given the requirement for TLS-everywhere, the next step was to enable SSL encryption of the service. This wasn’t as simple a task as I had hoped.

[Continue reading](https://parko.id.au/2019/03/18/enable-ssl-for-an-oslo-wsgi-service/)

### [Updating CloudForms advanced settings without a Web UI](https://parko.id.au/2018/08/31/cloudforms-advanced-settings-without-web-ui/)
To update the advanced settings of a CloudForms appliance you need to be logged in to the web interface of the actual appliance that needs updating. This is somewhat different to other general settings, which can be updated from any appliance or even from the appliance console.

“So what?” you ask. Well, things get complicated when you do not have access to the web interface. Perhaps it has not been enabled on one or more appliances in your cluster. Perhaps you are load balancing your web UI and are experiencing SSL certificate woes when trying to access appliance URLs. Or maybe, just maybe, you forgot to enable the Web Services role when upgrading from CloudForms 4.2 to 4.6 (CFME 5.7 => 5.9), effectively disabling authentication via the UI, like I may or may not have done…

[Continue reading](https://parko.id.au/2018/08/31/cloudforms-advanced-settings-without-web-ui/)

### [Complex data structures and the Ansible json_query filter](https://parko.id.au/2018/08/16/complex-data-structures-and-the-ansible-json_query-filter/)
While Ansible is busy fighting its own internal battle not to become a fully fledged programming language, instead remaining as simple and purely declarative as possible, it is still often necessary to work with more complex data structures. This is where the Jinja2 and Ansible filters can really shine.

Recently I stumbled across the Ansible json_query filter as a very neat solution to a problem that would have been otherwise messy to solve in Ansible. The filter is already well-documented, but I thought I would share a few examples of how it came in handy for me.

[Continue reading](https://parko.id.au/2018/08/16/complex-data-structures-and-the-ansible-json_query-filter/)

### [Querying the CloudForms VMDB via the REST API](https://parko.id.au/2018/08/08/query-cloudforms-manageiq-vmdb-rest-api/)
I have been playing around a lot more with the embedded Ansible feature of CloudForms 4.6. While this functionality was introduced in version 4.5, the ability to call a playbook method from a state machine in version 4.6 opens up a lot of possibilities.

One thing I was caught up on though was how to query VMDB collections for a specific item from within a playbook. Initially I thought it was going to be necessary to iterate through every item in the collection, something that would require a large amount of API calls and become totally impractical for larger collections. Luckily my initial thoughts were incorrect – the expansion and filtering capabilities allow for a single API query.

[Continue reading](https://parko.id.au/2018/08/08/query-cloudforms-manageiq-vmdb-rest-api/)
