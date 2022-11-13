# Growthbook & Monk
This repository contains Monk.io template to deploy Growthbook & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/Burakhan/monk-growthbook
```

## Load Template
```bash
cd monk-growthbook
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list monk-growthbook
✔ Got the list
Type      Template                       Repository  Version  Tags
runnable  monk-growthbook/growthbook     local       -        -
runnable  monk-growthbook/growthbook-db  local       -        -
group     monk-growthbook/stack          local       -        -
```

## Deploy Stack
```bash
foo@bar:~$ monk run monk-vaultwarden/stack
? Select tag to run [local/monk-growthbook/stack] on: mnk
✔ Starting the job: local/monk-growthbook/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% growthbook/growthbook:latest mnk
✔ [================================================] 100% mongo:latest mnk
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Started local/monk-growthbook/stack

🔩 templates/local/monk-growthbook/stack
 └─🧊 Peer mnk
    ├─🔩 templates/local/monk-growthbook/growthbook
    │  └─📦 aaf1b34cf8be374551539e3d6d6fbd19-ok-growthbook-monk-vaultwarden
    │     ├─🧩 growthbook/growthbook:latest
    │     ├─💾 /var/lib/monkd/volumes/growthbook -> /usr/local/src/app/packages/back-end/uploads
    │     ├─🔌 open 13.51.200.163:3100 (0.0.0.0:3100) -> 3100
    │     └─🔌 open 13.51.200.163:3000 (0.0.0.0:3000) -> 3000
    └─🔩 templates/local/monk-growthbook/growthbook-db
       └─📦 0921ecdbc1abeef8f50ff0c1208b520d-ok-growthbook-db-monk-mongo-db
          └─🧩 mongo:latest

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/monk-growthbook/stack - Inspect logs
	monk shell     local/monk-growthbook/stack - Connect to the container's shell
	monk do        local/monk-growthbook/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```
## Check web gui

`http://13.51.200.163:3000/`



## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                               	|
|------------------------------	|-------------------------------------------	|
| jtw_secret                    | Growthbook jwt secret, Default: monk 	               |
| growthbook_domain                    | Growthbook domain Default: growthbook.monk.io  	               |
| growthbook_http                    | http or https, Default: http 	               |
| growthbook_port1                    | Growthbook port, Default: 3100 	               |
| growthbook_port2                    | Growthbook port, Default: 3000 	               |
| db_password                    | DB Password, Default: monk 	               |




## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```

