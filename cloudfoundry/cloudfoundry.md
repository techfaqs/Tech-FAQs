# Cloud foundry cli commands

Cloud foundry is the open source PAAS( Platform As A Service ). Following has the consolidated commands list one can user for 
daily deployment of apps.

http://cli.cloudfoundry.org/en-US/cf/

help	Show help
version	Print the version
login	Log user in
logout	Log user out
passwd	Change user password
target	Set or view the targeted org or space
api	Set or view target api url
auth	Authenticate user non-interactively

apps	List all apps in the target space
app	Display health and status for an app
push	Push a new app or sync changes to an existing app
scale	Change or view the instance count, disk space limit, and memory limit for an app
delete	Delete an app
rename	Rename an app
start	Start an app
stop	Stop an app
restart	Stop all instances of the app, then start them again. This causes downtime.
restage	Recreate the app's executable artifact using the latest pushed app files and the latest environment (variables, service bindings, buildpack, stack, etc.)
restart-app-instance	Terminate the running application Instance at the given index and instantiate a new instance of the application with the same index
run-task	Run a one-off task on an app
tasks	List tasks of an app
terminate-task	Terminate a running task of an app
events	Show recent app events
files	Print out a list of files in a directory or the contents of a specific file of an app running on the DEA backend
logs	Tail or show recent logs for an app
env	Show all env variables for an app
set-env	Set an env variable for an app
unset-env	Remove an env variable
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
