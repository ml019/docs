---
sidebar_label: components
title: components
---
import Admonition from 'react-admonitions';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# apigateway

Application level API proxy

There are multiple modes of deployment offered for the API Gateway, mainly to
support use of product domains for endpoints. The key
consideration is the handling of the host header. The modes reflect the
changes and improvements AWS have made to the API Gateway over time.
For whitelisted APIs, mode 4 is the recommended one now.

1.  Multi-domain cloudfront + EDGE endpoint
    -   waf based IP whitelisting
    -   multiple cloudfront aliases
    -   host header blocked
    -   EDGE based API Gateway
    -   signing based on AWS assigned API domain name
    -   API-KEY used as shared secret between cloudfront and the API
2.  Single domain cloudfront + EDGE endpoint
    -   waf based IP whitelisting
    -   single cloudfront alias
    -   host header blocked
    -   EDGE based API Gateway
    -   signing based on "sig4-" + alias
    -   API-KEY used as shared secret between cloudfront and the API
3.  Multi-domain cloudfront + REGIONAL endpoint
    -   waf based IP whitelisting
    -   multiple cloudfront aliases
    -   host header passed through to endpoint
    -   REGIONAL based API Gateway
    -   signing based on any of the aliases
    -   API-KEY used as shared secret between cloudfront and the API
4.  API endpoint
    -   waf or policy based IP whitelisting
    -   multiple aliases or AWS assigned domain
    -   EDGE or REGIONAL
    -   signing based on any of the aliases
    -   API-KEY can be used for client metering

