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

> **Note**: Not all the parameters have been documented yet. These will be documented soon.

 Parameter                                                 | Description                                                               | Default                                             |
| -------------------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------------- |
| `replicaCount`                                           | Number of replicas in the replica set                                     | `1`                               |
| `image.repository`                                       | Vonk image name                                                           | `simplifier/vonk`                            |
| `image.tag`                                              | Vonk image tag                                                            | `1.0.0`                                      |
| `image.pullPolicy`                                       | Vonk image pull policy                                                    | `IfNotPresent`                                             |
| `vonk.administration.cosmosDbOptions.connectionString`   | [Using Microsoft Azure CosmosDB](http://docs.simplifier.net/vonk/configuration/db_cosmosdb.html#configure-cosmosdb)  | `nil`                        |
| `vonk.administration.cosmosDbOptions.entryCollection`    | [Using Microsoft Azure CosmosDB](http://docs.simplifier.net/vonk/configuration/db_cosmosdb.html#configure-cosmosdb)  | `vonkentries`    |
| `vonk.administration.mongoDbOptions.connectionString`    | [Using MongoDb](http://docs.simplifier.net/vonk/configuration/db_mongo.html#configure-mongodb) | `nil`                                      |
| `vonk.administration.mongoDbOptions.entryCollection`     | [Using MongoDb](http://docs.simplifier.net/vonk/configuration/db_mongo.html#configure-mongodb)   | `vonkentries`                                             |
| `vonk.administration.repository`                         |  Choose which type of repository you want. Valid values are: Memory, SQL, SQLite, MongoDb    | `SQLite`                                               |
| `vonk.administration.security.allowedNetworks`           | [Using limited access](http://docs.simplifier.net/vonk/configuration/administration.html#limited-access)                                                 | `{}`                         |
| `vonk.administration.security.operationsToBeSecured`     | [Using limited access](http://docs.simplifier.net/vonk/configuration/administration.html#limited-access)                                | `{}`                                                |
| `vonk.administration.sqlDbOptions.autoUpdateDatabase`    | [Using SQL Server](http://docs.simplifier.net/vonk/configuration/db_sql.html#configure-sql) | `true`                                                |
| `vonk.administration.sqlDbOptions.connectionString`      | [Using SQL Server](http://docs.simplifier.net/vonk/configuration/db_sql.html#configure-sql) | `nil`|
| `vonk.administration.sqLiteDbOptions.autoUpdateDatabase` | [Using SQLite](http://docs.simplifier.net/vonk/configuration/db_sqlite.html#configure-sqlite)                                          | `true`                                                |
| `vonk.administration.sqLiteDbOptions.connectionString`   | [Using SQLite](http://docs.simplifier.net/vonk/configuration/db_sqlite.html#configure-sqlite) | `nil`|
| `vonk.administrationImportOptions.importDirectory`       |                           | `./vonk-import`          |
| `vonk.administrationImportOptions.importedDirectory`     |                         | `./vonk-imported`          |
| `vonk.administrationImportOptions.maxInParallel`         |                        | `5`          |
| `vonk.bundleOptions.defaultCount`                        | `DefaultCount` sets the number of results if the user has not specified a `_count` parameter.  |  `10`|
| `vonk.bundleOptions.maxCount`                            | `MaxCount` sets the number of results in case the user specifies a `_count` value higher than this maximum.  |  `50`|
| `vonk.cache.maxConformanceResources`                     |  |  `5000` |
| `vonk.fhirCapabilities.conditionalDeleteOptions.conditionalDeleteType` | | `Single` |
| `vonk.fhirCapabilities.conditionalDeleteOptions.conditionalDeleteMaxItems` | | `1` |
| `vonk.historyOptions.maxReturnedResults`                 | | `100` |
| `vonk.hosting.httpPort`                                  | | `4080` |
| `vonk.memoryOptions.simulateTransactions`                | | `false` |
| `vonk.mongoDbOptions.connectionString`                   | [Using MongoDb](http://docs.simplifier.net/vonk/configuration/db_mongo.html#configure-mongodb)   | `nil` |
| `vonk.mongoDbOptions.entryCollection`                    | [Using MongoDb](http://docs.simplifier.net/vonk/configuration/db_mongo.html#configure-mongodb)   | `vonkentries` |
| `vonk.mongoDbOptions.simulateTransactions`               | | `false` |
| `vonk.reindexOptions.batchSize`                          | | `100` |
| `vonk.reindexOptions.maxDegreeOfParallelism`             | | `10` |
| `vonk.repository`                                        | Choose which type of repository you want. Valid values are: Memory, SQL, SQLite, MongoDb | `SQLite` |
| `vonk.sizeLimits.maxBatchEntries`                        | `MaxBatchEntries` limits the number of entries that is allowed in a batch or transaction bundle. | `200` |
| `vonk.sizeLimits.maxBatchSize`                           | `MaxBatchSize` sets the maximum size of a batch or transaction bundle. (Note that a POST http(s)://<vonk-endpoint>/Bundle will be limited by MaxResourceSize, since the bundle must be processed as a whole then.) | `5MiB` |
| `vonk.sizeLimits.maxResourceSize`                        | `MaxResourceSize` sets the maximum size of a resource that is sent in a create or update. | `1MiB` |
| `vonk.smartAuthorizationOptions.audience`                | | `vonk` |
| `vonk.smartAuthorizationOptions.enabled`                 | | `false` |
| `vonk.smartAuthorizationOptions.filters`                 | | `{}` |
| `vonk.smartAuthorizationOptions.protected.instanceLevelInteractions` | | `{}` |
| `vonk.smartAuthorizationOptions.protected.typeLevelInteractions` | | `{}` |
| `vonk.smartAuthorizationOptions.protected.wholeSystemInteractions` | | `{}` |
| `vonk.smartAuthorizationOptions.requireHttpsToProvider`  | | `false` |
| `vonk.sqlDbOptions.autoUpdateDatabase`                   | [Using SQL Server](http://docs.simplifier.net/vonk/configuration/db_sql.html#configure-sql) | `true` |
| `vonk.sqlDbOptions.connectionString`                     | [Using SQL Server](http://docs.simplifier.net/vonk/configuration/db_sql.html#configure-sql) | `` |
| `vonk.sqLiteDbOptions.autoUpdateDatabase`                | [Using SQLite](http://docs.simplifier.net/vonk/configuration/db_sqlite.html#configure-sqlite) | `true` |
| `vonk.sqLiteDbOptions.connectionString`                  | [Using SQLite](http://docs.simplifier.net/vonk/configuration/db_sqlite.html#configure-sqlite) | `` |
| `vonk.subscriptionEvaluatorOptions.enabled`              | | `true` |
| `vonk.subscriptionEvaluatorOptions.repeatPeriod`         | | `20000` |
| `vonk.subscriptionEvaluatorOptions.subscriptionBatchSize` | | `1` |
| `vonk.supportedInteractions.instanceLevelInteractions`   | | `20000` |
| `vonk.supportedInteractions.typeLevelInteractions`       | | `20000` |
| `vonk.supportedInteractions.wholeSystemInteractions`     | | `20000` |
| `vonk.supportedModel.restrictToResources`                | | `{}` |
| `vonk.supportedModel.restrictToSearchParameters`         | | `{}` |
| `vonk.supportedModel.restrictToCompartments`             | | `{}` |
| `vonk.validation.allowedProfiles`                        | | `{}` |
| `vonk.validation.validateIncomingResources`              | | `false` |
| `log.minimumLevel.default`                               | | `Error` |
| `log.minimumLevel.override`                              | | `{}` |
| `log.writeTo.console.restrictedToMinimumLevel`           | | `Information` |
| `log.writeTo.console.outputTemplate`                     | | `` |
| `log.writeTo.rollingFile.pathFormat`                     | | `%temp%/vonk-{Date}.log` |
| `log.writeTo.rollingFile.fileSizeLimitBytes`             | | `` |
| `log.writeTo.rollingFile.retainedFileCountLimit`         | | `7` |
| `log.writeTo.rollingFile.outputTemplate`                 | | `` |
| `log.writeTo.rollingFile.restrictedToMinimumLevel`       | | `Information` |
| `log.writeTo.applicationInsightsTraces.restrictedToMinimumLevel` | | `Information` |
| `license.secretName`                                     | | `nil` |
| `license.fileName`                                       | | `vonk-license.json` |
| `license.value`                                          | | `nil` |
| `service.type`                                           | Kubernetes Service type | `LoadBalancer` |
| `service.port`                                           | The port which the Kubernetes service will expose the Vonk pod | `80` |
| `ingress.enabled`                                        | Enable ingress controller resource | `false` |
| `ingress.annotations`                                    | Annotations for this host's ingress record | `{}` |
| `ingress.ingressClass`                                   | | `nginx` |
| `ingress.certIssuer`                                     | | `letsencrypt-production` |
| `ingress.path`                                           | Path within the url structure | `/` |
| `ingress.hosts[0]`                                       | Hostname to your Vonk installation | `nil` |
| `persistence.enabled`                                    | | `false` |
| `readinessProbe.initialDelaySeconds`                     | Number of seconds after the container has started before readiness probes are initiated | `120` |
| `readinessProbe.timeoutSeconds`                          | Number of seconds after which the probe times out  | `5` |
| `readinessProbe.failureThreshold`                        | When a Pod starts and the probe fails, Kubernetes will try `failureThreshold` times before giving up. The Pod will be marked Unready. | 3`| 
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

```console
license:
  value: '{"LicenseOptions": {"Kind": "Evaluation","ValidUntil": "2018-11-13","Licensee": "marco@fire.ly"}, "Signature": "+hLwZrrTL4tcW+l0r5yDHYSASM6EWiaVcRBN1..etc"}'
```
> **Note**: the option value should be on one line. No line feeds.

Install the Vonk Chart like this:
```console
$ helm install --name my-release -f .\vonk-license.yaml firely/vonk 
```