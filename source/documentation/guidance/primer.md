
# GOV.UK PaaS Primer

> A primer for Architects, Technical Leads and Information Assurance

<!--
Changes

- 2019-07-17 Incorporate content into technical documentation
- 2019-06-17 Fix Languages table
- 2019-06-17 Ensure all links are https
- 2019-06-16 Convert to markdown so that its under version control and consistent with the rest of our documentation
-->

## Introduction

A high level introduction to GOV.UK Platform as a Service aimed at Architects, Technical Leads and Information Assurance so that they can understand how their service can be hosted on the platform.

## Essentials

[GOV.UK Platform as a Service](https://cloud.service.gov.uk) is a [multi-tenant](https://en.wikipedia.org/wiki/Multitenancy) container hosting solution for [cloud native](https://pivotal.io/cloud-native) applications based on [Open Source Cloud Foundry](https://www.cloudfoundry.org/).

GOV.UK PaaS supports the needs of [UK Government Departments](https://www.gov.uk/government/organisations).

If your department uses the GOV.UK PaaS, you do not need to procure hosting and manage cloud infrastructure.

GOV.UK PaaS Supports non-Crown organisations, including local authorities through an "invitation only" pilot. (From April 2019 )

The GOV.UK PaaS platform:

-   hosts 33 live services including [DiT Export Opportunities](https://www.great.gov.uk/export-opportunities/), [HMRC Trade Tariffs](https://www.gov.uk/trade-tariff), [BEIS Primary Authority Register](https://primary-authority.beis.gov.uk/), [GOV.UK Notify](https://www.notifications.service.gov.uk/), [Digital Marketplace](https://www.digitalmarketplace.service.gov.uk/)
-   complies with the [GDPR](https://team-manual.cloud.service.gov.uk/team/tenant_personal_data/)
-   uses [Amazon Web Services](https://aws.amazon.com/) in multiple availability zones in Dublin and London
-   is supported by the [GOV.UK PaaS  team](https://www.cloud.service.gov.uk/support)
-   provides 99.99% uptime for tenant applications (based on the last six months' performance)
-   offers 24-hour platform-level support for billable live services

The GOV.UK PaaS team are [Security Cleared](https://www.gov.uk/guidance/security-vetting-and-clearance#applicant) civil servants at the [Government Digital Service](https://www.gov.uk/government/organisations/government-digital-service).

We [code in the open](https://www.gov.uk/service-manual/technology/making-source-code-open-and-reusable) and our software is available for review on [GitHub](https://github.com/alphagov?utf8=%E2%9C%93&q=paas-&type=&language=).

## Shared Responsibility

The [GOV.UK PaaS team](https://www.cloud.service.gov.uk/support) is responsible for the engineering of the platform itself and kernel and security vulnerability patching. This relieves your development team of these responsibilities.

View our [responsibility model in our documentation](https://docs.cloud.service.gov.uk/guidance.html#responsibility-model) to learn more.

## Security

-   The platform is designed to meet the NCSC [Cloud Security Principles](https://www.ncsc.gov.uk/guidance/implementing-cloud-security-principles).
-   The platform supports data classified as '[OFFICIAL](https://www.gov.uk/government/publications/government-security-classifications)'.
-   Data in transit is protected by [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security).
-   Our Backing Services support encryption at rest by default.
-   The platform and backing services are [IA assured](https://www.cloud.service.gov.uk/ia).
-   The platform is penetration tested annually by external security specialists. The latest test was in February 2019.
-   [Read more about our security approach](https://www.cloud.service.gov.uk/security)

## Applications

-   Applications must follow the [12 factor principles](https://docs.cloud.service.gov.uk/architecture.html#12-factor-application-principles).
-   Applications are hosted in isolated containers.
-   The platform [supports Docker containers](https://docs.cloudfoundry.org/adminguide/docker.html).
-   Applications must not rely on local file system persistence.
-   The platform handles horizontal scaling of applications and ensures the workload is evenly spread across the availability zones for resilience.
-   The platform is not optimised for analytics workloads or long running/batch processes.
s may present public web addresses to the internet or be private.

### Quotas

The GOV.UK PaaS provides resources to tenants through a series of [Cloud Foundry Quotas](https://docs.cloudfoundry.org/adminguide/quota-plans.html)


|name                   |total memory|routes|service-instances|
|-----------------------|------------|------|-----------------|
|default (no paid plans)|5Gb         |1000  |10 |
|small                  |10Gb        |1000  |10 |
|medium                 |60Gb        |1000  |20 |
|large                  |100Gb       |1000  |40 |
|xlarge                 |200Gb       |1000  |80 |
|2xlarge                |400Gb       |1000  |160 |
|4xlarge                |800Gb       |2000  |320 |
|8xlarge                |1.6Tb       |4000  |720 |

In the event your service requires more resource than is available in the largest plan, please contact the support team and we will advise you or provision a larger plan.

### Services

The GOV.UK PaaS provides a number of highly available backing services.

| Service     | Description    | Version       | Plans|
|-------------|-------------|-------------|-------------|
| CDN-Route | Proxy traffic from a domain that the user controls to an existing Cloud Foundry application or external URL| - | - |
| Elasticsearch |A search engine based on Lucene. It provides a distributed, multitenant capable full-text search engine with an HTTP web interface and schema-free JSON documents. | 6.x| tiny (80Gb) small (240Gb) medium (525Gb) large (1,050Gb) |
| MySQL |A relational database management system |5.7 | tiny (5Gb) small (20Gb) medium (100Gb) large (512Gb) xlarge (2Tb)|
| Object Store |Object storage | - | invitation only private beta |
| PostgreSQL |A relational database management system |9.x + 10 | tiny (5Gb) small (20Gb) medium (100Gb) large (512Gb) xlarge (2Tb) |
| Redis | A distributed, in-memory key-value database with optional durability. | |tiny (568Mb) medium (6.3Gb) |

### Languages

The platform supports a variety of programming languages through the
concept of [buildpacks](https://docs.cloudfoundry.org/buildpacks/).

| Buildpack                     |Release Notes|  Description                   |
|-------------------------------|-------------|--------------------------------|
| [Binary](https://docs.cloudfoundry.org/buildpacks/binary/index.html) |[release notes](https://github.com/cloudfoundry/binary-buildpack/releases) |Buildpack for running arbitrary binary web applications.  |
| [Custom](https://docs.cloudfoundry.org/buildpacks/custom.html) | |Bring your own custom buildpacks providing support for arbitrary languages. |
| [Go](https://docs.cloudfoundry.org/buildpacks/go/index.html)  |[release notes](https://github.com/cloudfoundry/go-buildpack/releases) |Buildpack for golang applications.   |
| [Java](https://docs.cloudfoundry.org/buildpacks/java/index.html) |[release notes](https://github.com/cloudfoundry/java-buildpack/releases) | Buildpack for Java language applications.  |
| [Nginx](https://docs.cloudfoundry.org/buildpacks/nginx/index.html)| [release notes](https://github.com/cloudfoundry/nginx-buildpack/releases) |Buildpack for nginx. |
| [Nodejs](https://docs.cloudfoundry.org/buildpacks/node/index.html)| [release notes](https://github.com/cloudfoundry/nodejs-buildpack/releases)|Buildpack for nodejs javascript applications.  |
| [PHP](https://docs.cloudfoundry.org/buildpacks/php/index.html)     |[release notes](https://github.com/cloudfoundry/php-buildpack/releases) |Buildpack for PHP applications. |
| [Python](https://docs.cloudfoundry.org/buildpacks/python/index.html)     | [release notes](https://github.ßcom/cloudfoundry/python-buildpack/releases)|Buildpack for python applications. |
| [Ruby](https://docs.cloudfoundry.org/buildpacks/ruby/index.html) |[release notes](https://github.com/cloudfoundry/ruby-buildpack/releases) |Buildpack for Ruby applications. |
| [R](https://docs.cloudfoundry.org/buildpacks/r/index.html)        | [release notes](https://github.com/cloudfoundry/r-buildpack/releases)|Buildpack for R language applications. |
| [Static](https://docs.cloudfoundry.org/buildpacks/staticfile/index.html) | [release notes](https://github.com/cloudfoundry/staticfile-buildpack/releases)|Buildpack for static web sites. |
| [.NET Core](https://github.com/cloudfoundry/dotnet-core-buildpack)|[release notes](https://github.com/cloudfoundry/dotnet-core-buildpack/releases)  |Buildpack for Microsoft .NET Core. |

### Docker

The platform supports Docker as follows

#### Deployment

The platform [supports the deployment of Docker
images](https://docs.cloud.service.gov.uk/deploying_apps.html#deploy-a-docker-image-experimental).

#### Docker Compose

The platform does not support [Docker
Compose](https://docs.docker.com/compose/overview/)
multi-container applications.

#### Maximum Docker image size

The maximum size of Docker image that may be staged is 4Gb and is a
platform wide limit.

#### Registries

Images must be pushed to a Docker registry such as
[DockerHub](https://hub.docker.com/) or [Google Container
Registry](https://cloud.google.com/container-registry/)
before they can be pushed to the GOV.UK PaaS. Your ability to stage and
restage Docker applications is tied to the availability of the registry
hosting the images.

The GOV.UK PaaS does not offer a Docker registry service.

## Networking

### Bring your own domain

You may bring your own domain or subdomain to the platform. We provide a
[service](https://docs.cloud.service.gov.uk/deploying_services/use_a_custom_domain/#managing-custom-domains-using-the-cdn-route-service)
that allows for automated creation and management of TLS certificates
for secure HTTPS traffic.

### Integration of external APIs

Applications can connect out to other internet hosted back ends allowing
your to integrate third party SaaS services and other platforms through
public web apis.

### Private applications

Where more control is needed over which applications can talk to each
other the platform now supports [private applications](https://docs.cloud.service.gov.uk/deploying_apps.html#deploying-private-apps)
(i.e. applications without a public internet route).

### Public applications

Applications typically have a route to allow [inbound connections via
the internet.](https://docs.cloud.service.gov.uk/deploying_apps.html#deploying-public-apps)

### Service Discovery

Applications using microservice architectures can now make use of the
new service discovery feature to manage scaling of individual
microservices.


## Observability

### Logs

The platform [aggregates logs for your application in a buffer of
finite
size.](https://docs.cloud.service.gov.uk/monitoring_apps.html#logs)
If you want to preserve these for longer term analysis or debugging you
must ship your logs to an external log provider. Logging as a Service is
on our
[roadmap](https://www.cloud.service.gov.uk/roadmap).

### Metrics

The platform can be configured to [emit application metrics in standard
statsd or prometheus
format.](https://docs.cloud.service.gov.uk/monitoring_apps.html#monitoring-apps)
It is currently the tenant's responsibility to procure an external
service to handle these metrics. Metrics as a Service is on our
[roadmap](https://www.cloud.service.gov.uk/roadmap).

### Tracing

The platform [adds Zipkin compatible
headers](https://docs.cloud.service.gov.uk/troubleshooting.html#tracing-http-requests)
to the incoming requests so you can match those with your application's
responses.

## Continuous Integration

The platform does not offer CICD as a service and currently service
teams must [bring their own tooling](https://docs.cloud.service.gov.uk/using_ci.html#configuring-a-continuous-integration-ci-tool).
CICD as a
service is on our
[roadmap](https://www.cloud.service.gov.uk/roadmap).

## Platform constraints

### Functions as a service

The GOV.UK PaaS does not support the Functions as a Service programming
model.

### GPU support

Some machine learning workloads require the use of specific Amazon
machine instance types that support hardware GPUs. The PaaS does not
support GPUs.

### Identity Provider

The GOV.UK PaaS does not offer an identity provider for use in tenant
applications.

### PSN

The platform does not currently support connection to the Public
Services Network or
[PSN](https://www.gov.uk/government/groups/public-services-network).

### UDP networking

Our routers support HTTP and TCP protocols. The platform does not
support UDP networking.

### Virtual Machines

The platform is designed to host applications provided as source code
(as buildpacks) or Docker images, we do not offer a Virtual Machine
hosting service.

### Web Application Firewall

The platform does not supply a Web Application Firewall (WAF) however we
are aware that tenants of the platform have used WAFs such as AWS WAF
and Naxsi.

### Windows

At the lowest level the platform runs a Linux kernel based on Ubuntu
Bionic 18.04. The GOV.UK PaaS platform does not support native windows
workloads running on Windows operating system kernels. However it
supports applications written in .NET Core via a buildpack.

## GOV.UK PaaS Accounts

### Billing

Users are billed in arrears based on monthly consumption. Itemised
billing and self-service user management is available via the
[adminstration
interface](https://admin.cloud.service.gov.uk/). We charge
for resource use to the nearest second of consumption.

### Calculator

Our
[calculator](https://admin.cloud.service.gov.uk/calculator)
provides an estimate of monthly costs. This can be used to look at the
costs for various configurations.

### Memorandum of Understanding

If at any time if you'd like to access the full service, your
department will need to sign a Memorandum of Understanding with
Government Digital Service. You will also need to identify a Billing
Manager and get their approval to move to the paid service.

### Organisations, Spaces and Users

The platform uses the concepts of
[Organisations](https://docs.cloud.service.gov.uk/orgs_spaces_users.html#organisations)
and
[Spaces](https://docs.cloud.service.gov.uk/orgs_spaces_users.html#spaces)
to manage the applications and backing stores that comprise a service.

Who is able to do what with the system is controlled using the concepts
of [users and
roles.](https://docs.cloud.service.gov.uk/orgs_spaces_users.html#users-and-user-roles)

The technical documentation describes some [stereotypical ways that
departments arrange their
affairs.](https://docs.cloud.service.gov.uk/orgs_spaces_users.html#case-studies)

### Trial Accounts

You can request a trial account for GOV.UK PaaS that will last up to 3
months and give you a set of basic features and a capped quota of
compute and storage. You can't use the trial version of the platform for
production or live services. [Learn how to get started with GOV.UK
PaaS.](https://www.cloud.service.gov.uk/get-started)

<!--
## More information

### References

|resource|link|
|--------|----|
|Product Page| [GOV.UK PaaS](https://www.cloud.service.gov.uk/)|
|Estimate costs  |[Calculator](https://admin.cloud.service.gov.uk/calculator) |
|Review features   | [Features](https://www.cloud.service.gov.uk/features)|
|Information Assurance stance  | [Information Assurance](https://www.cloud.service.gov.uk/ia)|
|Cloud guidance from NCSC| [NCSC Cloud Principles](https://www.ncsc.gov.uk/collection/cloud-security?curPage=/collection/cloud-security/implementing-the-cloud-security-principles)|
|Our roadmap |[Roadmap](https://www.cloud.service.gov.uk/roadmap)|
|Who is responsible for what |[Shared Responsibility Model](https://docs.cloud.service.gov.uk/guidance.html#responsibility-model)|
|Our support structure|[Support](https://www.cloud.service.gov.uk/support)|
|Technical documentation for developers|Technical documentation](https://docs.cloud.service.gov.uk/#gov-uk-platform-as-a-service)|
|Cloud Native application guidance |[12 Factor Applications](https://12factor.net/)|


### Contacts

|resource|link|
|-|-|
  |Email                 |   [gov-uk-paas-support\@digital.cabinet-office.gov.uk](mailto:gov-uk-paas-support@digital.cabinet-office.gov.uk)|
  | Cross Government Slack  | [\#govuk-paas](https://ukgovernmentdigital.slack.com/messages/C33SAH4GJ)|

  -->