If multiple domains are provided, the primary domain is used to provide the
endpoint for the the API documentation and for the gateway attributes. For
documentation, the others redirect to the primary.

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"apigateway" : {
		"Fragment" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"WAF" : {
			"IPAddressGroups" : "<array of string>",
			"OWASP" : false
		},
		"EndpointType" : "EDGE",
		"IPAddressGroups" : "<array of string>",
		"Authentication" : "IP",
		"CloudFront" : {
			"AssumeSNI" : true,
			"EnableLogging" : true,
			"CountryGroups" : "<array of string>",
			"CustomHeaders" : "<array of any>",
			"Mapping" : false,
			"Compress" : true
		},
		"Certificate" : {
			"Qualifiers" : "<object>",
			"Domain" : "<string>",
			"IncludeInDomain" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>"
			},
			"Host" : "<string>",
			"HostParts" : "<array of string>",
			"IncludeInHost" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>",
				"Tier" : "<boolean>",
				"Component" : "<boolean>",
				"Instance" : "<boolean>",
				"Version" : "<boolean>",
				"Host" : "<boolean>"
			},
			"External" : "<boolean>",
			"Wildcard" : "<boolean>"
		},
		"Publish" : {
			"DnsNamePrefix" : "docs",
			"IPAddressGroups" : "<array of string>"
		},
		"Publishers" : {
			"example" : {
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				},
				"Path" : {
					"Host" : "<string>",
					"Style" : "single",
					"IncludeInPath" : {
						"Product" : true,
						"Environment" : false,
						"Solution" : false,
						"Segment" : true,
						"Tier" : false,
						"Component" : false,
						"Instance" : false,
						"Version" : false,
						"Host" : false
					}
				}
			}
		},
		"Mapping" : {
			"IncludeStage" : true
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Security" : "default"
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"LogMetrics" : {
			"example" : {
				"LogFilter" : "<string>"
			}
		},
		"BasePathBehaviour" : "ignore"
	}
}
```

</TabItem>
<TabItem value='attributes'>

```markdown

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [WAF](#WAF)
    -   [IPAddressGroups](#IPAddressGroups) - Required - **Type:** array of string  
    -   [OWASP](#OWASP) - Optional - **Type:** boolean - **Default:** `false`  
-   [EndpointType](#EndpointType) - Optional - **Type:** string - **Default:** `EDGE`  
    **Possible Values:** `[EDGE, REGIONAL]`
-   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
-   [Authentication](#Authentication) - Optional - **Type:** string - **Default:** `IP`  
    **Possible Values:** `[IP, SIG4ORIP, SIG4ANDIP]`
-   [CloudFront](#CloudFront)
    -   [AssumeSNI](#AssumeSNI) - Optional - **Type:** boolean - **Default:** `true`  
    -   [EnableLogging](#EnableLogging) - Optional - **Type:** boolean - **Default:** `true`  
    -   [CountryGroups](#CountryGroups) - Optional - **Type:** array of string  
    -   [CustomHeaders](#CustomHeaders) - Optional - **Type:** array of any  
    -   [Mapping](#Mapping) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Compress](#Compress) - Optional - **Type:** boolean - **Default:** `true`  
-   [Certificate](#Certificate)
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [Domain](#Domain) - Optional - **Type:** string  
    -   [IncludeInDomain](#IncludeInDomain)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** string  
    -   [HostParts](#HostParts) - Optional - **Type:** array of string  
    -   [IncludeInHost](#IncludeInHost)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Tier](#Tier) - Optional - **Type:** boolean  
    -   [Component](#Component) - Optional - **Type:** boolean  
    -   [Instance](#Instance) - Optional - **Type:** boolean  
    -   [Version](#Version) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** boolean  
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [External](#External) - Optional - **Type:** boolean  
    -   [Wildcard](#Wildcard) - Optional - **Type:** boolean  
-   [Publish](#Publish)
    -   [DnsNamePrefix](#DnsNamePrefix) - Optional - **Type:** string - **Default:** `docs`  
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
-   [Publishers](#Publishers)
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Path](#Path)
    -   [Host](#Host) - Optional - **Type:** string  
    -   [Style](#Style) - Optional - **Type:** string - **Default:** `single`  
    -   [IncludeInPath](#IncludeInPath)
    -   [Product](#Product) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Environment](#Environment) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Solution](#Solution) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Segment](#Segment) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Tier](#Tier) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Component](#Component) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Instance](#Instance) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Version](#Version) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Host](#Host) - Optional - **Type:** boolean - **Default:** `false`  
-   [Mapping](#Mapping)
    -   [IncludeStage](#IncludeStage) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Security](#Security) - Optional - **Type:** string - **Default:** `default`  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
-   [BasePathBehaviour](#BasePathBehaviour) - Optional - **Type:** string - **Default:** `ignore`  
    **Description:** How to handle base paths provided in the spec  **Possible Values:** `[ignore, prepend, split]`

```

</TabItem>
</Tabs>

# apiusageplan

provides a metered link between an API gateway and an invoking client

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"apiusageplan" : {
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# baseline

A set of resources required for every segment deployment

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment

**Sub Components**

-   [baselinedata](#baselinedata)
    -   **Component Attribute** - DataBuckets
    -   **Link Attribute** - DataBucket
-   [baselinekey](#baselinekey)
    -   **Component Attribute** - Keys
    -   **Link Attribute** - Key


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"baseline" : {
		"Active" : false,
		"Seed" : {
			"Length" : 10
		},
		"DataBuckets" : {
			"example" : "< instance of baselinedata>"
		},
		"Keys" : {
			"example" : "< instance of baselinekey>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [Seed](#Seed)
    -   [Length](#Length) - Optional - **Type:** number - **Default:** `10`  

```

</TabItem>
</Tabs>

# baselinedata

A segment shared data store

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"baselinedata" : {
		"Role" : "<string>",
		"Lifecycles" : {
			"example" : {
				"Prefix" : "<unknown>",
				"Expiration" : "_operations",
				"Offline" : "_operations"
			}
		},
		"Versioning" : false,
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Notifications" : {
			"example" : {
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				},
				"Prefix" : "<string>",
				"Suffix" : "<string>",
				"Events" : [
					"create"
				]
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Role](#Role) - Required - **Type:** string  
    **Possible Values:** `[appdata, operations]`
-   [Lifecycles](#Lifecycles)
    -   [Prefix](#Prefix) - Optional  
           **Types:** string  **Description:** The prefix to apply the lifecycle to
    -   [Expiration](#Expiration) - Optional - **Default:** `_operations`  
           **Types:** string, number  **Description:** Provide either a date or a number of days
    -   [Offline](#Offline) - Optional - **Default:** `_operations`  
           **Types:** string, number  **Description:** Provide either a date or a number of days
-   [Versioning](#Versioning) - Optional - **Type:** boolean - **Default:** `false`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Notifications](#Notifications)
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Prefix](#Prefix) - Optional - **Type:** string  
    -   [Suffix](#Suffix) - Optional - **Type:** string  
    -   [Events](#Events) - Optional - **Type:** array of string - **Default:** `create`  
           **Possible Values:** `[create, remove, restore, reducedredundancy]`

```

</TabItem>
</Tabs>

# baselinekey

Shared security keys for a segment

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"baselinekey" : {
		"Engine" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Required - **Type:** string  
    **Possible Values:** `[cmk, ssh, oai]`
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# bastion

An bastion instance to manage vpc only components

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"bastion" : {
		"Active" : false,
		"OS" : "linux",
		"Fragment" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"AutoScaling" : {
			"DetailedMetrics" : true,
			"WaitForSignal" : true,
			"MinUpdateInstances" : 1,
			"ReplaceCluster" : false,
			"UpdatePauseTime" : "10M",
			"StartupTimeout" : "15M",
			"AlwaysReplaceOnUpdate" : false,
			"ActivityCooldown" : 30
		},
		"Permissions" : {
			"Decrypt" : false,
			"AsFile" : false,
			"AppData" : false,
			"AppPublic" : false
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [OS](#OS) - Optional - **Type:** string - **Default:** `linux`  
    **Possible Values:** `[linux]`
-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [AutoScaling](#AutoScaling)
    -   [DetailedMetrics](#DetailedMetrics) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Enable the collection of autoscale group detailed metrics
    -   [WaitForSignal](#WaitForSignal) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Wait for a cfn-signal before treating the instances as alive
    -   [MinUpdateInstances](#MinUpdateInstances) - Optional - **Type:** number - **Default:** `1`  
           **Description:** The minimum number of instances which must be available during an update
    -   [ReplaceCluster](#ReplaceCluster) - Optional - **Type:** boolean - **Default:** `false`  
           **Description:** When set to true a brand new cluster will be built, if false the instances in the current cluster will be replaced
    -   [UpdatePauseTime](#UpdatePauseTime) - Optional - **Type:** string - **Default:** `10M`  
           **Description:** How long to pause betweeen updates of instances
    -   [StartupTimeout](#StartupTimeout) - Optional - **Type:** string - **Default:** `15M`  
           **Description:** How long to wait for a cfn-signal to be received from a host
    -   [AlwaysReplaceOnUpdate](#AlwaysReplaceOnUpdate) - Optional - **Type:** boolean - **Default:** `false`  
           **Description:** Replace instances on every update action
    -   [ActivityCooldown](#ActivityCooldown) - Optional - **Type:** number - **Default:** `30`  
-   [Permissions](#Permissions)
    -   [Decrypt](#Decrypt) - Optional - **Type:** boolean - **Default:** `false`  
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `false`  
    -   [AppData](#AppData) - Optional - **Type:** boolean - **Default:** `false`  
    -   [AppPublic](#AppPublic) - Optional - **Type:** boolean - **Default:** `false`  

```

</TabItem>
</Tabs>

# cache

Managed in-memory cache services

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"cache" : {
		"Engine" : "<string>",
		"EngineVersion" : "<string>",
		"Port" : "<string>",
		"Backup" : {
			"RetentionPeriod" : "<string>"
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"Hibernate" : {
			"Enabled" : false,
			"StartUpMode" : "replace"
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Required - **Type:** string  
-   [EngineVersion](#EngineVersion) - Optional - **Type:** string  
-   [Port](#Port) - Optional - **Type:** string  
-   [Backup](#Backup)
    -   [RetentionPeriod](#RetentionPeriod) - Optional - **Type:** string  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [Hibernate](#Hibernate)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
    -   [StartUpMode](#StartUpMode) - Optional - **Type:** string - **Default:** `replace`  
           **Possible Values:** `[replace]`
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  

```

</TabItem>
</Tabs>

# computecluster

Auto-Scaling IaaS with code deployment

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"computecluster" : {
		"Fragment" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"UseInitAsService" : false,
		"AutoScaling" : {
			"DetailedMetrics" : true,
			"WaitForSignal" : true,
			"MinUpdateInstances" : 1,
			"ReplaceCluster" : false,
			"UpdatePauseTime" : "10M",
			"StartupTimeout" : "15M",
			"AlwaysReplaceOnUpdate" : false,
			"ActivityCooldown" : 30
		},
		"DockerHost" : false,
		"Ports" : {
			"example" : {
				"IPAddressGroups" : "<array of string>",
				"LB" : {
					"Tier" : "<string>",
					"Component" : "<string>",
					"LinkName" : "lb",
					"Instance" : "<string>",
					"Version" : "<string>",
					"PortMapping" : "<string>"
				}
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [UseInitAsService](#UseInitAsService) - Optional - **Type:** boolean - **Default:** `false`  
-   [AutoScaling](#AutoScaling)
    -   [DetailedMetrics](#DetailedMetrics) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Enable the collection of autoscale group detailed metrics
    -   [WaitForSignal](#WaitForSignal) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Wait for a cfn-signal before treating the instances as alive
    -   [MinUpdateInstances](#MinUpdateInstances) - Optional - **Type:** number - **Default:** `1`  
           **Description:** The minimum number of instances which must be available during an update
    -   [ReplaceCluster](#ReplaceCluster) - Optional - **Type:** boolean - **Default:** `false`  
           **Description:** When set to true a brand new cluster will be built, if false the instances in the current cluster will be replaced
    -   [UpdatePauseTime](#UpdatePauseTime) - Optional - **Type:** string - **Default:** `10M`  
           **Description:** How long to pause betweeen updates of instances
    -   [StartupTimeout](#StartupTimeout) - Optional - **Type:** string - **Default:** `15M`  
           **Description:** How long to wait for a cfn-signal to be received from a host
    -   [AlwaysReplaceOnUpdate](#AlwaysReplaceOnUpdate) - Optional - **Type:** boolean - **Default:** `false`  
           **Description:** Replace instances on every update action
    -   [ActivityCooldown](#ActivityCooldown) - Optional - **Type:** number - **Default:** `30`  
-   [DockerHost](#DockerHost) - Optional - **Type:** boolean - **Default:** `false`  
-   [Ports](#Ports)
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
    -   [LB](#LB)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [LinkName](#LinkName) - Optional - **Type:** string - **Default:** `lb`  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  

```

</TabItem>
</Tabs>

# configstore

A configuration store to provide dynamic attributes

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Sub Components**

-   [configbranch](#configbranch)
    -   **Component Attribute** - Branches
    -   **Link Attribute** - Branch


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"configstore" : {
		"Fragment" : "<string>",
		"Table" : {
			"Billing" : "provisioned",
			"Capacity" : {
				"Read" : 1,
				"Write" : 1
			},
			"Backup" : {
				"Enabled" : false
			},
			"Stream" : {
				"Enabled" : false,
				"ViewType" : "NEW_IMAGE"
			}
		},
		"SecondaryKey" : false,
		"Branches" : {
			"example" : "< instance of configbranch>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Table](#Table)
    -   [Billing](#Billing) - Optional - **Type:** string - **Default:** `provisioned`  
           **Description:** The billing mode for the table  **Possible Values:** `[provisioned, per-request]`
    -   [Capacity](#Capacity)
    -   [Read](#Read) - Optional - **Type:** number - **Default:** `1`  
                  **Description:** When using provisioned billing the maximum RCU of the table
    -   [Write](#Write) - Optional - **Type:** number - **Default:** `1`  
                  **Description:** When using provisioned billing the maximum WCU of the table
    -   [Backup](#Backup)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
                  **Description:** Enables point in time recovery on the table
    -   [Stream](#Stream)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
                  **Description:** Enables dynamodb event stream
    -   [ViewType](#ViewType) - Optional - **Type:** string - **Default:** `NEW_IMAGE`  
                  **Possible Values:** `[KEYS_ONLY, NEW_IMAGE, OLD_IMAGE, NEW_AND_OLD_IMAGES]`
-   [SecondaryKey](#SecondaryKey) - Optional - **Type:** boolean - **Default:** `false`  
    **Description:** Uses the name of the branch to provide a secondary sort key on branches - id being the primary

```

</TabItem>
</Tabs>

# configbranch

A branch of configuration which belongs to a config store

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"configbranch" : {
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"States" : {
			"example" : {
				"InitialValue" : "-"
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [States](#States)
    -   [InitialValue](#InitialValue) - Optional - **Type:** string - **Default:** `-`  
           **Description:** The initial value that will be applied to the state

```

</TabItem>
</Tabs>

# contenthub

Hub for decentralised content hosting with centralised publishing

**Deployment Properties**

-   **Available Providers** - github
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"contenthub" : {
		"Prefix" : "<string>",
		"Engine" : "github",
		"Branch" : "master",
		"Repository" : "<string>"
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Prefix](#Prefix) - Required - **Type:** string  
-   [Engine](#Engine) - Optional - **Type:** string - **Default:** `github`  
-   [Branch](#Branch) - Optional - **Type:** string - **Default:** `master`  
-   [Repository](#Repository) - Optional - **Type:** string  

```

</TabItem>
</Tabs>

# contentnode

Node for decentralised content hosting with centralised publishing

**Deployment Properties**

-   **Available Providers** - github
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"contentnode" : {
		"Path" : {
			"Host" : "<string>",
			"Style" : "single",
			"IncludeInPath" : {
				"Product" : true,
				"Environment" : false,
				"Solution" : false,
				"Segment" : true,
				"Tier" : false,
				"Component" : false,
				"Instance" : false,
				"Version" : false,
				"Host" : false
			}
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Path](#Path)
    -   [Host](#Host) - Optional - **Type:** string  
    -   [Style](#Style) - Optional - **Type:** string - **Default:** `single`  
    -   [IncludeInPath](#IncludeInPath)
    -   [Product](#Product) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Environment](#Environment) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Solution](#Solution) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Segment](#Segment) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Tier](#Tier) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Component](#Component) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Instance](#Instance) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Version](#Version) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Host](#Host) - Optional - **Type:** boolean - **Default:** `false`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# datafeed

A service which feeds data into the ES index currently based on kineses data firehose

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"datafeed" : {
		"ElasticSearch" : {
			"IndexPrefix" : "<string>",
			"IndexRotation" : "OneMonth",
			"DocumentType" : "<string>"
		},
		"Buffering" : {
			"Interval" : 60,
			"Size" : 1
		},
		"Logging" : true,
		"Encrypted" : false,
		"Backup" : {
			"FailureDuration" : 3600,
			"Policy" : "FailedDocumentsOnly"
		},
		"Destination" : {
			"Link" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"LogWatchers" : {
			"example" : {
				"LogFilter" : "<string>",
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				}
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [ElasticSearch](#ElasticSearch)
    -   [IndexPrefix](#IndexPrefix) - Required - **Type:** string  
           **Description:** The prefix applied to generate the index name ( if not using roll over this will be the index name)
    -   [IndexRotation](#IndexRotation) - Optional - **Type:** string - **Default:** `OneMonth`  
           **Description:** When to rotate the index ( the timestamp will be appended to the indexprefix)  **Possible Values:** `[NoRotation, OneDay, OneHour, OneMonth, OneWeek]`
    -   [DocumentType](#DocumentType) - Required - **Type:** string  
           **Description:** The document type used when creating the document
-   [Buffering](#Buffering)
    -   [Interval](#Interval) - Optional - **Type:** number - **Default:** `60`  
           **Description:** The time in seconds before data should be delivered
    -   [Size](#Size) - Optional - **Type:** number - **Default:** `1`  
           **Description:** The size in MB before data should be delivered
-   [Logging](#Logging) - Optional - **Type:** boolean - **Default:** `true`  
-   [Encrypted](#Encrypted) - Optional - **Type:** boolean - **Default:** `false`  
-   [Backup](#Backup)
    -   [FailureDuration](#FailureDuration) - Optional - **Type:** number - **Default:** `3600`  
           **Description:** The time in seconds that the data feed will attempt to deliver the data before it is sent to backup
    -   [Policy](#Policy) - Optional - **Type:** string - **Default:** `FailedDocumentsOnly`  
           **Description:** The backup policy to apply to records  **Possible Values:** `[AllDocuments, FailedDocumentsOnly]`
-   [Destination](#Destination)
    -   [Link](#Link)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [LogWatchers](#LogWatchers)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# datapipeline

Managed Data ETL Processing

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"datapipeline" : {
		"Fragment" : "<string>",
		"Permissions" : {
			"Decrypt" : true,
			"AsFile" : true,
			"AppData" : true,
			"AppPublic" : true
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Permissions](#Permissions)
    -   [Decrypt](#Decrypt) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppData](#AppData) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppPublic](#AppPublic) - Optional - **Type:** boolean - **Default:** `true`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  

```

</TabItem>
</Tabs>

# dataset

A data aretefact that is managed in a similar way to a code unit

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"dataset" : {
		"Engine" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Prefix" : "<string>",
		"BuildEnvironment" : "<array of string>"
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Required - **Type:** string  
    **Possible Values:** `[s3, rds]`
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Prefix](#Prefix) - Optional - **Type:** string  
-   [BuildEnvironment](#BuildEnvironment) - Required - **Type:** array of string  
    **Description:** The environments used to build the dataset

```

</TabItem>
</Tabs>

# datavolume

A persistant disk volume independent of compute

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"datavolume" : {
		"Engine" : "ebs",
		"Encrypted" : false,
		"Size" : 20,
		"VolumeType" : "gp2",
		"ProvisionedIops" : 100,
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Backup" : {
			"Enabled" : true,
			"Schedule" : "rate(1 day)",
			"ScheduleTimeZone" : "Etc/UTC",
			"RetentionPeriod" : 35
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Optional - **Type:** string - **Default:** `ebs`  
    **Possible Values:** `[ebs]`
-   [Encrypted](#Encrypted) - Optional - **Type:** boolean - **Default:** `false`  
-   [Size](#Size) - Optional - **Type:** number - **Default:** `20`  
-   [VolumeType](#VolumeType) - Optional - **Type:** string - **Default:** `gp2`  
    **Possible Values:** `[standard, io1, gp2, sc1, st1]`
-   [ProvisionedIops](#ProvisionedIops) - Optional - **Type:** number - **Default:** `100`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [Backup](#Backup)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Create scheduled snapshots of the data volume
    -   [Schedule](#Schedule) - Optional - **Type:** string - **Default:** `rate(1 day)`  
           **Description:** Schedule in rate() or cron() formats
    -   [ScheduleTimeZone](#ScheduleTimeZone) - Optional - **Type:** string - **Default:** `Etc/UTC`  
           **Description:** When using a cron expression in Schedule sets the time zone to base it from
    -   [RetentionPeriod](#RetentionPeriod) - Optional - **Type:** number - **Default:** `35`  
           **Description:** How long to keep snapshot for in days

```

</TabItem>
</Tabs>

# ec2

A single virtual machine with no code deployment 

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"ec2" : {
		"FixedIP" : false,
		"DockerHost" : false,
		"Fragment" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"Ports" : {
			"example" : {
				"IPAddressGroups" : "<array of string>",
				"LB" : {
					"Tier" : "<string>",
					"Component" : "<string>",
					"LinkName" : "lb",
					"Instance" : "<string>",
					"Version" : "<string>",
					"PortMapping" : "<string>"
				}
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [FixedIP](#FixedIP) - Optional - **Type:** boolean - **Default:** `false`  
-   [DockerHost](#DockerHost) - Optional - **Type:** boolean - **Default:** `false`  
-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [Ports](#Ports)
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
    -   [LB](#LB)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [LinkName](#LinkName) - Optional - **Type:** string - **Default:** `lb`  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  

```

</TabItem>
</Tabs>

# ecs

An autoscaling container host cluster

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Sub Components**

-   [service](#service)
    -   **Component Attribute** - Services
    -   **Link Attribute** - Service
-   [task](#task)
    -   **Component Attribute** - Tasks
    -   **Link Attribute** - Task


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"ecs" : {
		"Fragment" : "<string>",
		"FixedIP" : false,
		"LogDriver" : "awslogs",
		"VolumeDrivers" : "<array of string>",
		"ClusterLogGroup" : true,
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"AutoScaling" : {
			"DetailedMetrics" : true,
			"WaitForSignal" : true,
			"MinUpdateInstances" : 1,
			"ReplaceCluster" : false,
			"UpdatePauseTime" : "10M",
			"StartupTimeout" : "15M",
			"AlwaysReplaceOnUpdate" : false,
			"ActivityCooldown" : 30
		},
		"DockerUsers" : {
			"example" : {
				"UserName" : "<string>",
				"UID" : "<number>"
			}
		},
		"LogMetrics" : {
			"example" : {
				"LogFilter" : "<string>"
			}
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"Hibernate" : {
			"Enabled" : false,
			"StartUpMode" : "replace"
		},
		"Services" : {
			"example" : "< instance of service>"
		},
		"Tasks" : {
			"example" : "< instance of task>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [FixedIP](#FixedIP) - Optional - **Type:** boolean - **Default:** `false`  
-   [LogDriver](#LogDriver) - Optional - **Type:** string - **Default:** `awslogs`  
    **Possible Values:** `[awslogs, json-file, fluentd]`
-   [VolumeDrivers](#VolumeDrivers) - Optional - **Type:** array of string  
    **Possible Values:** `[ebs]`
-   [ClusterLogGroup](#ClusterLogGroup) - Optional - **Type:** boolean - **Default:** `true`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [AutoScaling](#AutoScaling)
    -   [DetailedMetrics](#DetailedMetrics) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Enable the collection of autoscale group detailed metrics
    -   [WaitForSignal](#WaitForSignal) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Wait for a cfn-signal before treating the instances as alive
    -   [MinUpdateInstances](#MinUpdateInstances) - Optional - **Type:** number - **Default:** `1`  
           **Description:** The minimum number of instances which must be available during an update
    -   [ReplaceCluster](#ReplaceCluster) - Optional - **Type:** boolean - **Default:** `false`  
           **Description:** When set to true a brand new cluster will be built, if false the instances in the current cluster will be replaced
    -   [UpdatePauseTime](#UpdatePauseTime) - Optional - **Type:** string - **Default:** `10M`  
           **Description:** How long to pause betweeen updates of instances
    -   [StartupTimeout](#StartupTimeout) - Optional - **Type:** string - **Default:** `15M`  
           **Description:** How long to wait for a cfn-signal to be received from a host
    -   [AlwaysReplaceOnUpdate](#AlwaysReplaceOnUpdate) - Optional - **Type:** boolean - **Default:** `false`  
           **Description:** Replace instances on every update action
    -   [ActivityCooldown](#ActivityCooldown) - Optional - **Type:** number - **Default:** `30`  
-   [DockerUsers](#DockerUsers)
    -   [UserName](#UserName) - Optional - **Type:** string  
    -   [UID](#UID) - Required - **Type:** number  
-   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [Hibernate](#Hibernate)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
    -   [StartUpMode](#StartUpMode) - Optional - **Type:** string - **Default:** `replace`  
           **Possible Values:** `[replace]`

```

</TabItem>
</Tabs>

# service

An orchestrated container with always on scheduling

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"service" : {
		"Engine" : "ec2",
		"Containers" : {
			"example" : {
				"Cpu" : "<number>",
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				},
				"LocalLogging" : false,
				"LogDriver" : "awslogs",
				"LogMetrics" : {
					"example" : {
						"LogFilter" : "<string>"
					}
				},
				"Alerts" : {
					"example" : {
						"Description" : "unknown",
						"Name" : "<string>",
						"Resource" : {
							"Id" : "<string>",
							"Type" : "<string>"
						},
						"Metric" : "<string>",
						"Threshold" : 1,
						"Severity" : "Info",
						"Namespace" : "<string>",
						"Comparison" : "Threshold",
						"Operator" : "GreaterThanOrEqualToThreshold",
						"Time" : 300,
						"Periods" : 1,
						"Statistic" : "Sum",
						"ReportOk" : false,
						"MissingData" : "notBreaching"
					}
				},
				"ContainerLogGroup" : false,
				"RunCapabilities" : "<array of string>",
				"Privileged" : false,
				"MaximumMemory" : "<unknown>",
				"MemoryReservation" : "<number>",
				"Ports" : {
					"example" : {
						"Container" : "unknown",
						"DynamicHostPort" : false,
						"LB" : {
							"Tier" : "<string>",
							"Component" : "<string>",
							"LinkName" : "lb",
							"Instance" : "<string>",
							"Version" : "<string>",
							"PortMapping" : "<string>"
						},
						"Registry" : {
							"Tier" : "<string>",
							"Component" : "<string>",
							"LinkName" : "srvreg",
							"Instance" : "<string>",
							"Version" : "<string>",
							"RegistryService" : "<string>"
						},
						"IPAddressGroups" : "<array of string>"
					}
				},
				"Version" : "<string>",
				"ContainerNetworkLinks" : "<array of string>"
			}
		},
		"DesiredCount" : -1,
		"UseTaskRole" : true,
		"Permissions" : {
			"Decrypt" : true,
			"AsFile" : true,
			"AppData" : true,
			"AppPublic" : true
		},
		"TaskLogGroup" : true,
		"LogMetrics" : {
			"example" : {
				"LogFilter" : "<string>"
			}
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"NetworkMode" : "<string>",
		"ContainerNetworkLinks" : false,
		"Placement" : {
			"Strategy" : "<string>"
		},
		"Profiles" : {
			"Deployment" : "<array of string>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Optional - **Type:** string - **Default:** `ec2`  
    **Possible Values:** `[ec2, fargate]`
-   [Containers](#Containers)
    -   [Cpu](#Cpu) - Optional - **Type:** number  
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
    -   [LocalLogging](#LocalLogging) - Optional - **Type:** boolean - **Default:** `false`  
    -   [LogDriver](#LogDriver) - Optional - **Type:** string - **Default:** `awslogs`  
           **Possible Values:** `[awslogs, json-file, fluentd]`
    -   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
    -   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
    -   [ContainerLogGroup](#ContainerLogGroup) - Optional - **Type:** boolean - **Default:** `false`  
    -   [RunCapabilities](#RunCapabilities) - Optional - **Type:** array of string  
    -   [Privileged](#Privileged) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MaximumMemory](#MaximumMemory) _(MemoryMaximum, MaxMemory)_ - Optional  
           **Types:** number  **Description:** Set to 0 to not set a maximum
    -   [MemoryReservation](#MemoryReservation) _(Memory, ReservedMemory)_ - Required - **Type:** number  
    -   [Ports](#Ports)
    -   [Container](#Container) - Optional  
    -   [DynamicHostPort](#DynamicHostPort) - Optional - **Type:** boolean - **Default:** `false`  
    -   [LB](#LB)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [LinkName](#LinkName) - Optional - **Type:** string - **Default:** `lb`  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Registry](#Registry)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [LinkName](#LinkName) - Optional - **Type:** string - **Default:** `srvreg`  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [ContainerNetworkLinks](#ContainerNetworkLinks) - Optional - **Type:** array of string  
-   [DesiredCount](#DesiredCount) - Optional - **Type:** number - **Default:** `-1`  
-   [UseTaskRole](#UseTaskRole) - Optional - **Type:** boolean - **Default:** `true`  
-   [Permissions](#Permissions)
    -   [Decrypt](#Decrypt) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppData](#AppData) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppPublic](#AppPublic) - Optional - **Type:** boolean - **Default:** `true`  
-   [TaskLogGroup](#TaskLogGroup) - Optional - **Type:** boolean - **Default:** `true`  
-   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [NetworkMode](#NetworkMode) - Optional - **Type:** string  
    **Possible Values:** `[none, bridge, awsvpc, host]`
-   [ContainerNetworkLinks](#ContainerNetworkLinks) - Optional - **Type:** boolean - **Default:** `false`  
-   [Placement](#Placement)
    -   [Strategy](#Strategy) - Optional - **Type:** string  
           **Possible Values:** `[, daemon]`  **Description:** How to place containers on the cluster
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  

```

</TabItem>
</Tabs>

# task

A container defintion which is invoked on demand

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"task" : {
		"Engine" : "ec2",
		"Containers" : {
			"example" : {
				"Cpu" : "<number>",
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				},
				"LocalLogging" : false,
				"LogDriver" : "awslogs",
				"LogMetrics" : {
					"example" : {
						"LogFilter" : "<string>"
					}
				},
				"Alerts" : {
					"example" : {
						"Description" : "unknown",
						"Name" : "<string>",
						"Resource" : {
							"Id" : "<string>",
							"Type" : "<string>"
						},
						"Metric" : "<string>",
						"Threshold" : 1,
						"Severity" : "Info",
						"Namespace" : "<string>",
						"Comparison" : "Threshold",
						"Operator" : "GreaterThanOrEqualToThreshold",
						"Time" : 300,
						"Periods" : 1,
						"Statistic" : "Sum",
						"ReportOk" : false,
						"MissingData" : "notBreaching"
					}
				},
				"ContainerLogGroup" : false,
				"RunCapabilities" : "<array of string>",
				"Privileged" : false,
				"MaximumMemory" : "<unknown>",
				"MemoryReservation" : "<number>",
				"Ports" : {
					"example" : {
						"Container" : "unknown",
						"DynamicHostPort" : false,
						"LB" : {
							"Tier" : "<string>",
							"Component" : "<string>",
							"LinkName" : "lb",
							"Instance" : "<string>",
							"Version" : "<string>",
							"PortMapping" : "<string>"
						},
						"Registry" : {
							"Tier" : "<string>",
							"Component" : "<string>",
							"LinkName" : "srvreg",
							"Instance" : "<string>",
							"Version" : "<string>",
							"RegistryService" : "<string>"
						},
						"IPAddressGroups" : "<array of string>"
					}
				},
				"Version" : "<string>",
				"ContainerNetworkLinks" : "<array of string>"
			}
		},
		"UseTaskRole" : true,
		"Permissions" : {
			"Decrypt" : true,
			"AsFile" : true,
			"AppData" : true,
			"AppPublic" : true
		},
		"TaskLogGroup" : true,
		"LogMetrics" : {
			"example" : {
				"LogFilter" : "<string>"
			}
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"NetworkMode" : "<string>",
		"FixedName" : false,
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Schedules" : {
			"example" : {
				"Expression" : "rate(1 hours)",
				"TaskCount" : 1
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Optional - **Type:** string - **Default:** `ec2`  
    **Possible Values:** `[ec2, fargate]`
-   [Containers](#Containers)
    -   [Cpu](#Cpu) - Optional - **Type:** number  
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
    -   [LocalLogging](#LocalLogging) - Optional - **Type:** boolean - **Default:** `false`  
    -   [LogDriver](#LogDriver) - Optional - **Type:** string - **Default:** `awslogs`  
           **Possible Values:** `[awslogs, json-file, fluentd]`
    -   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
    -   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
    -   [ContainerLogGroup](#ContainerLogGroup) - Optional - **Type:** boolean - **Default:** `false`  
    -   [RunCapabilities](#RunCapabilities) - Optional - **Type:** array of string  
    -   [Privileged](#Privileged) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MaximumMemory](#MaximumMemory) _(MemoryMaximum, MaxMemory)_ - Optional  
           **Types:** number  **Description:** Set to 0 to not set a maximum
    -   [MemoryReservation](#MemoryReservation) _(Memory, ReservedMemory)_ - Required - **Type:** number  
    -   [Ports](#Ports)
    -   [Container](#Container) - Optional  
    -   [DynamicHostPort](#DynamicHostPort) - Optional - **Type:** boolean - **Default:** `false`  
    -   [LB](#LB)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [LinkName](#LinkName) - Optional - **Type:** string - **Default:** `lb`  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Registry](#Registry)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [LinkName](#LinkName) - Optional - **Type:** string - **Default:** `srvreg`  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [ContainerNetworkLinks](#ContainerNetworkLinks) - Optional - **Type:** array of string  
-   [UseTaskRole](#UseTaskRole) - Optional - **Type:** boolean - **Default:** `true`  
-   [Permissions](#Permissions)
    -   [Decrypt](#Decrypt) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppData](#AppData) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppPublic](#AppPublic) - Optional - **Type:** boolean - **Default:** `true`  
-   [TaskLogGroup](#TaskLogGroup) - Optional - **Type:** boolean - **Default:** `true`  
-   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [NetworkMode](#NetworkMode) - Optional - **Type:** string  
    **Possible Values:** `[none, bridge, awsvpc, host]`
-   [FixedName](#FixedName) - Optional - **Type:** boolean - **Default:** `false`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [Schedules](#Schedules)
    -   [Expression](#Expression) - Optional - **Type:** string - **Default:** `rate(1 hours)`  
    -   [TaskCount](#TaskCount) - Optional - **Type:** number - **Default:** `1`  
           **Description:** The number of tasks to run on the schedule

```

</TabItem>
</Tabs>

# efs

A managed network attached file share

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Sub Components**

-   [efsMount](#efsMount)
    -   **Component Attribute** - Mounts
    -   **Link Attribute** - Mount


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"efs" : {
		"Encrypted" : true,
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Mounts" : {
			"example" : "< instance of efsMount>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Encrypted](#Encrypted) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  

```

</TabItem>
</Tabs>

# efsmount

A specific directory on the share for OS mounting

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"efsMount" : {
		"Directory" : "<string>"
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Directory](#Directory) - Required - **Type:** string  

```

</TabItem>
</Tabs>

# es

A managed ElasticSearch instance

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"es" : {
		"Authentication" : "IP",
		"Accounts" : [
			"_environment"
		],
		"IPAddressGroups" : "<array of string>",
		"AdvancedOptions" : "<array of string>",
		"Version" : "<string>",
		"Encrypted" : false,
		"Snapshot" : {
			"Hour" : "<string>"
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Authentication](#Authentication) - Optional - **Type:** string - **Default:** `IP`  
    **Possible Values:** `[IP, SIG4ORIP, SIG4ANDIP]`
-   [Accounts](#Accounts) - Optional - **Type:** array of string - **Default:** `_environment`  
    **Description:** A list of accounts which will be permitted to access the ES index
-   [IPAddressGroups](#IPAddressGroups) - Required - **Type:** array of string  
    **Description:** A list of IP Address Groups which will be permitted to access the ES index
-   [AdvancedOptions](#AdvancedOptions) - Optional - **Type:** array of string  
-   [Version](#Version) - Required - **Type:** string  
-   [Encrypted](#Encrypted) - Optional - **Type:** boolean - **Default:** `false`  
-   [Snapshot](#Snapshot)
    -   [Hour](#Hour) - Optional - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  

```

</TabItem>
</Tabs>

# lambda

Container for a Function as a Service deployment

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application

**Sub Components**

-   [function](#function)
    -   **Component Attribute** - Functions
    -   **Link Attribute** - Function


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"lambda" : {
		"DeploymentType" : "REGIONAL",
		"Functions" : {
			"example" : "< instance of function>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [DeploymentType](#DeploymentType) - Optional - **Type:** string - **Default:** `REGIONAL`  
    **Possible Values:** `[EDGE, REGIONAL]`

```

</TabItem>
</Tabs>

# function

A specific entry point for the lambda deployment

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"function" : {
		"Fragment" : "<string>",
		"Handler" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"LogMetrics" : {
			"example" : {
				"LogFilter" : "<string>"
			}
		},
		"LogWatchers" : {
			"example" : {
				"LogFilter" : "<string>",
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				}
			}
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"Memory" : 0,
		"RunTime" : "<string>",
		"Schedules" : {
			"example" : {
				"Expression" : "rate(6 minutes)",
				"InputPath" : "/healthcheck",
				"Input" : "<object>"
			}
		},
		"Timeout" : 0,
		"VPCAccess" : true,
		"UseSegmentKey" : false,
		"Permissions" : {
			"Decrypt" : true,
			"AsFile" : true,
			"AppData" : true,
			"AppPublic" : true
		},
		"PredefineLogGroup" : false,
		"Environment" : {
			"AsFile" : false,
			"Json" : {
				"Escaped" : true,
				"Prefix" : "json"
			}
		},
		"FixedCodeVersion" : {
			"CodeHash" : "<unknown>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Handler](#Handler) - Required - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
-   [LogWatchers](#LogWatchers)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [Memory](#Memory) _(MemorySize)_ - Optional - **Type:** number - **Default:** `0`  
-   [RunTime](#RunTime) - Required - **Type:** string  
    **Possible Values:** `[nodejs, nodejs4.3, nodejs6.10, nodejs8.10, java8, python2.7, python3.6, dotnetcore1.0, dotnetcore2.0, dotnetcore2.1, nodejs4.3-edge, go1.x]`
-   [Schedules](#Schedules)
    -   [Expression](#Expression) - Optional - **Type:** string - **Default:** `rate(6 minutes)`  
    -   [InputPath](#InputPath) - Optional - **Type:** string - **Default:** `/healthcheck`  
    -   [Input](#Input) - Optional - **Type:** object  
-   [Timeout](#Timeout) - Optional - **Type:** number - **Default:** `0`  
-   [VPCAccess](#VPCAccess) - Optional - **Type:** boolean - **Default:** `true`  
-   [UseSegmentKey](#UseSegmentKey) - Optional - **Type:** boolean - **Default:** `false`  
-   [Permissions](#Permissions)
    -   [Decrypt](#Decrypt) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppData](#AppData) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppPublic](#AppPublic) - Optional - **Type:** boolean - **Default:** `true`  
-   [PredefineLogGroup](#PredefineLogGroup) - Optional - **Type:** boolean - **Default:** `false`  
-   [Environment](#Environment)
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Json](#Json)
    -   [Escaped](#Escaped) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Prefix](#Prefix) - Optional - **Type:** string - **Default:** `json`  
                  **Possible Values:** `[json, ]`
-   [FixedCodeVersion](#FixedCodeVersion)
    -   [CodeHash](#CodeHash) - Optional  
           **Description:** A sha256 hash of the code zip file

```

</TabItem>
</Tabs>

# lb

A load balancer for virtual network based components

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Notes**

!!! warning
    Requires second deployment to complete configuration

**Sub Components**

-   [lbport](#lbport)
    -   **Component Attribute** - PortMappings
    -   **Link Attribute** - PortMapping, Port


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"lb" : {
		"Logs" : false,
		"Engine" : "application",
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Security" : "default"
		},
		"IdleTimeout" : 60,
		"HealthCheckPort" : "<string>",
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"PortMappings" : {
			"example" : "< instance of lbport>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Logs](#Logs) - Optional - **Type:** boolean - **Default:** `false`  
-   [Engine](#Engine) - Optional - **Type:** string - **Default:** `application`  
    **Possible Values:** `[application, network, classic]`
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Security](#Security) - Optional - **Type:** string - **Default:** `default`  
-   [IdleTimeout](#IdleTimeout) - Optional - **Type:** number - **Default:** `60`  
-   [HealthCheckPort](#HealthCheckPort) - Optional - **Type:** string  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# lbport

A specifc listener based on the client side network port

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"lbport" : {
		"IPAddressGroups" : "<array of string>",
		"Certificate" : {
			"Qualifiers" : "<object>",
			"Domain" : "<string>",
			"IncludeInDomain" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>"
			},
			"Host" : "<string>",
			"HostParts" : "<array of string>",
			"IncludeInHost" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>",
				"Tier" : "<boolean>",
				"Component" : "<boolean>",
				"Instance" : "<boolean>",
				"Version" : "<boolean>",
				"Host" : "<boolean>"
			},
			"External" : "<boolean>",
			"Wildcard" : "<boolean>"
		},
		"HostFilter" : false,
		"Mapping" : "<string>",
		"Path" : "default",
		"Priority" : 100,
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Authentication" : {
			"SessionCookieName" : "AWSELBAuthSessionCookie",
			"SessionTimeout" : 604800
		},
		"Redirect" : {
			"Protocol" : "HTTPS",
			"Port" : "443",
			"Host" : "#{host}",
			"Path" : "/#{path}",
			"Query" : "#{query}",
			"Permanent" : true
		},
		"Fixed" : {
			"Message" : "This application is currently unavailable. Please try again later.",
			"ContentType" : "text/plain",
			"StatusCode" : "404"
		},
		"Forward" : {
			"TargetType" : "instance",
			"SlowStartTime" : -1,
			"StickinessTime" : -1,
			"DeregistrationTimeout" : 30
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
-   [Certificate](#Certificate)
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [Domain](#Domain) - Optional - **Type:** string  
    -   [IncludeInDomain](#IncludeInDomain)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** string  
    -   [HostParts](#HostParts) - Optional - **Type:** array of string  
    -   [IncludeInHost](#IncludeInHost)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Tier](#Tier) - Optional - **Type:** boolean  
    -   [Component](#Component) - Optional - **Type:** boolean  
    -   [Instance](#Instance) - Optional - **Type:** boolean  
    -   [Version](#Version) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** boolean  
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [External](#External) - Optional - **Type:** boolean  
    -   [Wildcard](#Wildcard) - Optional - **Type:** boolean  
-   [HostFilter](#HostFilter) - Optional - **Type:** boolean - **Default:** `false`  
-   [Mapping](#Mapping) - Optional - **Type:** string  
-   [Path](#Path) - Optional - **Type:** string - **Default:** `default`  
-   [Priority](#Priority) - Optional - **Type:** number - **Default:** `100`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Authentication](#Authentication)
    -   [SessionCookieName](#SessionCookieName) - Optional - **Type:** string - **Default:** `AWSELBAuthSessionCookie`  
    -   [SessionTimeout](#SessionTimeout) - Optional - **Type:** number - **Default:** `604800`  
-   [Redirect](#Redirect)
    -   [Protocol](#Protocol) - Optional - **Type:** string - **Default:** `HTTPS`  
           **Possible Values:** `[HTTPS, #{protocol}]`
    -   [Port](#Port) - Optional - **Type:** string - **Default:** `443`  
    -   [Host](#Host) - Optional - **Type:** string - **Default:** `#{host}`  
    -   [Path](#Path) - Optional - **Type:** string - **Default:** `/#{path}`  
    -   [Query](#Query) - Optional - **Type:** string - **Default:** `#{query}`  
    -   [Permanent](#Permanent) - Optional - **Type:** boolean - **Default:** `true`  
-   [Fixed](#Fixed)
    -   [Message](#Message) - Optional - **Type:** string - **Default:** `This application is currently unavailable. Please try again later.`  
    -   [ContentType](#ContentType) - Optional - **Type:** string - **Default:** `text/plain`  
    -   [StatusCode](#StatusCode) - Optional - **Type:** string - **Default:** `404`  
-   [Forward](#Forward)
    -   [TargetType](#TargetType) - Optional - **Type:** string - **Default:** `instance`  
           **Possible Values:** `[instance, ip]`
    -   [SlowStartTime](#SlowStartTime) - Optional - **Type:** number - **Default:** `-1`  
    -   [StickinessTime](#StickinessTime) - Optional - **Type:** number - **Default:** `-1`  
    -   [DeregistrationTimeout](#DeregistrationTimeout) - Optional - **Type:** number - **Default:** `30`  

```

</TabItem>
</Tabs>

# mobileapp

mobile apps with over the air update hosting

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"mobileapp" : {
		"Engine" : "expo",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"BuildFormats" : [
			"ios",
			"android"
		],
		"Fragment" : "<string>"
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Optional - **Type:** string - **Default:** `expo`  
    **Possible Values:** `[expo]`
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [BuildFormats](#BuildFormats) - Optional - **Type:** array of string - **Default:** `ios, android`  
    **Possible Values:** `[ios, android]`
-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  

```

</TabItem>
</Tabs>

# mobilenotifier

A managed mobile notification proxy

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Sub Components**

-   [mobilenotiferplatform](#mobilenotiferplatform)
    -   **Component Attribute** - Platforms
    -   **Link Attribute** - Platform


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"mobilenotifier" : {
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"SuccessSampleRate" : "100",
		"Credentials" : {
			"EncryptionScheme" : "base64"
		},
		"Platforms" : {
			"example" : "< instance of mobilenotiferplatform>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [SuccessSampleRate](#SuccessSampleRate) - Optional - **Type:** string - **Default:** `100`  
-   [Credentials](#Credentials)
    -   [EncryptionScheme](#EncryptionScheme) - Optional - **Type:** string - **Default:** `base64`  
           **Possible Values:** `[base64]`

```

</TabItem>
</Tabs>

# mobilenotiferplatform

A specific mobile platform notification proxy

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Notes**

!!! warning
    SMS Engine requires account level configuration for AWS provider
!!! info
    Platform specific credentials are required and must be provided as credentials


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"mobilenotiferplatform" : {
		"Engine" : "<string>",
		"SuccessSampleRate" : "<string>",
		"Credentials" : {
			"EncryptionScheme" : "<string>"
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"LogMetrics" : {
			"example" : {
				"LogFilter" : "<string>"
			}
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Optional - **Type:** string  
-   [SuccessSampleRate](#SuccessSampleRate) - Optional - **Type:** string  
-   [Credentials](#Credentials)
    -   [EncryptionScheme](#EncryptionScheme) - Optional - **Type:** string  
           **Possible Values:** `[base64]`
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [LogMetrics](#LogMetrics)
    -   [LogFilter](#LogFilter) - Required - **Type:** string  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  

```

</TabItem>
</Tabs>

# network

A virtual network segment used by private resources

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment

**Sub Components**

-   [networkroute](#networkroute)
    -   **Component Attribute** - RouteTables
    -   **Link Attribute** - RouteTable
-   [networkacl](#networkacl)
    -   **Component Attribute** - NetworkACLs
    -   **Link Attribute** - NetworkACL


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"network" : {
		"Active" : false,
		"Logging" : {
			"EnableFlowLogs" : true
		},
		"DNS" : {
			"UseProvider" : true,
			"GenerateHostNames" : true
		},
		"Address" : {
			"CIDR" : "10.0.0.0/16"
		},
		"RouteTables" : {
			"example" : "< instance of networkroute>"
		},
		"NetworkACLs" : {
			"example" : "< instance of networkacl>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [Logging](#Logging)
    -   [EnableFlowLogs](#EnableFlowLogs) - Optional - **Type:** boolean - **Default:** `true`  
-   [DNS](#DNS)
    -   [UseProvider](#UseProvider) - Optional - **Type:** boolean - **Default:** `true`  
    -   [GenerateHostNames](#GenerateHostNames) - Optional - **Type:** boolean - **Default:** `true`  
-   [Address](#Address)
    -   [CIDR](#CIDR) - Optional - **Type:** string - **Default:** `10.0.0.0/16`  

```

</TabItem>
</Tabs>

# networkroute

A network routing table providing acess to resources outside of the network

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"networkroute" : {
		"Active" : false,
		"Public" : false,
		"Profiles" : {
			"Deployment" : "<array of string>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [Public](#Public) - Optional - **Type:** boolean - **Default:** `false`  
    **Description:** Does the route table require Public IP internet access
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  

```

</TabItem>
</Tabs>

# networkacl

A tier/subnet level network access control policy

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"networkacl" : {
		"Active" : false,
		"Rules" : {
			"example" : {
				"Priority" : "<number>",
				"Action" : "deny",
				"Source" : {
					"IPAddressGroups" : "<array of string>",
					"Port" : "ephemeraltcp"
				},
				"Destination" : {
					"IPAddressGroups" : "<array of string>",
					"Port" : "<string>"
				},
				"ReturnTraffic" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [Rules](#Rules)
    -   [Priority](#Priority) - Optional - **Type:** number  
           **Required:** true
    -   [Action](#Action) - Optional - **Type:** string - **Default:** `deny`  
           **Possible Values:** `[allow, deny]`
    -   [Source](#Source)
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
                  **Required:** true
    -   [Port](#Port) - Optional - **Type:** string - **Default:** `ephemeraltcp`  
                  **Description:** Port or port range the source is coming from
    -   [Destination](#Destination)
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
                  **Required:** true
    -   [Port](#Port) - Optional - **Type:** string  
                  **Description:** Port or port range the source is trying to access  **Required:** true
    -   [ReturnTraffic](#ReturnTraffic) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** If ACL is stateless add a return rule

```

</TabItem>
</Tabs>

# gateway

A service providing a route to another network

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment

**Sub Components**

-   [gatewaydestination](#gatewaydestination)
    -   **Component Attribute** - Destinations
    -   **Link Attribute** - Destination


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"gateway" : {
		"Active" : false,
		"Engine" : "<string>",
		"SourceIPAddressGroups" : [
			"_localnet"
		],
		"Destinations" : {
			"example" : "< instance of gatewaydestination>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [Engine](#Engine) - Optional - **Type:** string  
    **Possible Values:** `[natgw, igw, vpcendpoint]`  **Required:** true
-   [SourceIPAddressGroups](#SourceIPAddressGroups) - Optional - **Type:** array of string - **Default:** `_localnet`  
    **Description:** IP Address Groups which can access this gateway

```

</TabItem>
</Tabs>

# gatewaydestination

A network destination offerred by the Gateway

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - segment


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"gatewaydestination" : {
		"Active" : false,
		"IPAddressGroups" : "<array of string>",
		"NetworkEndpointGroups" : "<array of string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Active](#Active) - Optional - **Type:** boolean - **Default:** `false`  
-   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string  
    **Description:** An IP Address Group reference
-   [NetworkEndpointGroups](#NetworkEndpointGroups) - Optional - **Type:** array of string  
    **Description:** A cloud provider service group reference
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# rds

A managed SQL database instance

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"rds" : {
		"Engine" : "<unknown>",
		"EngineVersion" : "<string>",
		"Port" : "<string>",
		"Encrypted" : false,
		"GenerateCredentials" : {
			"Enabled" : false,
			"MasterUserName" : "root",
			"CharacterLength" : 20,
			"EncryptionScheme" : "<string>"
		},
		"Size" : 20,
		"Backup" : {
			"RetentionPeriod" : 35,
			"SnapshotOnDeploy" : true,
			"DeleteAutoBackups" : true,
			"DeletionPolicy" : "Snapshot",
			"UpdateReplacePolicy" : "Snapshot"
		},
		"AutoMinorVersionUpgrade" : "<boolean>",
		"DatabaseName" : "<string>",
		"DBParameters" : "<object>",
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Processor" : "default"
		},
		"Hibernate" : {
			"Enabled" : false,
			"StartUpMode" : "restore"
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"AlwaysCreateFromSnapshot" : false
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Required  
-   [EngineVersion](#EngineVersion) - Optional - **Type:** string  
-   [Port](#Port) - Optional - **Type:** string  
-   [Encrypted](#Encrypted) - Optional - **Type:** boolean - **Default:** `false`  
-   [GenerateCredentials](#GenerateCredentials)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MasterUserName](#MasterUserName) - Optional - **Type:** string - **Default:** `root`  
    -   [CharacterLength](#CharacterLength) - Optional - **Type:** number - **Default:** `20`  
    -   [EncryptionScheme](#EncryptionScheme) - Optional - **Type:** string  
           **Possible Values:** `[base64]`
-   [Size](#Size) - Optional - **Type:** number - **Default:** `20`  
-   [Backup](#Backup)
    -   [RetentionPeriod](#RetentionPeriod) - Optional - **Type:** number - **Default:** `35`  
    -   [SnapshotOnDeploy](#SnapshotOnDeploy) - Optional - **Type:** boolean - **Default:** `true`  
    -   [DeleteAutoBackups](#DeleteAutoBackups) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Delete automated snapshots when the instance is deleted
    -   [DeletionPolicy](#DeletionPolicy) - Optional - **Type:** string - **Default:** `Snapshot`  
           **Possible Values:** `[Snapshot, Delete, Retain]`
    -   [UpdateReplacePolicy](#UpdateReplacePolicy) - Optional - **Type:** string - **Default:** `Snapshot`  
           **Possible Values:** `[Snapshot, Delete, Retain]`
-   [AutoMinorVersionUpgrade](#AutoMinorVersionUpgrade) - Optional - **Type:** boolean  
-   [DatabaseName](#DatabaseName) - Optional - **Type:** string  
-   [DBParameters](#DBParameters) - Optional - **Type:** object  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Processor](#Processor) - Optional - **Type:** string - **Default:** `default`  
-   [Hibernate](#Hibernate)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
    -   [StartUpMode](#StartUpMode) - Optional - **Type:** string - **Default:** `restore`  
           **Possible Values:** `[restore, replace]`
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [AlwaysCreateFromSnapshot](#AlwaysCreateFromSnapshot) - Optional - **Type:** boolean - **Default:** `false`  
    **Description:** Always create the database from a snapshot

```

</TabItem>
</Tabs>

# s3

HTTP based object storage service

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"s3" : {
		"Lifecycle" : {
			"Expiration" : "<unknown>",
			"Offline" : "<unknown>",
			"Versioning" : false
		},
		"Website" : {
			"Index" : "index.html",
			"Error" : "<string>"
		},
		"PublicAccess" : {
			"example" : {
				"Enabled" : false,
				"Permissions" : "ro",
				"IPAddressGroups" : [
					"_localnet"
				],
				"Paths" : "<array of string>"
			}
		},
		"Style" : "<string>",
		"Notifications" : {
			"example" : {
				"Links" : {
					"example" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					}
				},
				"Prefix" : "<string>",
				"Suffix" : "<string>",
				"Events" : [
					"create"
				]
			}
		},
		"CORSBehaviours" : "<array of string>",
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Replication" : {
			"Prefixes" : [
				""
			],
			"Enabled" : true
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Lifecycle](#Lifecycle)
    -   [Expiration](#Expiration) - Optional  
           **Types:** string, number  **Description:** Provide either a date or a number of days
    -   [Offline](#Offline) - Optional  
           **Types:** string, number  **Description:** Provide either a date or a number of days
    -   [Versioning](#Versioning) - Optional - **Type:** boolean - **Default:** `false`  
-   [Website](#Website)
    -   [Index](#Index) - Optional - **Type:** string - **Default:** `index.html`  
    -   [Error](#Error) - Optional - **Type:** string  
-   [PublicAccess](#PublicAccess)
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `false`  
    -   [Permissions](#Permissions) - Optional - **Type:** string - **Default:** `ro`  
           **Possible Values:** `[ro, wo, rw]`
    -   [IPAddressGroups](#IPAddressGroups) - Optional - **Type:** array of string - **Default:** `_localnet`  
    -   [Paths](#Paths) - Optional - **Type:** array of string  
-   [Style](#Style) - Optional - **Type:** string  
    **Description:** TODO(mfl): Think this can be removed
-   [Notifications](#Notifications)
    -   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Prefix](#Prefix) - Optional - **Type:** string  
    -   [Suffix](#Suffix) - Optional - **Type:** string  
    -   [Events](#Events) - Optional - **Type:** array of string - **Default:** `create`  
           **Possible Values:** `[create, remove, restore, reducedredundancy]`
-   [CORSBehaviours](#CORSBehaviours) - Optional - **Type:** array of string  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [Replication](#Replication)
    -   [Prefixes](#Prefixes) - Optional - **Type:** array of string - **Default:** `null`  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# serviceregistry

DNS based service registry

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Sub Components**

-   [serviceregistryservice](#serviceregistryservice)
    -   **Component Attribute** - RegistryServices
    -   **Link Attribute** - RegistryService


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"serviceregistry" : {
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Namespace" : {
			"Qualifiers" : "<object>",
			"Domain" : "<string>",
			"IncludeInDomain" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>"
			}
		},
		"RegistryServices" : {
			"example" : "< instance of serviceregistryservice>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Namespace](#Namespace)
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [Domain](#Domain) - Optional - **Type:** string  
    -   [IncludeInDomain](#IncludeInDomain)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  

```

</TabItem>
</Tabs>

# serviceregistryservice

An individual service in the registry

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"serviceregistryservice" : {
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"ServiceName" : {
			"Host" : "<string>",
			"HostParts" : "<array of string>",
			"IncludeInHost" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>",
				"Tier" : "<boolean>",
				"Component" : "<boolean>",
				"Instance" : "<boolean>",
				"Version" : "<boolean>",
				"Host" : "<boolean>"
			}
		},
		"RecordTypes" : [
			"A"
		],
		"RecordTTL" : 300,
		"RoutingPolicy" : "OnlyOne"
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [ServiceName](#ServiceName)
    -   [Host](#Host) - Optional - **Type:** string  
    -   [HostParts](#HostParts) - Optional - **Type:** array of string  
    -   [IncludeInHost](#IncludeInHost)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Tier](#Tier) - Optional - **Type:** boolean  
    -   [Component](#Component) - Optional - **Type:** boolean  
    -   [Instance](#Instance) - Optional - **Type:** boolean  
    -   [Version](#Version) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** boolean  
-   [RecordTypes](#RecordTypes) - Optional - **Type:** array of string - **Default:** `A`  
    **Description:** The types of DNS records that an instance can register with the service  **Possible Values:** `[A, AAAA, CNAME, SRV]`
-   [RecordTTL](#RecordTTL) - Optional - **Type:** number - **Default:** `300`  
    **Description:** DNS record TTL ( in seconds)
-   [RoutingPolicy](#RoutingPolicy) - Optional - **Type:** string - **Default:** `OnlyOne`  
    **Description:** How the service returns records to the client  **Possible Values:** `[AllAtOnce, OnlyOne]`

```

</TabItem>
</Tabs>

# spa

Object stored hosted web application with content distribution management

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"spa" : {
		"Fragment" : "<string>",
		"Links" : "<object>",
		"WAF" : {
			"IPAddressGroups" : "<array of string>",
			"OWASP" : false
		},
		"CloudFront" : {
			"AssumeSNI" : true,
			"EnableLogging" : true,
			"CountryGroups" : "<array of string>",
			"ErrorPage" : "/index.html",
			"DeniedPage" : "<string>",
			"NotFoundPage" : "<string>",
			"CachingTTL" : {
				"Default" : 600,
				"Maximum" : 31536000,
				"Minimum" : 0
			},
			"Compress" : true,
			"RedirectAliases" : {
				"RedirectVersion" : "v1"
			},
			"EventHandlers" : {
				"example" : {
					"Tier" : "<string>",
					"Component" : "<string>",
					"Function" : "<string>",
					"Instance" : "<string>",
					"Version" : "<string>",
					"Action" : "<string>"
				}
			},
			"Paths" : {
				"example" : {
					"PathPattern" : "<string>",
					"Link" : {
						"Any" : "<string>",
						"Tenant" : "<string>",
						"Product" : "<string>",
						"Environment" : "<string>",
						"Segment" : "<string>",
						"Tier" : "<string>",
						"Component" : "<string>",
						"Function" : "<string>",
						"Service" : "<string>",
						"Task" : "<string>",
						"PortMapping" : "<string>",
						"Mount" : "<string>",
						"Platform" : "<string>",
						"RouteTable" : "<string>",
						"NetworkACL" : "<string>",
						"DataBucket" : "<string>",
						"Key" : "<string>",
						"Branch" : "<string>",
						"Client" : "<string>",
						"AuthProvider" : "<string>",
						"DataFeed" : "<string>",
						"RegistryService" : "<string>",
						"Instance" : "<string>",
						"Version" : "<string>",
						"Role" : "<string>",
						"Direction" : "<string>",
						"Type" : "<string>",
						"Enabled" : true
					},
					"CachingTTL" : {
						"Default" : 600,
						"Maximum" : 31536000,
						"Minimum" : 0
					},
					"Compress" : false
				}
			}
		},
		"Certificate" : {
			"Qualifiers" : "<object>",
			"Domain" : "<string>",
			"IncludeInDomain" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>"
			},
			"Host" : "<string>",
			"HostParts" : "<array of string>",
			"IncludeInHost" : {
				"Product" : "<boolean>",
				"Environment" : "<boolean>",
				"Segment" : "<boolean>",
				"Tier" : "<boolean>",
				"Component" : "<boolean>",
				"Instance" : "<boolean>",
				"Version" : "<boolean>",
				"Host" : "<boolean>"
			},
			"External" : "<boolean>",
			"Wildcard" : "<boolean>"
		},
		"Profiles" : {
			"Deployment" : "<array of string>",
			"Security" : "default"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Links](#Links) - Optional - **Type:** object  
-   [WAF](#WAF)
    -   [IPAddressGroups](#IPAddressGroups) - Required - **Type:** array of string  
    -   [OWASP](#OWASP) - Optional - **Type:** boolean - **Default:** `false`  
-   [CloudFront](#CloudFront)
    -   [AssumeSNI](#AssumeSNI) - Optional - **Type:** boolean - **Default:** `true`  
    -   [EnableLogging](#EnableLogging) - Optional - **Type:** boolean - **Default:** `true`  
    -   [CountryGroups](#CountryGroups) - Optional - **Type:** array of string  
    -   [ErrorPage](#ErrorPage) - Optional - **Type:** string - **Default:** `/index.html`  
    -   [DeniedPage](#DeniedPage) - Optional - **Type:** string  
    -   [NotFoundPage](#NotFoundPage) - Optional - **Type:** string  
    -   [CachingTTL](#CachingTTL)
    -   [Default](#Default) - Optional - **Type:** number - **Default:** `600`  
    -   [Maximum](#Maximum) - Optional - **Type:** number - **Default:** `31536000`  
    -   [Minimum](#Minimum) - Optional - **Type:** number - **Default:** `0`  
    -   [Compress](#Compress) - Optional - **Type:** boolean - **Default:** `true`  
    -   [RedirectAliases](#RedirectAliases)
    -   [RedirectVersion](#RedirectVersion) - Optional - **Type:** string - **Default:** `v1`  
    -   [EventHandlers](#EventHandlers)
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Required - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Action](#Action) - Required - **Type:** string  
                  **Possible Values:** `[viewer-request, viewer-response, origin-request, origin-response]`
    -   [Paths](#Paths)
    -   [PathPattern](#PathPattern) - Required - **Type:** string  
    -   [Link](#Link)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
    -   [CachingTTL](#CachingTTL)
    -   [Default](#Default) - Optional - **Type:** number - **Default:** `600`  
    -   [Maximum](#Maximum) - Optional - **Type:** number - **Default:** `31536000`  
    -   [Minimum](#Minimum) - Optional - **Type:** number - **Default:** `0`  
    -   [Compress](#Compress) - Optional - **Type:** boolean - **Default:** `false`  
-   [Certificate](#Certificate)
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [Domain](#Domain) - Optional - **Type:** string  
    -   [IncludeInDomain](#IncludeInDomain)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** string  
    -   [HostParts](#HostParts) - Optional - **Type:** array of string  
    -   [IncludeInHost](#IncludeInHost)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Tier](#Tier) - Optional - **Type:** boolean  
    -   [Component](#Component) - Optional - **Type:** boolean  
    -   [Instance](#Instance) - Optional - **Type:** boolean  
    -   [Version](#Version) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** boolean  
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [External](#External) - Optional - **Type:** boolean  
    -   [Wildcard](#Wildcard) - Optional - **Type:** boolean  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
    -   [Security](#Security) - Optional - **Type:** string - **Default:** `default`  

```

</TabItem>
</Tabs>

# sqs

Managed worker queue engine

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"sqs" : {
		"DelaySeconds" : "<number>",
		"MaximumMessageSize" : "<number>",
		"MessageRetentionPeriod" : "<number>",
		"ReceiveMessageWaitTimeSeconds" : "<number>",
		"DeadLetterQueue" : {
			"MaxReceives" : 0
		},
		"VisibilityTimeout" : "<number>",
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"Alerts" : {
			"example" : {
				"Description" : "unknown",
				"Name" : "<string>",
				"Resource" : {
					"Id" : "<string>",
					"Type" : "<string>"
				},
				"Metric" : "<string>",
				"Threshold" : 1,
				"Severity" : "Info",
				"Namespace" : "<string>",
				"Comparison" : "Threshold",
				"Operator" : "GreaterThanOrEqualToThreshold",
				"Time" : 300,
				"Periods" : 1,
				"Statistic" : "Sum",
				"ReportOk" : false,
				"MissingData" : "notBreaching"
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [DelaySeconds](#DelaySeconds) - Optional - **Type:** number  
-   [MaximumMessageSize](#MaximumMessageSize) - Optional - **Type:** number  
-   [MessageRetentionPeriod](#MessageRetentionPeriod) - Optional - **Type:** number  
-   [ReceiveMessageWaitTimeSeconds](#ReceiveMessageWaitTimeSeconds) - Optional - **Type:** number  
-   [DeadLetterQueue](#DeadLetterQueue)
    -   [MaxReceives](#MaxReceives) - Optional - **Type:** number - **Default:** `0`  
-   [VisibilityTimeout](#VisibilityTimeout) - Optional - **Type:** number  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [Alerts](#Alerts)
    -   [Description](#Description) - Optional  
    -   [Name](#Name) - Required - **Type:** string  
    -   [Resource](#Resource)
    -   [Id](#Id) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Metric](#Metric) - Required - **Type:** string  
    -   [Threshold](#Threshold) - Optional - **Type:** number - **Default:** `1`  
    -   [Severity](#Severity) - Optional - **Type:** string - **Default:** `Info`  
    -   [Namespace](#Namespace) - Optional - **Type:** string  
    -   [Comparison](#Comparison) - Optional - **Type:** string - **Default:** `Threshold`  
    -   [Operator](#Operator) - Optional - **Type:** string - **Default:** `GreaterThanOrEqualToThreshold`  
    -   [Time](#Time) - Optional - **Type:** number - **Default:** `300`  
    -   [Periods](#Periods) - Optional - **Type:** number - **Default:** `1`  
    -   [Statistic](#Statistic) - Optional - **Type:** string - **Default:** `Sum`  
    -   [ReportOk](#ReportOk) - Optional - **Type:** boolean - **Default:** `false`  
    -   [MissingData](#MissingData) - Optional - **Type:** string - **Default:** `notBreaching`  

```

</TabItem>
</Tabs>

# user

A user with permissions on components deployed in the solution

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - application


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"user" : {
		"Fragment" : "<string>",
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"GenerateCredentials" : {
			"Formats" : [
				"system"
			],
			"EncryptionScheme" : "<string>",
			"CharacterLength" : 20
		},
		"Permissions" : {
			"Decrypt" : true,
			"AsFile" : true,
			"AppData" : true,
			"AppPublic" : true
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Fragment](#Fragment) _(Container)_ - Optional - **Type:** string  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [GenerateCredentials](#GenerateCredentials)
    -   [Formats](#Formats) - Optional - **Type:** array of string - **Default:** `system`  
           **Possible Values:** `[system, console]`
    -   [EncryptionScheme](#EncryptionScheme) - Optional - **Type:** string  
           **Possible Values:** `[base64]`
    -   [CharacterLength](#CharacterLength) - Optional - **Type:** number - **Default:** `20`  
-   [Permissions](#Permissions)
    -   [Decrypt](#Decrypt) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AsFile](#AsFile) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppData](#AppData) - Optional - **Type:** boolean - **Default:** `true`  
    -   [AppPublic](#AppPublic) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# userpool

Managed identity service

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution

**Notes**

!!! warning
    Make sure to plan your schema before initial deployment. Updating shema attributes causes a replaccement of the userpool
!!! warning
    Please read <https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools-add-custom-domain.html> before enabling custom domains on userpool hosted UI. An A Record is required in your base domain

**Sub Components**

-   [userpoolclient](#userpoolclient)
    -   **Component Attribute** - Clients
    -   **Link Attribute** - Client
-   [userpoolauthprovider](#userpoolauthprovider)
    -   **Component Attribute** - AuthProviders
    -   **Link Attribute** - AuthProvider


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"userpool" : {
		"MFA" : false,
		"AdminCreatesUser" : true,
		"UnusedAccountTimeout" : 7,
		"VerifyEmail" : true,
		"VerifyPhone" : false,
		"LoginAliases" : [
			"email"
		],
		"AllowUnauthenticatedIds" : false,
		"AuthorizationHeader" : "Authorization",
		"PasswordPolicy" : {
			"MinimumLength" : 10,
			"Lowercase" : true,
			"Uppercase" : true,
			"Numbers" : true,
			"SpecialCharacters" : true
		},
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		},
		"Profiles" : {
			"Deployment" : "<array of string>"
		},
		"DefaultClient" : true,
		"Schema" : {
			"example" : {
				"DataType" : "String",
				"Mutable" : true,
				"Required" : true
			}
		},
		"HostedUI" : {
			"Certificate" : {
				"Qualifiers" : "<object>",
				"Domain" : "<string>",
				"IncludeInDomain" : {
					"Product" : "<boolean>",
					"Environment" : "<boolean>",
					"Segment" : "<boolean>"
				},
				"Host" : "<string>",
				"HostParts" : "<array of string>",
				"IncludeInHost" : {
					"Product" : "<boolean>",
					"Environment" : "<boolean>",
					"Segment" : "<boolean>",
					"Tier" : "<boolean>",
					"Component" : "<boolean>",
					"Instance" : "<boolean>",
					"Version" : "<boolean>",
					"Host" : "<boolean>"
				},
				"External" : "<boolean>",
				"Wildcard" : "<boolean>"
			}
		},
		"Clients" : {
			"example" : "< instance of userpoolclient>"
		},
		"AuthProviders" : {
			"example" : "< instance of userpoolauthprovider>"
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [MFA](#MFA) - Optional - **Type:** boolean - **Default:** `false`  
-   [AdminCreatesUser](#AdminCreatesUser) - Optional - **Type:** boolean - **Default:** `true`  
-   [UnusedAccountTimeout](#UnusedAccountTimeout) - Optional - **Type:** number - **Default:** `7`  
-   [VerifyEmail](#VerifyEmail) - Optional - **Type:** boolean - **Default:** `true`  
-   [VerifyPhone](#VerifyPhone) - Optional - **Type:** boolean - **Default:** `false`  
-   [LoginAliases](#LoginAliases) - Optional - **Type:** array of string - **Default:** `email`  
-   [AllowUnauthenticatedIds](#AllowUnauthenticatedIds) - Optional - **Type:** boolean - **Default:** `false`  
-   [AuthorizationHeader](#AuthorizationHeader) - Optional - **Type:** string - **Default:** `Authorization`  
-   [PasswordPolicy](#PasswordPolicy)
    -   [MinimumLength](#MinimumLength) - Optional - **Type:** number - **Default:** `10`  
    -   [Lowercase](#Lowercase) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Uppercase](#Uppercase) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Numbers](#Numbers) - Optional - **Type:** boolean - **Default:** `true`  
    -   [SpecialCharacters](#SpecialCharacters) - Optional - **Type:** boolean - **Default:** `true`  
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  
-   [Profiles](#Profiles)
    -   [Deployment](#Deployment) - Optional - **Type:** array of string  
-   [DefaultClient](#DefaultClient) - Optional - **Type:** boolean - **Default:** `true`  
    **Description:** Enable default client mode which creates app client for the user pool and aligns with legacy config
-   [Schema](#Schema)
    -   [DataType](#DataType) - Optional - **Type:** string - **Default:** `String`  
           **Possible Values:** `[String, Number, DateTime, Boolean]`
    -   [Mutable](#Mutable) - Optional - **Type:** boolean - **Default:** `true`  
    -   [Required](#Required) - Optional - **Type:** boolean - **Default:** `true`  
-   [HostedUI](#HostedUI)
    -   [Certificate](#Certificate)
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [Domain](#Domain) - Optional - **Type:** string  
    -   [IncludeInDomain](#IncludeInDomain)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** string  
    -   [HostParts](#HostParts) - Optional - **Type:** array of string  
    -   [IncludeInHost](#IncludeInHost)
    -   [Product](#Product) - Optional - **Type:** boolean  
    -   [Environment](#Environment) - Optional - **Type:** boolean  
    -   [Segment](#Segment) - Optional - **Type:** boolean  
    -   [Tier](#Tier) - Optional - **Type:** boolean  
    -   [Component](#Component) - Optional - **Type:** boolean  
    -   [Instance](#Instance) - Optional - **Type:** boolean  
    -   [Version](#Version) - Optional - **Type:** boolean  
    -   [Host](#Host) - Optional - **Type:** boolean  
    -   [Qualifiers](#Qualifiers) - Optional - **Type:** object  
    -   [External](#External) - Optional - **Type:** boolean  
    -   [Wildcard](#Wildcard) - Optional - **Type:** boolean  

```

</TabItem>
</Tabs>

# userpoolclient

A oauth app client which belongs to the userpool

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"userpoolclient" : {
		"OAuth" : {
			"Scopes" : [
				"email",
				"openid"
			],
			"Flows" : [
				"code"
			]
		},
		"ClientGenerateSecret" : false,
		"ClientTokenValidity" : 30,
		"IdentityPoolAccess" : true,
		"AuthProviders" : [
			"COGNITO"
		],
		"Links" : {
			"example" : {
				"Any" : "<string>",
				"Tenant" : "<string>",
				"Product" : "<string>",
				"Environment" : "<string>",
				"Segment" : "<string>",
				"Tier" : "<string>",
				"Component" : "<string>",
				"Function" : "<string>",
				"Service" : "<string>",
				"Task" : "<string>",
				"PortMapping" : "<string>",
				"Mount" : "<string>",
				"Platform" : "<string>",
				"RouteTable" : "<string>",
				"NetworkACL" : "<string>",
				"DataBucket" : "<string>",
				"Key" : "<string>",
				"Branch" : "<string>",
				"Client" : "<string>",
				"AuthProvider" : "<string>",
				"DataFeed" : "<string>",
				"RegistryService" : "<string>",
				"Instance" : "<string>",
				"Version" : "<string>",
				"Role" : "<string>",
				"Direction" : "<string>",
				"Type" : "<string>",
				"Enabled" : true
			}
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [OAuth](#OAuth)
    -   [Scopes](#Scopes) - Optional - **Type:** array of string - **Default:** `email, openid`  
           **Possible Values:** `[phone, email, openid, aws.cognito.signin.user.admin, profile]`
    -   [Flows](#Flows) - Optional - **Type:** array of string - **Default:** `code`  
           **Possible Values:** `[code, implicit, client_credentials]`
-   [ClientGenerateSecret](#ClientGenerateSecret) - Optional - **Type:** boolean - **Default:** `false`  
    **Description:** Generate a client secret which musht be provided in auth calls
-   [ClientTokenValidity](#ClientTokenValidity) - Optional - **Type:** number - **Default:** `30`  
    **Description:** Time in days that the refresh token is valid for
-   [IdentityPoolAccess](#IdentityPoolAccess) - Optional - **Type:** boolean - **Default:** `true`  
    **Description:** Enable the use of the identity pool for this client
-   [AuthProviders](#AuthProviders) - Optional - **Type:** array of string - **Default:** `COGNITO`  
    **Description:** A list of user pool auth providers which can use this client
-   [Links](#Links)
    -   [Any](#Any) - Optional - **Type:** string  
    -   [Tenant](#Tenant) - Optional - **Type:** string  
    -   [Product](#Product) - Optional - **Type:** string  
    -   [Environment](#Environment) - Optional - **Type:** string  
    -   [Segment](#Segment) - Optional - **Type:** string  
    -   [Tier](#Tier) - Required - **Type:** string  
    -   [Component](#Component) - Required - **Type:** string  
    -   [Function](#Function) - Optional - **Type:** string  
    -   [Service](#Service) - Optional - **Type:** string  
    -   [Task](#Task) - Optional - **Type:** string  
    -   [PortMapping](#PortMapping) _(Port)_ - Optional - **Type:** string  
    -   [Mount](#Mount) - Optional - **Type:** string  
    -   [Platform](#Platform) - Optional - **Type:** string  
    -   [RouteTable](#RouteTable) - Optional - **Type:** string  
    -   [NetworkACL](#NetworkACL) - Optional - **Type:** string  
    -   [DataBucket](#DataBucket) - Optional - **Type:** string  
    -   [Key](#Key) - Optional - **Type:** string  
    -   [Branch](#Branch) - Optional - **Type:** string  
    -   [Client](#Client) - Optional - **Type:** string  
    -   [AuthProvider](#AuthProvider) - Optional - **Type:** string  
    -   [DataFeed](#DataFeed) - Optional - **Type:** string  
    -   [RegistryService](#RegistryService) - Optional - **Type:** string  
    -   [Instance](#Instance) - Optional - **Type:** string  
    -   [Version](#Version) - Optional - **Type:** string  
    -   [Role](#Role) - Optional - **Type:** string  
    -   [Direction](#Direction) - Optional - **Type:** string  
    -   [Type](#Type) - Optional - **Type:** string  
    -   [Enabled](#Enabled) - Optional - **Type:** boolean - **Default:** `true`  

```

</TabItem>
</Tabs>

# userpoolauthprovider

An external auth provider which will federate with the user pool

**Deployment Properties**

-   **Available Providers** - aws
-   **Component Level** - solution


<Tabs
    defaultValue="schema"
    values={[
        {label: 'Schema', value: 'schema'},
        {label: 'Attribute Reference', value: 'attributes'},
    ]
}>
<TabItem value='schema'>

```json
{
	"userpoolauthprovider" : {
		"Engine" : "<string>",
		"AttributeMappings" : {
			"example" : {
				"UserPoolAttribute" : "<string>",
				"ProviderAttribute" : "<string>"
			}
		},
		"IDPIdentifiers" : "<array of string>",
		"SAML" : {
			"MetadataUrl" : "<string>",
			"EnableIDPSignOut" : true
		}
	}
}
```

</TabItem>
<TabItem value='attributes'>

```text

-   [Engine](#Engine) - Required - **Type:** string  
    **Description:** The authentication provider type  **Possible Values:** `[SAML, OIDC]`
-   [AttributeMappings](#AttributeMappings)
    -   [UserPoolAttribute](#UserPoolAttribute) - Optional - **Type:** string  
           **Description:** The name of the attribute in the user pool schema - the id of the mapping will be used if not provided
    -   [ProviderAttribute](#ProviderAttribute) - Required - **Type:** string  
           **Description:** The provider attribute which will be mapped
-   [IDPIdentifiers](#IDPIdentifiers) - Optional - **Type:** array of string  
    **Description:** A list of identifiers that can be used to automatically pick the IDP - E.g. email domain
-   [SAML](#SAML)
    -   [MetadataUrl](#MetadataUrl) - Optional - **Type:** string  
           **Description:** The SAML metadataUrl endpoint
    -   [EnableIDPSignOut](#EnableIDPSignOut) - Optional - **Type:** boolean - **Default:** `true`  
           **Description:** Enable the IDP Signout Flow

```

</TabItem>
</Tabs>
