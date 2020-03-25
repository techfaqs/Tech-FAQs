# Cloud foundry cli commands

### cf - A command line tool to interact with Cloud Foundry

Cloud foundry is the open source PAAS(Platform As A Service). Following has the consolidated commands list one can use for 
daily deployment of apps-


#### USAGE
    cf [global options] command [arguments...] [command options]

#### GETTING STARTED
```
help	Show help
version	Print the version
login	Log user in
logout	Log user out
passwd	Change user password
target	Set or view the targeted org or space
api	Set or view target api url
auth	Authenticate non-interactively
```

#### APPS
```
apps	List all apps in the target space
app	Display health and status for an app
push	Push a new app or sync changes to an existing app
scale	Change or view the instance count, disk space limit, and memory limit for an app
delete	Delete an app
rename	Rename an app
start	Start an app
stop	Stop an app
restart	Stop all instances of the app, then start them again. This causes downtime.
restage	Recreate the app's executable artifact using the latest pushed app files and the latest environment (variables, service bindings, buildpack, stack, etc.). This action will cause app downtime.
restart-app-instance	Terminate, then restart an app instance
run-task	Run a one-off task on an app
tasks	List tasks of an app
terminate-task	Terminate a running task of an app
events	Show recent app events
files	Print out a list of files in a directory or the contents of a specific file of an app running on the DEA backend
logs	Tail or show recent logs for an app
env	Show all env variables for an app
set-env	Set an env variable for an app
unset-env	Remove an env variable from an app
stacks	List all stacks (a stack is a pre-built file system, including an operating system, that can run apps)
stack	Show information for a stack (a stack is a pre-built file system, including an operating system, that can run apps)
copy-source	Copies the source code of an application to another existing application (and restarts that application)
create-app-manifest	Create an app manifest for an app that has been pushed successfully
get-health-check	Show the type of health check performed on an app
set-health-check	Change type of health check performed on an app
enable-ssh	Enable ssh for the application
disable-ssh	Disable ssh for the application
ssh-enabled	Reports whether SSH is enabled on an application container instance
ssh	SSH to an application container instance
```

#### SERVICES

```
marketplace	List available offerings in the marketplace
services	List all service instances in the target space
service	Show service instance info
create-service	Create a service instance
update-service	Update a service instance
delete-service	Delete a service instance
rename-service	Rename a service instance
create-service-key	Create key for a service instance
service-keys	List keys for a service instance
service-key	Show service key info
delete-service-key	Delete a service key
bind-service	Bind a service instance to an app
unbind-service	Unbind a service instance from an app
bind-route-service	Bind a service instance to an HTTP route
unbind-route-service	Unbind a service instance from an HTTP route
create-user-provided-service	Make a user-provided service instance available to CF apps
update-user-provided-service	Update user-provided service instance
share-service	Share a service instance with another space
unshare-service	Unshare a shared service instance from a space
```

#### ORGS
```
orgs	List all orgs
org	Show org info
create-org	Create an org
delete-org	Delete an org
rename-org	Rename an org
SPACES
spaces	List all spaces in an org
space	Show space info
create-space	Create a space
delete-space	Delete a space
rename-space	Rename a space
allow-space-ssh	Allow SSH access for the space
disallow-space-ssh	Disallow SSH access for the space
space-ssh-allowed	Reports whether SSH is allowed in a space
```

#### DOMAINS
```
domains	List domains in the target org
create-domain	Create a domain in an org for later use
delete-domain	Delete a domain
create-shared-domain	Create a domain that can be used by all orgs (admin-only)
delete-shared-domain	Delete a shared domain
router-groups	List router groups
```

#### ROUTES
```
routes	List all routes in the current space or the current organization
create-route	Create a url route in a space for later use
check-route	Perform a simple check to determine whether a route currently exists or not
map-route	Add a url route to an app
unmap-route	Remove a url route from an app
delete-route	Delete a route
delete-orphaned-routes	Delete all orphaned routes in the currently targeted space (i.e. those that are not mapped to an app)
NETWORK POLICIES
network-policies	List direct network traffic policies
add-network-policy	Create policy to allow direct network traffic from one app to another
remove-network-policy	Remove network traffic policy of an app
```

#### BUILDPACKS
```
buildpacks	List all buildpacks
create-buildpack	Create a buildpack
update-buildpack	Update a buildpack
rename-buildpack	Rename a buildpack
delete-buildpack	Delete a buildpack
```

#### USER ADMIN
```
create-user	Create a new user
delete-user	Delete a user
org-users	Show org users by role
set-org-role	Assign an org role to a user
unset-org-role	Remove an org role from a user
space-users	Show space users by role
set-space-role	Assign a space role to a user
unset-space-role	Remove a space role from a user
```

#### ORG ADMIN
```
quotas	List available usage quotas
quota	Show quota info
set-quota	Assign a quota to an org
create-quota	Define a new resource quota
delete-quota	Delete a quota
update-quota	Update an existing resource quota
share-private-domain	Share a private domain with an org
unshare-private-domain	Unshare a private domain with an org
```

#### SPACE ADMIN
```
space-quotas	List available space resource quotas
space-quota	Show space quota info
create-space-quota	Define a new space resource quota
update-space-quota	Update an existing space quota
delete-space-quota	Delete a space quota definition and unassign the space quota from all spaces
set-space-quota	Assign a space quota definition to a space
unset-space-quota	Unassign a quota from a space
```

