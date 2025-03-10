![CrowdStrike Falcon](https://raw.githubusercontent.com/CrowdStrike/falconpy/main/docs/asset/cs-logo.png) 

[![Twitter URL](https://img.shields.io/twitter/url?label=Follow%20%40CrowdStrike&style=social&url=https%3A%2F%2Ftwitter.com%2FCrowdStrike)](https://twitter.com/CrowdStrike)

# FalconPy Sample Library

These examples are provided as a quick start for your project.

+ [Authentication for Examples](#authentication-for-these-examples)
+ [Samples by API service collection](#samples-by-api-service-collection)
+ [Suggestions](#suggestions)

![Adversary Bust Museum](https://raw.githubusercontent.com/CrowdStrike/falconpy/main/docs/asset/origins-mural.png)

# Authentication for these Examples
In order to expedite sample delivery, examples will follow one of three standard patterns for defining and providing credentials for API access. 

| Pattern | Usage detail |
| :--- | :--- |
| Environment variables | Credentials are retrieved from the local environment of the machine the example is executed on.<BR/><BR/>These values are named:<ul><li>`FALCON_CLIENT_ID`</li><li>`FALCON_CLIENT_SECRET`</li></ul> |
| Runtime (Command line arguments) | Credentials are consumed at runtime via command line parameters. Typically this handled via the [`argparse`](https://docs.python.org/3/library/argparse.html) module. |
| Standardized "credential" file | This file is named `config.json`, and is in JSON format. This file is __not encrypted__ and may not be suitable for production deployments. A sample of this file, [`config_sample.json`](config_sample.json) is provided within this folder. Rename this file to `config.json`, and then update it's contents to reflect your current development API credentials.  |

> Please note: These are not the only methods for providing these values. 

# Samples by API service collection
The following samples are categorized by CrowdStrike Falcon API service collection. Some samples have specific FalconPy version requirements, check documentation maintained within the source or the sample `README.md` for more details.

![Total samples](https://img.shields.io/endpoint?url=https%3A%2F%2Ffalconpy.io%2F_samples.json&style=for-the-badge)

| Service Collection | Samples |
| :--- | :--- |
| [Detects](#detects) | [Detects Advisor](#detects-advisor) |
| [Event Streams](#event-streams) | [Send detections to AWS Security Hub](#send-detections-to-aws-security-hub) |
| [Falcon Discover](#falcon-discover) | [List discovered hosts](#list-discovered-hosts) |
| [Falcon Discover for Cloud and Containers](#falcon-discover-for-cloud-and-containers-aws-accounts) | [Manage Discover accounts (AWS)](#manage-discover-accounts) |
| [Falcon Horizon](#falcon-horizon) | [Get CSPM policies](#get-cspm-policies) |
| [Falcon Flight Control](#falcon-flight-control) | [Find child CID](#find-child-cid) |
| [Falcon X](#falcon-x) | [Manage sandbox uploads](#manage-sandbox-uploads)<BR/>[Falcon X single scan](#falcon-x-single-scan)<BR/>[Get all artifacts](#get-all-artifacts)<BR/>[Quick Scan a target](#quick-scan-a-target)<BR/>[S3 Bucket Protection](#s3-bucket-protection) |
| [Firewall Management](#firewall-management) | [Export Firewall events to a file](#export-firewall-events-to-a-file) |
| [Hosts](#hosts) | [List sensors by hostname](#list-sensors-by-hostname)<BR/>[CUSSED (Manage stale sensors)](#cussed-manage-stale-sensors)<BR/>[Offset vs. Token](#offset-vs-token)<BR/>[Quarantine a host](#quarantine-a-host)<BR/>[Quarantine a host (updated version)](#quarantine-a-host-updated-version) |
| [Incidents](#incidents) | [CrowdScore QuickChart](#crowdscore-quickchart)<BR/>[Incident Triage](#incident-triage) |
| [Intel](#intel) | [MISP Import](#misp-import) |
| [IOC](#ioc) | [Create indicators](#create-indicators) |
| [MalQuery](#malquery) | [Malqueryinator](#malqueryinator) |
| [Prevention Policy](#prevention-policy) | [Prevention Policy Hawk](#prevention-policy-hawk) |
| [Real Time Response](#real-time-response) | [Bulk execute a command](#bulk-execute-a-command)<BR/>[Bulk execute a command (queued)](#bulk-execute-a-command-queued)<BR/>[Dump memory for a running process](#dump-memory-for-a-running-process)<BR/>[My Little RTR](#my-little-rtr) |
| [Sensor Download](#sensor-download) | [Download the CrowdStrike sensor](#download-the-crowdstrike-sensor) |
| [Sensor Update Policies](#sensor-update-policies) | [Policy Wonk](#policy-wonk) |
| [Spotlight](#spotlight) | [Find vulnerable hosts by CVE ID](#find-vulnerable-hosts-by-cve-id)<BR/>[CISA DHS Known Exploited Vulnerabilities](#cisa-dhs-known-exploited-vulnerabilities) |
| [User Management](#user-management) | [Bulk user administration](#bulk-user-administration) |


##### Class type legend
Provided examples are further categorized by the type of class used to interact with the CrowdStrike API.

| Indicator | Detail |
| :--- | :--- |
| [![Service Class](https://img.shields.io/badge/-Service%20Class-red?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](https://www.falconpy.io/Usage/Basic-Service-Class-usage.html) | These samples leverage Service Classes to perform the example task. |
| [![Uber Class](https://img.shields.io/badge/-Uber%20Class-maroon?style=for-the-badge&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](https://www.falconpy.io/Usage/Basic-Uber-Class-usage.html) | These samples make use of the Uber Class to perform the example task. |
| [![MSSP Usage supported](https://img.shields.io/badge/-Supports%20MSSP-darkblue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==&style=for-the-badge)](https://falconpy.io/Usage/Authenticating-to-the-API.html#mssp-examples-hosts) | These samples support MSSP usage scenarios.


## Detects
The CrowdStrike Detects API service collection is the sole focus of this category.

### Detects Advisor
[Detects Advisor](detects#detects-advisor) is an example application for triaging inbound detections in your CrowdStrike Falcon tenant.

[![Detects](https://img.shields.io/badge/Service%20Class-Detects%20Advisor-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](detects#detects-advisor)

#### Detects API operations discussed
This sample demonstrate the following CrowdStrike Detects API operations:

| Operation | Description |
| :--- | :--- |
| [GetDetectSummaries](https://falconpy.io/Service-Collections/Detects.html#getdetectsummaries) | View information about detections. |
| [QueryDetects](https://falconpy.io/Service-Collections/Detects.html#querydetects) | Search for detection IDs that match a given query. |
| [UpdateDetectsByIdsV2](https://falconpy.io/Service-Collections/Detects.html#updatedetectsbyidsv2) | Modify the state, assignee, and visibility of detections. |



## Event Streams
This category is focused on the CrowdStrike Event Streams API service collection.

### Send detections to AWS Security Hub
This [example](https://github.com/CrowdStrike/Cloud-AWS/tree/main/Security-Hub) demonstrates publishing AWS Security Hub findings from CrowdStrike Falcon Event Streams API.

[![Event Streams](https://img.shields.io/badge/Uber%20Class-Send%20Detections%20to%20AWS%20Security%20Hub-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](https://github.com/CrowdStrike/Cloud-AWS/tree/main/Security-Hub)

#### Event Streams API operations discussed
This sample demonstrate the following CrowdStrike Event Streams API operations:

| Operation | Description |
| :--- | :--- |
| [listAvailableStreamsOAuth2](https://falconpy.io/Service-Collections/Event-Streams.html#listavailablestreamsoauth2) | Discover all event streams in your environment. |
| [refreshActiveStreamSession](https://falconpy.io/Service-Collections/Event-Streams.html#refreshactivestreamsession) | Refresh an active event stream. Use the URL shown in a [listAvailableStreamsOAuth2](https://falconpy.io/Service-Collections/Event-Streams.html#listavailablestreamsoauth2) response. |

## Falcon Discover
The samples in this section focus on the CrowdStrike Falcon Discover API service collection.

### List discovered hosts

In this [example](discover/list_discovered_hosts.py), we demonstrate listing up to the first 100 hosts identified by Falcon Discover.

[![Falcon Discover](https://img.shields.io/badge/Service%20Class-List%20Discovered%20Hosts-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](discover/list_discovered_hosts.py) 

#### Cloud Connect AWS API operations discussed
This sample demonstrate the following CrowdStrike Discover API operations:

| Operation | Description |
| :--- | :--- |
| [get_hosts](https://falconpy.io/Service-Collections/Discover.html#get_hosts) | Get details on assets by providing one or more IDs. |
| [query_hosts](https://falconpy.io/Service-Collections/Discover.html#query_hosts) | Search for assets in your environment by providing a FQL (Falcon Query Language) filter and paging details. Returns a set of asset IDs which match the filter criteria. |


## Falcon Discover for Cloud and Containers (AWS Accounts)
This section discusses Falcon Discover for Cloud and Containers, and the two API service collections, Cloud Connect AWS and D4C Registration.

### Manage Discover accounts
This example demonstrates using FalconPy to register and remove accounts managed by CrowdStrike Falcon Discover for Cloud (AWS). Both [Service Class](discover_aws/manage_discover_accounts_service.py) and [Uber Class](discover_aws/manage_discover_accounts_uber.py) examples are provided.

[![Falcon Discover for Cloud (AWS)](https://img.shields.io/badge/Service%20Class-Manage%20Discover%20Accounts-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](discover_aws/manage_discover_accounts_service.py) 
[![Falcon Discover for Cloud (AWS)](https://img.shields.io/badge/Uber%20Class-Manage%20Discover%20Accounts-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](discover_aws/manage_discover_accounts_uber.py)

#### Cloud Connect AWS API operations discussed
These samples demonstrate the following CrowdStrike Cloud Connect AWS (Discover for Cloud and Containers) API operations:

| Operation | Description |
| :--- | :--- |
| [DeleteAWSAccounts](https://falconpy.io/Service-Collections/Cloud-Connect-AWS.html#deleteawsaccounts) | Delete a set of AWS Accounts by specifying their IDs. |
| [ProvisionAWSAccounts](https://falconpy.io/Service-Collections/Cloud-Connect-AWS.html#provisionawsaccounts) | Provision AWS Accounts by specifying details about the accounts to provision. |
| [QueryAWSAccounts](https://falconpy.io/Service-Collections/Cloud-Connect-AWS.html#queryawsaccounts) | Search for provisioned AWS Accounts by providing a FQL filter and paging details. Returns a set of AWS accounts which match the filter criteria. |
| [UpdateAWSAccounts](https://falconpy.io/Service-Collections/Cloud-Connect-AWS.html#updateawsaccounts) | Update AWS Accounts by specifying the ID of the account and details to update. |
| [VerifyAWSAccountAccess](https://falconpy.io/Service-Collections/Cloud-Connect-AWS.html#verifyawsaccountaccess) | Search for provisioned AWS Accounts by providing a FQL filter and paging details. Returns a set of AWS account IDs which match the filter criteria. |

## Falcon Horizon
These samples focus on CrowdStrike Falcon Horizon and the available API operations within the CSPM Registration service collection.

### Get CSPM policies
Submitted by `@mccbryan3`, this [example](cspm_registration/get_cspm_policies.py) uses FalconPy to report or export as CSV, all or selective Falcon Horizon CSPM Policies.

[![Falcon Horizon](https://img.shields.io/badge/Service%20Class-Report%20Horizon%20Policies-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](cspm_registration/get_cspm_policies.py) 

#### CSPM Registration API operations discussed
This sample demonstrate the following CrowdStrike CSPM Registration (Horizon) API operations:

| Operation | Description |
| :--- | :--- |
| [GetCSPMPolicySettings](https://falconpy.io/Service-Collections/CSPM-Registration.html#getcspmpolicysettings) | Returns information about current policy settings. |


## Falcon Flight Control
The samples in this category demonstrate functionality for MSSP scenarios using the Falcon Flight Control API service collection.

### Find child CID
This [example](flight_control/find_child_cid.py) demonstrates retrieving a child CID using the CrowdStrike Falcon Flight Control API.

[![Falcon Flight Control](https://img.shields.io/badge/Service%20Class-Find%20Child%20CID-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](flight_control/find_child_cid.py) [![MSSP Use supported](https://img.shields.io/badge/-Supports%20MSSP-darkblue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==&style=for-the-badge)](flight_control/find_child_cid.py)

#### Flight Control API operations discussed
This sample demonstrate the following CrowdStrike Flight Control API operations:

| Operation | Description |
| :--- | :--- |
| [QueryChildren](https://falconpy.io/Service-Collections/MSSP.html#querychildren) | Query for customers linked as children. |

## Falcon X
This category is dedicated to Falcon X, and discusses the Falcon X Sandbox, Quick Scan, and Sample Uploads API service collections.

- [Manage sandbox uploads](#manage-sandbox-uploads)
- [Falcon X single scan](#falcon-x-single-scan)
- [Get all artifacts](#get-all-artifacts)
- [Quick Scan a target](#quick-scan-a-target)
- [S3 Bucket Protection](#s3-bucket-protection)

### Manage sandbox uploads
These samples use the CrowdStrike Sample Uploads API to upload, retrieve and delete files from Falcon X Sandbox. An example for using the [Service Class](sample_uploads/sample_uploads_service.py) and the [Uber Class](sample_uploads/sample_uploads_uber.py) are provided.

[![Sample Uploads](https://img.shields.io/badge/Service%20Class-Handle%20Sandbox%20Files-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](sample_uploads/sample_uploads_service.py) 
[![Sample Uploads](https://img.shields.io/badge/Uber%20Class-Handle%20Sandbox%20Files-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](sample_uploads/sample_uploads_uber.py)

#### Sample Uploads API operations discussed
These samples demonstrate the following CrowdStrike Sample Uploads API operations:

| Operation | Description |
| :--- | :--- |
| [GetSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#getsamplev3) | Retrieves the file associated with the given ID (SHA256). |
| [UploadSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#uploadsamplev3) | Upload a file for further cloud analysis. After uploading, call the specific analysis API endpoint. |
| [DeleteSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#deletesamplev3) | Removes a sample, including file, meta and submissions from the collection. |

---

### Falcon X single scan

Analyze a single file for malware using the Falcon X Sandbox API with these [examples](falconx_sandbox/single_scan). A sample using the [Service Class](https://github.com/CrowdStrike/falconpy/blob/samples/samples/falconx_sandbox/single_scan/falconx_scan_example.py) and one using the [Uber Class](https://github.com/CrowdStrike/falconpy/blob/samples/samples/falconx_sandbox/single_scan/falconx_scan_example_uber.py) are provided.

[![Falcon X Sandbox](https://img.shields.io/badge/Service%20Class-Analyze%20a%20Single%20file-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](falconx_sandbox/single_scan) 
[![Falcon X Sandbox](https://img.shields.io/badge/Uber%20Class-Analyze%20a%20Single%20File-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](falconx_sandbox/single_scan)

#### Falcon X Sandbox API operations discussed
These samples demonstrates the following CrowdStrike Falcon X Sandbox API operations:

| Operation | Description |
| :--- | :--- |
| [DeleteSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#deletesamplev3) | Removes a sample, including file, meta and submissions from the collection. |
| [GetReports](https://falconpy.io/Service-Collections/Falconx-Sandbox.html#getreports) | Get a full sandbox report. |
| [GetSubmissions](https://falconpy.io/Service-Collections/Falconx-Sandbox.html#getsubmissions) | Check the status of a sandbox analysis. Time required for analysis varies but is usually less than 15 minutes. |
| [UploadSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#uploadsamplev3) | Upload a file for further cloud analysis. After uploading, call the specific analysis API endpoint. |
| [Submit](https://falconpy.io/Service-Collections/Falconx-Sandbox.html#submit) | Submit an uploaded file or a URL for sandbox analysis. Time required for analysis varies but is usually less than 15 minutes. |


---

### Get all artifacts

This [example](falconx_sandbox/get_all_artifacts.py) demonstrates retrieving all artifacts for all reports (in all supported formats).

[![Falcon X Sandbox](https://img.shields.io/badge/Service%20Class-Get%20All%20Artifacts-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](falconx_sandbox/get_all_artifacts.py) 

#### Falcon X Sandbox API operations discussed
This sample demonstrates the following CrowdStrike Falcon X Sandbox API operations:

| Operation | Description |
| :--- | :--- |
| [GetArtifacts](https://falconpy.io/Service-Collections/Falconx-Sandbox.html#getartifacts) | Download IOC packs, PCAP files, and other analysis artifacts. |
| [GetReports](https://falconpy.io/Service-Collections/Falconx-Sandbox.html#getreports) | Get a full sandbox report. |
| [QueryReports](https://falconpy.io/Service-Collections/Falconx-Sandbox.html#queryreports) | Find sandbox reports by providing a FQL filter and paging details. Returns a set of report IDs that match your criteria. |

---

### Quick Scan a target

This [demonstration](quick_scan/scan_target.py) leverages the Falcon Quick Scan and Sample Uploads APIs to scan the contents of a target folder. (Either on the local filesystem or a bucket in S3.)

[![Quick Scan / Sample Uploads](https://img.shields.io/badge/Service%20Class-Scan%20a%20target-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](quick_scan/scan_target.py)

#### Quick Scan and Sample Uploads API operations discussed
This sample demonstrates the following CrowdStrike Quick Scan and Sample Uploads API operations:

| Operation | Description |
| :--- | :--- |
| [DeleteSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#deletesamplev3) | Removes a sample, including file, meta and submissions from the collection. |
| [GetScans](https://falconpy.io/Service-Collections/Quick-Scan.html#getscans) | Check the status of a volume scan. Time required for analysis increases with the number of samples in a volume but usually it should take less than 1 minute. |
| [ScanSamples](https://falconpy.io/Service-Collections/Quick-Scan.html#scansamples) | Submit a volume of files for ml scanning. Time required for analysis increases with the number of samples in a volume but usually it should take less than 1 minute. |
| [UploadSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#uploadsamplev3) | Upload a file for further cloud analysis. After uploading, call the specific analysis API endpoint. |

---

### S3 Bucket Protection

Building on the previous example, this [solution](https://github.com/CrowdStrike/Cloud-AWS/tree/main/s3-bucket-protection) demonstrates a complete integration with AWS Lambda, AWS S3 and AWS Security Hub that scans files as they are uploaded to the bucket. Files that are found to be malicious are removed from the bucket and a finding is published to AWS Security Hub.

[![Quick Scan / Sample Uploads](https://img.shields.io/badge/Service%20Class-S3%20Bucket%20Protection-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](https://github.com/CrowdStrike/Cloud-AWS/tree/main/s3-bucket-protection)

#### Quick Scan and Sample Uploads API operations discussed
This sample demonstrates the following CrowdStrike Quick Scan and Sample Uploads API operations:

| Operation | Description |
| :--- | :--- |
| [DeleteSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#deletesamplev3) | Removes a sample, including file, meta and submissions from the collection. |
| [GetScans](https://falconpy.io/Service-Collections/Quick-Scan.html#getscans) | Check the status of a volume scan. Time required for analysis increases with the number of samples in a volume but usually it should take less than 1 minute. |
| [ScanSamples](https://falconpy.io/Service-Collections/Quick-Scan.html#scansamples) | Submit a volume of files for ml scanning. Time required for analysis increases with the number of samples in a volume but usually it should take less than 1 minute. |
| [UploadSampleV3](https://falconpy.io/Service-Collections/Sample-Uploads.html#uploadsamplev3) | Upload a file for further cloud analysis. After uploading, call the specific analysis API endpoint. |

## Firewall Management
The CrowdStrike Falcon Firewall Management and Firewall Policies APIs are the focus of this section.

### Export Firewall events to a file
Developed by `@wozboz`, this [example](firewall_management/get_firewall_events.py) demonstrates exporting Firewall events using the Firewall Management Service Class. This sample also provides an example of _tokenized pagination_ leveraging the `after` return parameter found in the `meta` branch.  More details regarding this style of pagination can be found [here](https://falconpy.io/Usage/Response-Handling.html#paginating-json-responses).

[![Firewall Management](https://img.shields.io/badge/Service%20Class-Export_Firewall_Events-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](firewall_management/get_firewall_events.py)

#### Firewall Management operations discussed
This sample demonstrate the following CrowdStrike Firewall Management API operations:

| Operation | Description |
| :--- | :--- |
| [get_events](https://falconpy.io/Service-Collections/Firewall-Management.html#get_events) | Get events entities by ID and optionally version. |
| [query_events](https://falconpy.io/Service-Collections/Firewall-Management.html#query_events) | Find all event IDs matching the query with filter. |


## Hosts
The samples collected in this section demonstrate leveraging CrowdStrike's Hosts and Host Group API service collections to secure your endpoints.

- [List sensors by hostname](#list-sensors-by-hostname)
- [CUSSED (Stale sensor detector)](#cussed-manage-stale-sensors)
- [Offset vs. Token](#offset-vs-token)
- [Quarantine a host](#quarantine-a-host)
- [Quarantine a host (updated)](#quarantine-a-host-updated-version)

### List sensors by hostname
This [example](hosts#list-sensors-by-hostname) will demonstrate how to retrieve a list of sensors by hostname.

[![Hosts](https://img.shields.io/badge/Service%20Class-List%20Sensors%20By%20Hostname-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](hosts#list-sensors-by-hostname) [![MSSP Use supported](https://img.shields.io/badge/-Supports%20MSSP-darkblue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==&style=for-the-badge)](hosts#list-sensors-by-hostname)

#### Hosts API operations discussed
This sample demonstrates the following CrowdStrike Hosts API operations:

| Operation | Description |
| :--- | :--- |
| [GetDeviceDetails](https://falconpy.io/Service-Collections/Hosts.html#getdevicedetails) | Get details on one or more hosts by providing agent IDs (AID). You can get a host's agent IDs (AIDs) from the /devices/queries/devices/v1 endpoint, the Falcon console or the Streaming API. |
| [QueryDevicesByFilter](https://falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilter) | Search for hosts in your environment by platform, hostname, IP, and other criteria. |

---

### CUSSED (Manage stale sensors)
Identify and optionally remove stale sensors using this [example](hosts#list-stale-sensors).

[![Hosts](https://img.shields.io/badge/Service%20Class-Find%20Stale%20Sensors-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](hosts#list-stale-sensors) [![MSSP Use supported](https://img.shields.io/badge/-Supports%20MSSP-darkblue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==&style=for-the-badge)](hosts#list-stale-sensors)

#### Hosts API operations discussed
This sample demonstrates the following CrowdStrike Hosts API operations:

| Operation | Description |
| :--- | :--- |
| [GetDeviceDetails](https://falconpy.io/Service-Collections/Hosts.html#getdevicedetails) | Get details on one or more hosts by providing agent IDs (AID). You can get a host's agent IDs (AIDs) from the /devices/queries/devices/v1 endpoint, the Falcon console or the Streaming API. |
| [PerformActionV2](https://falconpy.io/Service-Collections/Hosts.html#performactionv2) | Take various actions on the hosts in your environment. Contain or lift containment on a host. Delete or restore a host. |
| [QueryDevicesByFilterScroll](https://falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilterscroll) | Search for hosts in your environment by platform, hostname, IP, and other criteria with continuous pagination capability (based on offset pointer which expires after 2 minutes with no maximum limit). |

---

### Offset vs. Token
This [demonstration](hosts#comparing-querydevicesbyfilter-and-querydevicesbyfilterscroll-offset-vs-token) discusses the [pagination](https://falconpy.io/Usage/Response-Handling.html#paginating-json-responses) differences when using [`QueryDevicesByFilter`](https://www.falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilter) versus [`QueryDevicesByFilterScroll`](https://www.falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilterscroll).

[![Hosts](https://img.shields.io/badge/Service%20Class-Offset%20vs.%20Token-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](hosts#comparing-querydevicesbyfilter-and-querydevicesbyfilterscroll-offset-vs-token) 

#### Hosts API operations discussed
This sample demonstrates the following CrowdStrike Hosts API operations:

| Operation | Description |
| :--- | :--- |
| [QueryDevicesByFilter](https://falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilter) | Search for hosts in your environment by platform, hostname, IP, and other criteria. |
| [QueryDevicesByFilterScroll](https://falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilterscroll) | Search for hosts in your environment by platform, hostname, IP, and other criteria with continuous pagination capability (based on offset pointer which expires after 2 minutes with no maximum limit). |

---

### Quarantine a host
Developed by one of our maintainers `@soggysec`, this example demonstrates how to [quarantine target hosts](rtr/quarantine_hosts.py).

[![Hosts](https://img.shields.io/badge/Service%20Class-Quarantine%20Target%20Host-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](rtr/quarantine_hosts.py)

#### Hosts API operations discussed
This sample demonstrates the following CrowdStrike Hosts API operations:

| Operation | Description |
| :--- | :--- |
| [PerformActionV2](https://falconpy.io/Service-Collections/Hosts.html#performactionv2) | Take various actions on the hosts in your environment. Contain or lift containment on a host. Delete or restore a host. |
| [QueryDevicesByFilter](https://falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilter) | Search for hosts in your environment by platform, hostname, IP, and other criteria. |

---

### Quarantine a host (updated version)
This is the same solution, but [updated](hosts/quarantine_hosts_new.py) to demonstrate [Direct Authentication](https://www.falconpy.io/Usage/Authenticating-to-the-API.html#direct-authentication), [Body Payload Abstraction](https://www.falconpy.io/Usage/Payload-Handling.html#body-payload-abstraction) and [Parameter Abstraction](https://www.falconpy.io/Usage/Payload-Handling.html#parameter-abstraction).

[![Hosts](https://img.shields.io/badge/Service%20Class-Quarantine%20Target%20Host%20(Updated)-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](hosts/quarantine_hosts_new.py)

#### Hosts API operations discussed
This sample demonstrates the following CrowdStrike Hosts API operations:

| Operation | Description |
| :--- | :--- |
| [PerformActionV2](https://falconpy.io/Service-Collections/Hosts.html#performactionv2) | Take various actions on the hosts in your environment. Contain or lift containment on a host. Delete or restore a host. |
| [QueryDevicesByFilter](https://falconpy.io/Service-Collections/Hosts.html#querydevicesbyfilter) | Search for hosts in your environment by platform, hostname, IP, and other criteria. |

## Incidents
This category is dedicated to demonstrating the functionality provided by the CrowdStrike Incidents API service collection.

- [CrowdScore QuickChart](#crowdscore-quickchart)
- [Incidents Triage](#incident-triage)

### CrowdScore QuickChart
Quickly chart your past 24 hours of CrowdScore results with the [CrowdScore QuickChart](incidents#chart-your-crowdscore-for-the-past-day) sample.

[![Incidents](https://img.shields.io/badge/Service%20Class-CrowdScore_QuickChart-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](incidents#chart-your-crowdscore-for-the-past-day)

#### Incidents API operations discussed
This sample demonstrates the following CrowdStrike Incidents API operations:

| Operation | Description |
| :--- | :--- |
| [CrowdScore](https://falconpy.io/Service-Collections/Incidents.html#crowdscore) | Query environment wide CrowdScore and return the entity data. |

### Incident Triage
This example demonstrates triaging Incidents. You can assign / unassign responders, add / remove tags, and change name, description and status of an incident using the [Incident Triage](incidents#incident-triage) utility.

[![Incidents](https://img.shields.io/badge/Service%20Class-Incident_Triage-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](incidents#incident-triage)

#### Incidents API operations discussed
This sample demonstrates the following CrowdStrike Incidents API operations:

| Operation | Description |
| :--- | :--- |
| [PerformIncidentAction](https://falconpy.io/Service-Collections/Incidents.html#performincidentaction) | Perform a set of actions on one or more incidents, such as adding tags or comments or updating the incident name or description. |
| [GetIncidents](https://falconpy.io/Service-Collections/Incidents.html#getincidents) | Get details on incidents by providing incident IDs. |
| [QueryIncidents](https://falconpy.io/Service-Collections/Incidents.html#queryincidents) | Search for incidents by providing a FQL filter, sorting, and paging details. |

## Intel
This category provides samples that demonstrate the CrowdStrike Falcon Intel API service collection.

### MISP Import
This [utility](https://github.com/CrowdStrike/MISP-tools#manual-import) will import CrowdStrike Intel Threat indicators (Actors, Indicators and Reports) into your instance of [MISP](https://github.com/MISP/MISP).

[![Intel](https://img.shields.io/badge/Service%20Class-MISP_Import-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](https://github.com/CrowdStrike/MISP-tools#manual-import)

#### Intel API operations discussed
This sample demonstrates the following CrowdStrike Intel API operations:

| Operation | Description |
| :--- | :--- |
| [GetIntelActorEntities](https://falconpy.io/Service-Collections/Intel.html#getintelactorentities) | Retrieve specific actors using their actor IDs. |
| [GetIntelIndicatorEntities](https://falconpy.io/Service-Collections/Intel.html#getintelindicatorentities) | Retrieve specific indicators using their indicator IDs. |
| [GetIntelReportEntities](https://falconpy.io/Service-Collections/Intel.html#getintelreportentities) | Retrieve specific reports using their report IDs. |
| [QueryIntelActorEntities](https://falconpy.io/Service-Collections/Intel.html#queryintelactorentities) | Get info about actors that match provided FQL filters. |
| [QueryIntelIndicatorEntities](https://falconpy.io/Service-Collections/Intel.html#queryintelindicatorentities) | Get info about indicators that match provided FQL filters. |
| [QueryIntelReportEntities](https://falconpy.io/Service-Collections/Intel.html#queryintelreportentities) | Get info about reports that match provided FQL filters. |



## IOC
The samples in this section focus on the CrowdStrike IOC API service collection.

### Create indicators
Use this example to [create an Indicator of Compromise](ioc/create_ioc.py) (IOC). This example demonstrates the same operation using both the Service Class and the Uber Class. The Uber Class solution does not make use of [Body Payload Abstraction](https://falconpy.io/Usage/Payload-Handling.html#body-payload-abstraction).

[![IOC](https://img.shields.io/badge/Service%20Class-Create%20An%20IOC-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](ioc/create_ioc.py) 
[![IOC](https://img.shields.io/badge/Uber%20Class-Create%20An%20IOC-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](ioc/create_ioc.py)

#### IOC API operations discussed
This sample demonstrates the following CrowdStrike IOC API operations:

| Operation | Description |
| :--- | :--- |
| [indicator_create_v1](https://falconpy.io/Service-Collections/IOC.html#indicator_create_v1) | Create indicators. |


## MalQuery
This section is dedicated to the CrowdStrike MalQuery API service collection.

### Malqueryinator
Coded by our [**Purveyor of Lint**](https://xkcd.com/1513/) `@jlangdev`, [Malqueryinator](malquery#search-and-download-samples-from-malquery) demonstrates how to use the CrowdStrike MalQuery API to search and download malware samples.

[![MalQuery](https://img.shields.io/badge/Uber%20Class-Download%20Malware%20Samples%20with%20Malqueryinator-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](malquery#search-and-download-samples-from-malquery)

> This sample has been used in other integrations! You can check out the related integration [here](https://github.com/CrowdStrike/Cloud-AWS/blob/main/s3-bucket-protection/demo/instance.tf#L45).

#### MalQuery API operations discussed
This sample demonstrates the following CrowdStrike MalQuery API operations:

| Operation | Description |
| :--- | :--- |
| [GetMalQueryEntitiesSamplesFetchV1](https://falconpy.io/Service-Collections/MalQuery.html#getmalqueryentitiessamplesfetchv1) | Fetch a zip archive with password 'infected' containing the samples. Call this once the /entities/samples-multidownload request has finished processing. |
| [GetMalQueryRequestV1](https://falconpy.io/Service-Collections/MalQuery.html#getmalqueryrequestv1) | Check the status and results of an asynchronous request, such as hunt or exact-search. Supports a single request id at this time. |
| [PostMalQueryEntitiesSamplesMultidownloadV1](https://falconpy.io/Service-Collections/MalQuery.html#postmalqueryentitiessamplesmultidownloadv1) | Schedule samples for download. Use the result id with the /request endpoint to check if the download is ready after which you can call the /entities/samples-fetch to get the zip. |
| [PostMalQueryFuzzySearchV1](https://falconpy.io/Service-Collections/MalQuery.html#postmalqueryfuzzysearchv1) | Search Falcon MalQuery quickly, but with more potential for false positives. Search for a combination of hex patterns and strings in order to identify samples based upon file content at byte level granularity. |

## Prevention Policy
The samples in this section demonstrate using CrowdStrike's Prevention Policy API service collection.

### Prevention Policy Hawk
Manage your CrowdStrike prevention policy settings using the [Prevention Policy Hawk](prevention_policy#manage-prevention-policies-with-prevention-policy-hawk) sample.

[![Prevention Policy](https://img.shields.io/badge/Service%20Class-Prevention_Policy_Hawk-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](prevention_policy#manage-prevention-policies-with-prevention-policy-hawk)

#### Prevention Policy API operations discussed
This sample demonstrates the following CrowdStrike Prevention Policy API operations:

| Operation | Description |
| :--- | :--- |
| [deletePreventionPolicies](https://falconpy.io/Service-Collections/Prevention-Policy.html#deletepreventionpolicies) | Delete a set of Prevention Policies by specifying their IDs. |
| [performPreventionPoliciesAction](https://falconpy.io/Service-Collections/Prevention-Policy.html#performpreventionpoliciesaction) | Perform the specified action on the Prevention Policies specified in the request. |
| [queryCombinedPreventionPolicies](https://falconpy.io/Service-Collections/Prevention-Policy.html#querycombinedpreventionpolicies) | Search for Prevention Policies in your environment by providing a FQL filter and paging details. Returns a set of Prevention Policies which match the filter criteria. |
| [getPreventionPolicies](https://falconpy.io/Service-Collections/Prevention-Policy.html#getpreventionpolicies) | Retrieve a set of Prevention Policies by specifying their IDs. |
| [queryPreventionPolicies](https://falconpy.io/Service-Collections/Prevention-Policy.html#querypreventionpolicies) | Search for Prevention Policies in your environment by providing a FQL filter and paging details. Returns a set of Prevention Policy IDs which match the filter criteria. |
| [updatePreventionPolicies](https://falconpy.io/Service-Collections/Prevention-Policy.html#updatepreventionpolicies) | Update Prevention Policies by specifying the ID of the policy and details to update. |



## Real Time Response
These samples focus on CrowdStrike's Real Time Response and Real Time Response Admin API service collections.

- [Bulk execute a command](#bulk-execute-a-command)
- [Bulk execute a command (queued)](#bulk-execute-a-command-queued)
- [Dump memory for a running process](#dump-memory-for-a-running-process)
- [My Little RTR](#my-little-rtr)

### Bulk execute a command
Using this [demonstration](rtr#bulk-execute-a-command-on-matched-hosts), you can execute a command on multiple hosts that have a hostname matching a search string you provide.

[![Real Time Response](https://img.shields.io/badge/Service%20Class-Bulk%20execute%20a%20command-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](rtr#bulk-execute-a-command-on-matched-hosts)

#### Real Time Response API operations discussed
This sample demonstrates the following CrowdStrike Real Time Response and Real Time Response Admin API operations:

| Operation | Description |
| :--- | :--- |
| [BatchAdminCmd](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#batchadmincmd) | Batch executes a RTR administrator command across the hosts mapped to the given batch ID. |
| [BatchInitSessions](https://falconpy.io/Service-Collections/Real-Time-Response.html#batchinitsessions) | Batch initialize a RTR session on multiple hosts. Before any RTR commands can be used, an active session is needed on the host. |
| [RTR_DeleteSession](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_deletesession) | Delete a session. |

---

### Bulk execute a command (queued)

Building on the previous demonstration, this [sample](rtr/queued_execute.py) also executes a command on multiple hosts that have a hostname matching a search string, with the addition of queuing the commands for later processing should the host be offline.

[![Real Time Response](https://img.shields.io/badge/Service%20Class-Bulk%20execute%20a%20command_with_queuing-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](rtr/queued_execute.py)

#### Real Time Response API operations discussed
This sample demonstrates the following CrowdStrike Real Time Response and Real Time Response Admin API operations:

| Operation | Description |
| :--- | :--- |
| [BatchAdminCmd](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#batchadmincmd) | Batch executes a RTR administrator command across the hosts mapped to the given batch ID. |
| [BatchInitSessions](https://falconpy.io/Service-Collections/Real-Time-Response.html#batchinitsessions) | Batch initialize a RTR session on multiple hosts. Before any RTR commands can be used, an active session is needed on the host. |
| [RTR_CheckAdminCommandStatus](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_checkadmincommandstatus) | Get status of an executed RTR administrator command on a single host. |
| [RTR_DeleteSession](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_deletesession) | Delete a session. |
| [RTR_ListQueuedSessions](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_listqueuedsessions) | Get queued session metadata by session ID. |

---

### Dump memory for a running process
This [example](rtr/pid-dump) demonstrates using the CrowdStrike Real Time Response API to dump the memory contents of a specific process on the target host using the PID.

[![Real Time Response](https://img.shields.io/badge/Service%20Class-Dump%20memory%20for%20a%20running%20process-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](rtr/pid-dump)

#### Real Time Response API operations discussed
This sample demonstrates the following CrowdStrike Real Time Response and Real Time Response Admin API operations:

| Operation | Description |
| :--- | :--- |
| [RTR_CheckAdminCommandStatus](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_checkadmincommandstatus) | Get status of an executed RTR administrator command on a single host. |
| [RTR_CreatePut_Files](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_createput_files) | Upload a new put-file to use for the RTR `put` command. |
| [RTR_CreateScripts](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_createscripts) | Upload a new custom-script to use for the RTR `runscript` command. |
| [RTR_DeletePut_Files](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_deleteput_files) | Delete a put-file based on the ID given. Can only delete one file at a time. |
| [RTR_DeleteScripts](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_deletescripts) | Delete a custom-script based on the ID given. Can only delete one script at a time. |
| [RTR_DeleteSession](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_deletesession) | Delete a session. |
| [RTR_ExecuteAdminCommand](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_executeadmincommand) | Execute a RTR administrator command on a single host. |
| [RTR_GetExtractedFileContents](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_getextractedfilecontents) | Get RTR extracted file contents for specified session and sha256. |
| [RTR_InitSession](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_initsession) | Initialize a new session with the RTR cloud. |
| [RTR_ListPut_Files](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_listput_files) | Get a list of put-file ID's that are available to the user for the `put` command. |
| [RTR_ListScripts](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_listscripts) | Get a list of custom-script ID's that are available to the user for the `runscript` command. |

---

### My Little RTR
This [demonstration](rtr/pony) leverages the [ASCII-Pony](https://gitlab.com/mattia.basaglia/ASCII-Pony) open source project to retrieve basic system information from a target host (and draw My Little Ponies).

[![Real Time Response](https://img.shields.io/badge/Service%20Class-My%20Little%20RTR-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](rtr/pony)

#### Real Time Response API operations discussed
This sample demonstrates the following CrowdStrike Real Time Response and Real Time Response Admin API operations:

| Operation | Description |
| :--- | :--- |
| [RTR_CreateScripts](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_createscripts) | Upload a new custom-script to use for the RTR `runscript` command. |
| [RTR_CheckAdminCommandStatus](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_checkadmincommandstatus) | Get status of an executed RTR administrator command on a single host. |
| [RTR_DeleteSession](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_deletesession) | Delete a session. |
| [RTR_DeleteScripts](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_deletescripts) | Delete a custom-script based on the ID given. Can only delete one script at a time. |
| [RTR_ExecuteAdminCommand](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_executeadmincommand) | Execute a RTR administrator command on a single host. |
| [RTR_InitSession](https://falconpy.io/Service-Collections/Real-Time-Response.html#rtr_initsession) | Initialize a new session with the RTR cloud. |
| [RTR_ListScripts](https://falconpy.io/Service-Collections/Real-Time-Response-Admin.html#rtr_listscripts) | Get a list of custom-script ID's that are available to the user for the `runscript` command. |

## Sensor Download
The samples in this section focus on CrowdStrike Sensor Download API service collection.

### Download the CrowdStrike sensor
Use the Uber Class to [list or download versions of the CrowdStrike sensor](sensor_download/download_sensor.py).

[![Sensor Download](https://img.shields.io/badge/Uber%20Class-List%20or%20Download%20Falcon%20Sensor-silver?style=for-the-badge&labelColor=maroon&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](sensor_download/download_sensor.py)

#### Sensor Download API operations discussed
This sample demonstrates the following CrowdStrike Sensor Download API operations:

| Operation | Description |
| :--- | :--- |
| [DownloadSensorInstallerById](https://falconpy.io/Service-Collections/Sensor-Download.html#downloadsensorinstallerbyid) | Get sensor installer details by providing a query. |
| [GetCombinedSensorInstallersByQuery](https://falconpy.io/Service-Collections/Sensor-Download.html#getcombinedsensorinstallersbyquery) | Download sensor installer by SHA256 ID. |

## Sensor Update Policies
This section has samples that focus on the CrowdStrike Sensor Update Policies API service collection.

### Policy Wonk
Manage your sensor update policies with our [Policy Wonk](sensor_update_policies#manage-sensor-update-policies-with-policy-wonk) sample.

[![Sensor Update Policies](https://img.shields.io/badge/Service%20Class-Policy%20Wonk-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](sensor_update_policies#manage-sensor-update-policies-with-policy-wonk) 

#### Sensor Update Policies API operations discussed
This sample demonstrates the following CrowdStrike Sensor Update Policies API operations:

| Operation | Description |
| :--- | :--- |
| [createSensorUpdatePoliciesV2](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#createsensorupdatepoliciesv2) | Create Sensor Update Policies by specifying details about the policy to create. |
| [deleteSensorUpdatePolicies](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#deletesensorupdatepolicies) | Delete a set of Sensor Update Policies by specifying their IDs. |
| [performSensorUpdatePoliciesAction](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#performsensorupdatepoliciesaction) | Perform the specified action on the Sensor Update Policies specified in the request. |
| [queryCombinedSensorUpdateBuilds](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#querycombinedsensorupdatebuilds) | Retrieve available builds for use with Sensor Update Policies. |
| [queryCombinedSensorUpdateKernels](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#querycombinedsensorupdatekernels) | Retrieve kernel compatibility info for Sensor Update Builds. |
| [queryCombinedSensorUpdatePolicyMembers](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#querycombinedsensorupdatepolicymembers) | Search for members of a Sensor Update Policy in your environment by providing a FQL filter and paging details. Returns a set of host details which match the filter criteria. |
| [queryCombinedSensorUpdatePoliciesV2](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#querycombinedsensorupdatepoliciesv2) | Search for Sensor Update Policies with additional support for uninstall protection in your environment by providing a FQL filter and paging details. Returns a set of Sensor Update Policies which match the filter criteria. |
| [revealUninstallToken](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#revealuninstalltoken) | Reveals an uninstall token for a specific device. To retrieve the bulk maintenance token pass the value `MAINTENANCE` as the value for `device_id`. |
| [setSensorUpdatePoliciesPrecedence](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#setsensorupdatepoliciesprecedence) | Sets the precedence of Sensor Update Policies based on the order of IDs specified in the request. The first ID specified will have the highest precedence and the last ID specified will have the lowest. You must specify all non-Default Policies for a platform when updating precedence. |
| [updateSensorUpdatePoliciesV2](https://falconpy.io/Service-Collections/Sensor-Update-Policy.html#updatesensorupdatepolicies) | Update Sensor Update Policies by specifying the ID of the policy and details to update with additional support for uninstall protection. |


## Spotlight
These samples discuss leveraging the CrowdStrike Spotlight Evaluation Logic and Spotlight Vulnerabilities API service collections.

- [Find vulnerable hosts by CVE ID](#find-vulnerable-hosts-by-cve-id)
- [CISA DHS Known Exploited Vulnerabilities](#cisa-dhs-known-exploited-vulnerabilities)

### Find vulnerable hosts by CVE ID
In this [example](spotlight#identify-hosts-with-vulnerabilities-by-cve) we demonstrate searching Falcon Spotlight for vulnerable hosts based upon CVE ID.

[![Spotlight Vulnerabilities](https://img.shields.io/badge/Service%20Class-Identify%20Vulnerable%20Hosts%20by%20CVE-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](spotlight#identify-hosts-with-vulnerabilities-by-cve) 

#### Spotlight Vulnerabilities API operations discussed
This sample demonstrates the following CrowdStrike Spotlight Vulnerability API operations:

| Operation | Description |
| :--- | :--- |
| [getRemediationsV2](https://falconpy.io/Service-Collections/Spotlight-Vulnerabilities.html#getremediationsv2) | Get details on remediation by providing one or more IDs. |
| [getVulnerabilities](https://falconpy.io/Service-Collections/Spotlight-Vulnerabilities.html#getvulnerabilities) | Get details on vulnerabilities by providing one or more IDs. |
| [queryVulnerabilities](https://falconpy.io/Service-Collections/Spotlight-Vulnerabilities.html#queryvulnerabilities) | Search for Vulnerabilities in your environment by providing a FQL filter and paging details. Returns a set of Vulnerability IDs which match the filter criteria. |

---

### CISA DHS Known Exploited Vulnerabilities
Developed and submitted by `@ciberesponce`, this [solution](spotlight/CISA_known_exploited_vulns) provides simple CSV formatted output, sorting by DHS CISA's Due Date field, to allow for prioritization of mitigation actions across hosts. This is particularly useful for Departments and agencies (D/a) who are subject to CISA's due dates.

[![Spotlight Vulnerabilities](https://img.shields.io/badge/Service%20Class-CISA%20Known%20Exploited%20Vulnerabilities-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](spotlight/CISA_known_exploited_vulns) [![MSSP Use supported](https://img.shields.io/badge/-Supports%20MSSP-darkblue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==&style=for-the-badge)](spotlight/CISA_known_exploited_vulns)

#### Spotlight Vulnerabilities API operations discussed
This sample demonstrates the following CrowdStrike Spotlight Vulnerability API operations:

| Operation | Description |
| :--- | :--- |
| [queryVulnerabilities](https://falconpy.io/Service-Collections/Spotlight-Vulnerabilities.html#queryvulnerabilities) | Search for Vulnerabilities in your environment by providing a FQL filter and paging details. Returns a set of Vulnerability IDs which match the filter criteria. |

## User Management
This sample category is focused on examples that leverage CrowdStrike's User Management API service collection.

### Bulk user administration
This [sample](user_management#bulk-import-update-and-remove-users) demonstrates adding, updating and removing users in bulk using the User Management Service Class.

[![User Management](https://img.shields.io/badge/Service%20Class-Bulk%20Edit%20Users-silver?style=for-the-badge&labelColor=red&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==)](user_management#bulk-import-update-and-remove-users) [![MSSP Use supported](https://img.shields.io/badge/-Supports%20MSSP-darkblue?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAABhWlDQ1BJQ0MgcHJvZmlsZQAAKJF9kT1Iw1AUhU9TpaIVBzuIOGSoDmJBVEQ3rUIRKoRaoVUHk5f+CE0akhQXR8G14ODPYtXBxVlXB1dBEPwBcXNzUnSREu9LCi1ifPB4H+e9c7jvXkColZhmtY0Cmm6bqURczGRXxNAruhAEMI1hmVnGrCQl4bu+7hHg512MZ/m/+3N1qzmLAQGReIYZpk28Tjy5aRuc94kjrCirxOfEIyYVSPzIdcXjN84FlwWeGTHTqTniCLFYaGGlhVnR1IgniKOqplO+kPFY5bzFWStVWKNO/sNwTl9e4jrtASSwgEVIEKGggg2UYCNGp06KhRTdx338/a5fIpdCrg0wcsyjDA2y6wefwe/eWvnxMS8pHAfaXxznYxAI7QL1quN8HztO/QQIPgNXetNfrgFTn6RXm1r0COjZBi6um5qyB1zuAH1PhmzKrsTnL+TzwPsZjSkL9N4Cnate3xr3OH0A0tSr5A1wcAgMFSh7zeffHa19+/dNo38/hq9yr+iELI0AAAAGYktHRAAAAAAAAPlDu38AAAAJcEhZcwAACxMAAAsTAQCanBgAAAAHdElNRQflDAsTByz7Va2cAAAAGXRFWHRDb21tZW50AENyZWF0ZWQgd2l0aCBHSU1QV4EOFwAAAYBJREFUKM+lkjFIlVEYht/zn3sFkYYUyUnIRcemhCtCU6JQOLiIU+QeJEQg6BBIm0s4RBCBLjq5OEvgJC1uOniJhivesLx17/97/vO9b4NK4g25157hfHCGB773/cA0HZIEAKiMj+LWiOxljG/i96pnCFP58XHnrWX2+9cj0dYl9Yu2FE9/9rXrcAAgs2eSyiBfOe/XRD503h/CuffOubQVUXL+Jh9BllzBbyJJBgDclVkO4Kukd8zzkXJbeUljIldFTstsmSHM6S81ma2KfPKlFdkGAMY4wzx/bbXapMy21My+YizdKNq5mDzLkrxafSxySFKjSWX2oTmjKzz4vN0r2lOFcL/Q3V0/mX95ILMXTTGYVfaut/aP2+oCMAvnZgCcsF5fcR0dg65YHAdwB+QApADvu0AuOe/ftlJAD7Nsgmm6yBjDtfWORJZlNtFyo/lR5Z7MyheKA5ktSur7sTAHazSG27pehjAiaVfkN8b4XFIJ/wOzbOx07VNRUuHy7w98CzCcGPyWywAAAABJRU5ErkJggg==&style=for-the-badge)](user_management#bulk-import-update-and-remove-users)

#### User Management API operations discussed
This sample demonstrates the following CrowdStrike User Management API operations:

| Operation | Description |
| :--- | :--- |
| [CreateUser](https://falconpy.io/Service-Collections/User-Management.html#createuser) | Create a new user. After creating a user, assign one or more roles with [GrantUserRoleIds](https://falconpy.io/Service-Collections/User-Management.html#grantuserroleids). |
| [DeleteUser](https://falconpy.io/Service-Collections/User-Management.html#deleteuser) | Delete a user permanently. |
| [GetAvailableRoleIds](https://falconpy.io/Service-Collections/User-Management.html#getavailableroleids) | Show role IDs for all roles available in your customer account. For more information on each role, provide the role ID to [GetRoles](https://falconpy.io/Service-Collections/User-Management.html#getroles). |
| [GetUserRoleIds](https://falconpy.io/Service-Collections/User-Management.html#getuserroleids) | Show role IDs of roles assigned to a user. For more information on each role, provide the role ID to [GetRoles](https://falconpy.io/Service-Collections/User-Management.html#getroles). |
| [GrantUserRoleIds](https://falconpy.io/Service-Collections/User-Management.html#grantuserroleids) | Assign one or more roles to a user. |
| [RetrieveUser](https://falconpy.io/Service-Collections/User-Management.html#retrieveuser) | Get info about a user. |
| [RetrieveUserUUID](https://falconpy.io/Service-Collections/User-Management.html#retrieveuseruuid) | Get a user's ID by providing a username (usually an email address). |
| [RetrieveUserUUIDsByCID](https://falconpy.io/Service-Collections/User-Management.html#retrieveuseruuidsbycid) | List user IDs for all users in your customer account. For more information on each user, provide the user ID to [RetrieveUser](https://falconpy.io/Service-Collections/User-Management.html#retrieveuser). |
| [RevokeUserRoleIds](https://falconpy.io/Service-Collections/User-Management.html#revokeuserroleids) | Revoke one or more roles from a user. |




## Suggestions
Do you have a suggestion for an example you'd like to see? Are one of the examples not working as expected? Let us know by posting a message to our [discussion board](https://github.com/CrowdStrike/falconpy/discussions).

Have an example you've developed yourself that you'd like to share?  **_Excellent!_** Please review our [contributing guidelines](/CONTRIBUTING.md) and then submit a pull request.

---

<p align="center"><img src="https://raw.githubusercontent.com/CrowdStrike/falconpy/main/docs/asset/cs-logo-footer.png"><BR/><img width="450px" src="https://raw.githubusercontent.com/CrowdStrike/falconpy/main/docs/asset/turbine-panda-lines.png"></P>
<h3><P align="center">WE STOP BREACHES</P></h3>
