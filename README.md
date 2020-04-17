# Vonk Helm Chart

## Prerequisites Details

* Kubernetes 1.8+ with Beta APIs enabled.
* PV support on the underlying infrastructure.
* Vonk license

## Chart Details

This chart implements a [Vonk](https://fire.ly/vonk) deployment on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh/) package manager.

## Installing the Chart

To install the chart with the release name `my-release`:

``` console
$ helm repo add firely https://raw.githubusercontent.com/FirelyTeam/Vonk.Helm.Charts/master/
$ helm install --name my-release firely/vonk
```
The command deploys Vonk on the Kubernetes cluster in the default configuration. The configuration section lists the parameters that can be configured during installation.

## Uninstalling the Chart
To uninstall/delete the `my-release` deployment:

``` console 
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Vonk chart and their default values.


 Parameter                                                 | Description                                                               | Default                                             |
| -------------------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------------- |
| `replicaCount`                                           | Number of replicas in the replica set                                     | `1`                                                 |
| `image.repository`                                       | Vonk image name                                                           | `simplifier/vonk`                                   |
| `image.tag`                                              | Vonk image tag                                                            | `3.4.0`                                             |
| `image.pullPolicy`                                       | Vonk image pull policy                                                    |`IfNotPresent`                                       |
| `vonksettings`                                           | The override of the appsettings of Vonk. This must be a Json format. Do not forget to indent this with 2 white spaces.  | `{ }` |
| `logsettings`                                            | The override of the logsettings of Vonk. This must be a Json format.  Do not forget to indent this with 2 white spaces. | `{ }` |
| `license.secretName`                                     | You can  save the Vonk license key yourself as a Kubernetes secret. Use then the name of that secret here. This setting overrides `license.value`| `nil` |
| `license.fileName`                                       | The name of the license file used internally. No reason to change that. | `vonk-license.json` |
| `license.value`                                          | The content of the license. See also more information below. | `nil` |
| `license.requestInfoFile`                                | Sets the location of the file with request information. This file will be used in future releases.| `nil` |
| `license.writeRequestInfoFileInterval`                   | Sets the time interval (in minutes) to write aggregate information about processed requests to the RequestInfoFile.| `nil` |
| `plugins[].url`                                          | An absolute url where a Vonk plugin can be downloaded| `nil` |
| `plugins[].checksum`                                     | The checksum of the plugin | `nil` |
| `service.type`                                           | Kubernetes Service type | `LoadBalancer` |
| `service.port`                                           | The port which the Kubernetes service will expose the Vonk pod | `80` |
| `ingress.enabled`                                        | Enable ingress controller resource | `false` |
| `ingress.annotations`                                    | Annotations for this host's ingress record | `{}` |
| `ingress.ingressClass`                                   | | `nginx` |
| `ingress.certIssuer`                                     | | `letsencrypt-production` |
| `ingress.path`                                           | Path within the url structure | `/` |
| `ingress.hosts[0]`                                       | Hostname to your Vonk installation | `nil` |
| `persistence.enabled`                                    | | `false` |
| `readinessProbe.initialDelaySeconds`                     | Number of seconds after the container has started before readiness probes are initiated | `15` |
| `readinessProbe.timeoutSeconds`                          | Number of seconds after which the probe times out  | `5` |
| `readinessProbe.failureThreshold`                        | When a Pod starts and the probe fails, Kubernetes will try `failureThreshold` times before giving up. The Pod will be marked Unready. | `3`| 
| `readinessProbe.periodSeconds`                           | How often (in seconds) to perform the probe | `10` |
| `readinessProbe.successThreshold`                        | Minimum consecutive successes for the probe to be considered successful after having failed | `1` |
| `livenessProbe.initialDelaySeconds`                      | Number of seconds after the container has started before liveness probes are initiated | `10` |
| `livenessProbe.timeoutSeconds`                           | Number of seconds after which the probe times out | `5` |
| `livenessProbe.failureThreshold`                         | When a Pod starts and the probe fails, Kubernetes will try `failureThreshold` times before giving up. The Pod will restart | `3` |
| `livenessProbe.periodSeconds`                            | How often (in seconds) to perform the probe | `120` |
| `livenessProbe.successThreshold`                         | inimum consecutive successes for the probe to be considered successful after having failed | `1` |

## Obtaining and using a license

Download the the license file from [Simplifier.net](https://simplifier.net/vonk).

Transform the downloaded license in the following format and save it as `vonk-license.yaml' 

```yaml
license:
  value: '{"LicenseOptions": {"Kind": "Evaluation","ValidUntil": "2018-11-13","Licensee": "marco@fire.ly"}, "Signature": "+hLwZrrTL4tcW+l0r5yDHYSASM6EWiaVcRBN1..etc"}'
```
> **Note**: the option value should be on one line. No line feeds.

Install the Vonk Chart like this:
```console
$ helm install --name my-release -f .\vonk-license.yaml firely/vonk 
```

## Override Vonk settings

You can override the default configuration settings of Vonk by override the appsettings elements, like described in http://docs.simplifier.net/vonk/configuration/appsettings.html. 

In the following example the `InformationModel` has been overriden. The default is now `Fhir4.0` instead of `Fhir3.0`, which is the default. Furthermore the minimal loglevel is set to `Information`.

```yaml
vonksettings: 
  {
    "InformationModel":{
      "Default":"Fhir4.0"
    }
  }

logsettings:
  {
    "Serilog": {
      "MinimumLevel": {
        "Default": "Information"
      }
    }
  }
```

> **Note**: be carefull to indent the json snippet correctly! The first curly bracket should have been indented with 2 white spaces. The next element (in our example `"InformationModel"`) should be prefixed with 4 white spaces, etc.

> **Note**: don't use double forward slashes (`//`) to comment out sections. JSON formally has no notion of comments.

Install the Vonk Chart like this:
```console
$ helm install --name my-release -f .\settings.yaml firely/vonk 
```