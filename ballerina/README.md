# Consolidate-packages bal tool

Ballerina inherently supports microservices-style deployments, which are well-suited for microservice orchestration platforms like Kubernetes.
However, many enterprise users deploy on VMs or Docker, where managing each service as a separate process increases complexity and resource overhead.
This tool provides a solution tailored to such scenarios by enabling consolidated deployments.

## Usage

### Create or update a consolidator package

Create a new package and add the `consolidate-packages` tool entry as shown in the below example into the `Ballerina.toml` with the services required to consolidate. Services can be added or removed as needed by updating the values provided for the `options.services` array. The tool will be automatically pulled during the package build.

```toml
[package]
org = "myorg"
name = "hotel_app"
version = "0.1.0"

[[tool.consolidate-packages]]
id = "consolidateSvc"
options.services = ["myorg/customer_service", "myorg/menu_service"]
```

#### Using the CLI tool
Alternatively, the `consolidate-packages` CLI tool can be installed to create the package, and add or remove services. This
is typically useful in CI/CD pipelines.

##### Installation

Execute the command below to pull the tool.

```bash
bal tool pull consolidate-packages
```

##### Creating a new consolidator package

```bash
$ bal consolidate-packages new --package-path <path> <comma-separated-list-of-services> 
```

For example,

```bash
$ bal consolidate-packages new --package-path hotel-app myorg/order_service,myorg/payment_service 
```

##### Adding new services to an existing package

Execute the following command from the package root directory.

```bash
$ bal consolidate-packages add <comma-separated-list-of-services>
```

For example,

```bash
$ cd hotel-app
$ bal consolidate-packages add myorg/customer_service,myorg/menu_service
```

##### Removing services from an existing package
Execute the following command from the package root directory.

```bash
$ bal consolidate-packages remove <comma-separated-list-of-services>
```

For example,

```bash
$ bal consolidate-packages remove myorg/payment_service
```

Run `bal consolidate-services --help` for more information about the commands. 