#### SERVICE ADMIN
```
service-auth-tokens	List service auth tokens
create-service-auth-token	Create a service auth token
update-service-auth-token	Update a service auth token
delete-service-auth-token	Delete a service auth token
service-brokers	List service brokers
create-service-broker	Create a service broker
update-service-broker	Update a service broker
delete-service-broker	Delete a service broker
rename-service-broker	Rename a service broker
migrate-service-instances	Migrate service instances from one service plan to another
purge-service-offering	Recursively remove a service and child objects from Cloud Foundry database without making requests to a service broker
purge-service-instance	Recursively remove a service instance and child objects from Cloud Foundry database without making requests to a service broker
service-access	List service access settings
enable-service-access	Enable access to a service or service plan for one or all orgs
disable-service-access	Disable access to a service or service plan for one or all orgs
```

#### SECURITY GROUP
```
security-group	Show a single security group
security-groups	List all security groups
create-security-group	Create a security group
update-security-group	Update a security group
delete-security-group	Deletes a security group
bind-security-group	Bind a security group to a particular space, or all existing spaces of an org
unbind-security-group	Unbind a security group from a space
bind-staging-security-group	Bind a security group to the list of security groups to be used for staging applications
staging-security-groups	List security groups in the staging set for applications
unbind-staging-security-group	Unbind a security group from the set of security groups for staging applications
bind-running-security-group	Bind a security group to the list of security groups to be used for running applications
running-security-groups	List security groups in the set of security groups for running applications
unbind-running-security-group	Unbind a security group from the set of security groups for running applications
```

#### ENVIRONMENT VARIABLE GROUPS
```
running-environment-variable-group	Retrieve the contents of the running environment variable group
staging-environment-variable-group	Retrieve the contents of the staging environment variable group
set-staging-environment-variable-group	Pass parameters as JSON to create a staging environment variable group
set-running-environment-variable-group	Pass parameters as JSON to create a running environment variable group
```

#### ISOLATION SEGMENTS
```
isolation-segments	List all isolation segments
create-isolation-segment	Create an isolation segment
delete-isolation-segment	Delete an isolation segment
enable-org-isolation	Entitle an organization to an isolation segment
disable-org-isolation	Revoke an organization's entitlement to an isolation segment
set-org-default-isolation-segment	Set the default isolation segment used for apps in spaces in an org
reset-org-default-isolation-segment	Reset the default isolation segment used for apps in spaces of an org
set-space-isolation-segment	Assign the isolation segment for a space
reset-space-isolation-segment	Reset the space's isolation segment to the org default
```

#### FEATURE FLAGS
```
feature-flags	Retrieve list of feature flags with status
feature-flag	Retrieve an individual feature flag with status
enable-feature-flag	Allow use of a feature
disable-feature-flag	Prevent use of a feature
```

#### ADVANCED
```
curl	Executes a request to the targeted API endpoint
config	Write default values to the config
oauth-token	Retrieve and display the OAuth token for the current session
ssh-code	Get a one time password for ssh clients
ADD/REMOVE PLUGIN REPOSITORY
add-plugin-repo	Add a new plugin repository
remove-plugin-repo	Remove a plugin repository
list-plugin-repos	List all the added plugin repositories
repo-plugins	List all available plugins in specified repository or in all added repositories
```

#### ADD/REMOVE PLUGIN
```
plugins	List commands of installed plugins
install-plugin	Install CLI plugin
uninstall-plugin	Uninstall CLI plugin
INSTALLED PLUGIN COMMANDS
ENVIRONMENT VARIABLES
CF_COLOR=false	Do not colorize output
CF_DIAL_TIMEOUT=6	Max wait time to establish a connection, including name resolution, in seconds
CF_HOME=path/to/dir/	Override path to default config directory
CF_PLUGIN_HOME=path/to/dir/	Override path to default plugin config directory
CF_TRACE=true	Print API request diagnostics to stdout
CF_TRACE=path/to/trace.log	Append API request diagnostics to a log file
all_proxy=proxy.example.com:8080	Specify a proxy server to enable proxying for all requests
https_proxy=proxy.example.com:8080	Enable proxying for HTTP requests
```

#### GLOBAL OPTIONS
```
--help, -h	Show help
-v	Print API request diagnostics to stdout
APPS (experimental)
v3-apps	List all apps in the target space
v3-create-app	Create a V3 App
v3-push	Push a new app or sync changes to an existing app
v3-scale	Change or view the instance count, disk space limit, and memory limit for an app
v3-delete	Delete a V3 App
v3-start	Start an app
v3-stop	Stop an app
v3-restart	Stop all instances of the app, then start them again. This causes downtime.
v3-stage	Create a new droplet for an app
v3-restart-app-instance	Terminate, then instantiate an app instance
v3-apply-manifest	Applies manifest properties to an application
v3-droplets	List droplets of an app
v3-set-droplet	Set the droplet used to run an app
v3-env	Show all env variables for an app
v3-set-env	Set an env variable for an app
v3-unset-env	Remove an env variable from an app
v3-get-health-check	Show the type of health check performed on an app
v3-set-health-check	Change type of health check performed on an app's process
v3-packages	List packages of an app
v3-create-package	Uploads a V3 Package
v3-ssh	SSH to an application container instance
```

Reference: 
http://cli.cloudfoundry.org/en-US/cf/
