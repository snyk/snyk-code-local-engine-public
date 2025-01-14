# Changelog

All notable changes to Code Local Engine project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

<a id="v2.11.0" />

## v2.11.0

#### 2025-01-09

### Changed

- Snyk Code rules updated
- Updated `broker-client` to [4.203.4](https://github.com/snyk/broker/releases/tag/v4.203.4)
- Update routing to handle Code PR checks in `sast-analysis-api` instead of `code-pr-check-service`. The `code-pr-check-service` has been made redundant and is pending removal.

### Removed

- The `broker-client` no longer supports body logging (`broker-client.logEnableBody`). This value is deprecated, and has no effect if specified.

### Fixed

- `scm-bundle-store` and `minio` images upgraded to resolve a vulnerability in the [Golang SSH package](https://security.snyk.io/vuln/SNYK-GOLANG-GOLANGORGXCRYPTOSSH-8496611). This vulnerability was not reachable in SCLE.

<a id="v2.10.0" />

## v2.10.0

#### 2024-10-28

### Added

- `broker-client` supports the [GitHub Server App](https://docs.snyk.io/scm-ide-and-ci-cd-integrations/snyk-scm-integrations/github-server-app) integration type - this functionality is in Closed Beta. Discuss with your Snyk representative for enablement.
- New documentation to support configuration of GitHub Server App connections with Snyk Code Local Engine

### Fixed

- Corrected `github-com` to `github` when specifying a Universal Broker connection to `github.com`
- Removed the `ephemeral-storage` limit for `scm-bundle-store`. This prevents pods that were previously being replaced by Kubernetes when exceeding `ephemeral-storage` limits remaining until cluster-level garbage collection occurs, keeping health checks accurate.

### Changed

- Snyk Code rules updated
- Updated `broker-client` to [4.196.7](https://github.com/snyk/broker/releases/tag/v4.196.7)

<a id="v2.9.0" />

## v2.9.0

#### 2024-08-19

### Added

- Included `.snyk` ignore file for Minio
- Add Snyk Code Local Engine documentation as a pdf

### Changed

- `broker-client` now deploys as a statefulset to increase stability when running in HA mode
- Updated `scm-bundle-store` to use Minio instead of MongoDB for backend storage
- `global.localEngine.mongodbSecretName` is deprecated, replaced by `global.localEngine.s3SecretName` and `global.localEngine.jwtSecretName`.
- Updated `broker-client` to [4.193.4](https://github.com/snyk/broker/releases/tag/v4.193.4)

### Removed

- References to the MongoDB image are removed

### Fixed

- Removed the deprecated form of `deeproxy.verificationEndpoint` from `values-customer-settings.yaml`, using `api.snyk.io` instead
- Added `broker-client.brokerDispatcherUrl` to `values-customer-settings.yaml` for High Availability Broker

<a id="v2.8.2" />

## v2.8.2

#### 2024-06-21

### Added

- Support for Personal Access Token in Bitbucket Server

### Fixed

- Resolved an ingress deployment failure when TLS secret name is provided. The fix ensures that Snyk Code Local Engine can now correctly use a pre-existing TLS secret for the certificate and key material when specified
- Corrected Broker behaviour when encountering non-ASCII characters in payloads
- Resolves some C++ analyses reporting all issues on line 1

### Changed

- Updated `broker-client` to [4.190.3](https://github.com/snyk/broker/releases/tag/v4.190.3)
- Update Snyk Code services with latest rulesets

<a id="v2.8.1" />

## v2.8.1

#### 2024-04-15

### Fixed

- Updated values-customer-settings.yaml file with new settings for Universal Broker

### Changed

- Updated MongoDB image to Debian 12 version
- Updated ignores for MongoDB
- Updated `broker-client` to [4.181.1](https://github.com/snyk/broker/releases/tag/v4.181.1)

<a id="v2.8.0" />

## v2.8.0

#### 2024-03-14

### Fixed

- Removed local analysis queue debug endpoints
- Corrected a filter for the GitLab Snyk Broker that would cause some requests to fail

### Changed

- Updated the list of images to remove the standalone `mongodb` image, which is no longer required
- Updated `broker-client` to [v4.179.3](https://github.com/snyk/broker/releases/tag/v4.179.3)

### Added

- Support for multiple SCMs/instances of SCMs via Broker in Universal mode
- Updated snyk ignore file for Redis

<a id="v2.7.11" />

## v2.7.11

#### 2024-02-08

### Added

- Added versioned snyk ignore (.snyk) files. These files detail any vulnerabilities within Snyk Code Local Engine that are either unreachable or otherwise not valid.

### Fixed

- Resolved a Helm validation bug for Broker

### Changed

- Snyk Code rules updated
- Updated `broker-client` to [v4.174.1](https://github.com/snyk/broker/releases/tag/v4.174.1)

### Removed

- `scm-bundle-store.server.useTokenAuth` is now deprecated - repository detection should ensure the presence of required headers for self-hosted Azure DevOps/TFS servers. This value now has no effect.

<a id="v2.7.10" />

## v2.7.10

#### 2024-01-26

### Added

- `scm-bundle-store.server.useTokenAuth` for compatibility with self-hosted Azure DevOps Server

### Fixed

- Corrected documentation for using EU or AU Snyk tenants with Snyk Code Local Engine
- Resolved a bug that caused git requests to Azure DevOps Server to fail

### Changed

- Snyk Code rules updated
- Introduced additional validation rules for EU or AU Snyk tenant usage
- Updates the default Snyk API domain from `https://snyk.io` to `https://api.snyk.io`
- Updated the `broker-client` to [v4.172.6](https://github.com/snyk/broker/releases/tag/v4.172.6)

<a id="v2.7.9" />

## v2.7.9

#### 2024-01-16

### Fixed

- Resolved a bug preventing cleanup jobs from running successfully

### Changed

- Updates to Snyk images for updated rulesets
- Updated the `broker-client` to [v4.172.2](https://github.com/snyk/broker/releases/tag/v4.172.2)

<a id="v2.7.8" />

## v2.7.8

#### 2024-01-11

### Changed

- Documentation updated to include alternative tenant setup
- Updates to Snyk images for new rulesets
- Updated the `broker-client` to [v4.171.9](https://github.com/snyk/broker/releases/tag/v4.171.9)

<a id="v2.7.7" />

## v2.7.7

#### 2023-12-07

### Fixed

- Snyk Code rules updated
- Suggest services updated JDK to remove vulnerabilities
- Documentation updated to remove "Overview" section and streamline introduction to Snyk Code Local Engine

<a id="v2.7.6" />

## v2.7.6

#### 2023-12-07

### Added

- CronJobs to clean up older/expired data in MongoDB

### Changed

- Minimum Kubernetes version is now 1.21

<a id="v2.7.5" />

## v2.7.5

#### 2023-11-27

### Fixed

- Fixed non-reachable vulnerabilities in the scm-bundle-store and mongodb components.

<a id="v2.7.4" />

## v2.7.4

#### 2023-11-23

### Changed

- Corrected the list of images under the Private Registry section

### Removed

- The `scm-meld` component is no longer required and has been removed

### Fixed

- Resolved an "Unauthorized" failure during IDE and CLI scans occurring after a proxy CA certificate change. The fix ensures that Snyk Code Local Engine properly picks up the new configuration when redeployed.

<a id="v2.7.3" />

## v2.7.3

#### 2023-11-10

### Changed

- The `/status` endpoint is now also presented on `/` for better compatibility with Load Balancer health checks

<a id="v2.7.2" />

## v2.7.2

#### 2023-11-08

### Changed

- Updated the `broker-client` to [v4.169.2](https://github.com/snyk/broker/releases/tag/v4.169.2)
- Updates to latest Snyk Code rules
- Updates to Snyk Code services

### Fixed

- Fixed outbound CA support for SCM when a proxy is not utilized

<a id="v2.7.1" />

## v2.7.1

#### 2023-10-17

### Changed

- Updated the architectural diagram with `suggest-sticky` component

<a id="v2.7.0" />

## v2.7.0

#### 2023-10-17

### Added

- Introduced a new `largeManifestFileRule` value, gives the option to add rule for fetching large manifest file. Avaliable for Github and Github Enterprise only.
- Caching mechanism for IDE scans by the new `suggest-sticky` component.

### Changed

- Updated architecture diagram with new internal-proxy connectivity

## v2.6.1

#### 2023-09-20

### Changed

- Updated Ingress template to include the `host` key if specified
- Updated documentation for JetBrains IDE

## v2.6.0

#### 2023-09-18

### Added

- `internal-proxy` component (based on `envoy`) replaces routes previously defined by the Ingress resource

### Changed

- Updated the `broker-client` to [v4.163.0](https://github.com/snyk/broker/releases/tag/v4.161.0)
- Ingress resource simplified - defies one route (`/`) and removes the need for request rewriting/regex capture groups

### Fixed

- Updated documentation for proxy and custom Certificate Authority support for better clarity
- Specify the `brokerServerUrl` by default in the `values-customer-settings.yaml` file

### Removed

- Any references to the previously-used MongoDB Sharded cluster in documentation
- The pre-packaged NGINX Ingress Controller is removed. Functionality is handled internally by the `internal-proxy` component

## v2.5.0

#### 2023-09-04

### Added

- Allows python projects that use poetry to be scanned by Snyk Open Source through the broker

### Changed

- Updated the `broker-client` to [v4.161.0](https://github.com/snyk/broker/releases/tag/v4.161.0)
- Updated Snyk Code services for latest analysis rules
- Changed database infrastructure for `scm-bundle-store` from a sharded MongoDB cluster to a single MongoDB instance

### Fixed

- Fixed an upgrade/stability issue with MongoDB by migrating to a single MongoDB instance

## v2.4.2

#### 2023-08-17

### Added

- Snyk Code Local Engine now supports custom CAs towards SCMs via `global.privateCaCert.*` values.
- A subset of available Helm values are listed in documentation
- A subset of available Helm values are subject to input validation
- The IDE has been added to the Architecture diagram

#### Changed

- NGINX Ingress documentation has been updated to better reflect usage and deployment options

### Deprecated

- The `global.proxy.cert` and `global.proxy.useCustomCert` values are both _deprecated_.

## v2.4.1

#### 2023-07-14

### Added

- The inbuilt NGINX Ingress Controller is now disabled by default, and is separate from the Ingress resource. This enables customers to re-use their own instance of NGINX Ingress Controller without manually manipulating the Chart.
  - To enable the NGINX Ingress Controller, set `global.ingressController.enabled: true`.

## v2.4.0

#### 2023-07-13

### Added

- Support for custom image registries:
  - Authenticated/unauthenticated private registries
  - Custom image pull secrets

## v2.3.0

#### 2023-07-12

### Added

- IDE Scans for VSCode v1.21 and higher

## v2.2.3

#### 2023-06-15

### Added

- Update of scm-meld to support custom CA override
- Update of files-bundle-store to improve CPU usage, and concurrency

## v2.2.2

#### 2023-06-13

### Fixed

- Suggest has been upgraded with some key bug fixes:
  - Better queueing mechanism to reduce stuck analyses
  - Introduced better analyses timeout mechanisms
  - Suggest runs as non-root

## v2.2.1

#### 2023-06-09

### Added

- Migrates additional services to run as non-root

### Fixed

- Inconsistency when deploying Local Engine to a custom namespace
- Webhook creation for PR checks

## v2.2.0

#### 2023-05-12

### Added

- Modular service deployment, only deploy the services needed for the intended use case
- PR check functionality
- Ability to configure self managed secrets
- Partial standardisation of service base images (more to follow)
- Partial migration of services not to run as root anymore (more to follow)
- Updates core Snyk Code services to include new rule sets

### Removed

- We removed CRDs and ClusterRoles - no more cluster-wide access needed.

## v2.0.0

#### 2023-04-20

### Added

- Includes the “new” Snyk Code stack, giving customers parity between Snyk SaaS and Local Engine environments.
- We host the Helm Chart on Dockerhub - customers can pull the Helm Chart with the same credentials for v1.Documentation and the values-customer-settings.yaml are still shared manually with the customer.

### Removed

- We removed CRDs and ClusterRoles - no more cluster-wide access needed.

### Changed

- This release does not include PR Checks. CLI scans/ Imports are currently supported.
- This release does not include pulling images from a custom registry.
- This release does not include centralised logging.
