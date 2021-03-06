# Kubernetes Elastic Agent plugin for GoCD

## Requirements

* GoCD server version v17.9.0 or above
* Kubernetes Cluster

## Installation

Copy the file `build/libs/kubernetes-elastic-agent-plugin-VERSION.jar` to the GoCD server under `${GO_SERVER_DIR}/plugins/external` 
and restart the server. The `GO_SERVER_DIR` is usually `/var/lib/go-server` on Linux and `C:\Program Files\Go Server` 
on Windows.

## Configuration

### Configure Plugin Settings

1. Login to `GoCD server` as admin and navigate to **_Admin_** _>_ **_Plugins_**
2. Click on **_Settings icon_** of `Kubernetes Elastic Agent Plugin` to update plugin settings configuration.
    1. Optionally specify `Go Server URL`, if GoCD secure site URL is not configured.
    2. Specify `Agent auto-register Timeout`
    3. Specify `Kubernetes Cluster URL`.
    4. Optionally specify `Kubernetes Cluster Username`, `Kubernetes Cluster Password` and `Kubernetes Cluster CA Certificate`, for secure Kubernetes Cluster.

    !["Kubernetes Plugin settings"][1]

## Create an elastic profile

1. Login to `GoCD server` as admin and navigate to **_Admin_** _>_ **_Elastic Agent Profiles_**

![Elastic Profiles][2]

2. Click on **_Add_** to create new elastic agent profile
    1. Specify `id` for profile.
    2. Select `Kubernetes Elastic Agent Plugin` for **_Plugin id_**
    3. Specify GoCD elastic agent docker image name.
    4. Specify Maximum Memory limit. Container memory will be limit to the value specified here.
    5. Specify Maximum CPU limit. Container memory will be limit to the value specified here.
    6. Optionally specify Environment Variables. These variables are passed to the container for use.
    7. Save your profile.
    
![Create elastic profile][3]    

### Configure job to use an elastic agent profile

1. Click the gear icon on **_Pipeline_**

![Pipeline][4]

2. Click on **_Quick Edit_** button

![Quick edit][5]

3. Click on **_Stages_**
4. Create/Edit a job
5. Enter the `unique id` of an elastic profile in Job Settings

![Configure a job][6]

6. Save your changes

## Troubleshooting

Enabling debug level logging can help you troubleshoot an issue with the elastic agent plugin. To enable debug level logs, edit the `/etc/default/go-server` (for Linux) to add:

```bash
export GO_SERVER_SYSTEM_PROPERTIES="$GO_SERVER_SYSTEM_PROPERTIES -Dplugin.cd.go.contrib.elasticagent.kubernetes.log.level=debug"
```

If you're running the server via `./server.sh` script —

```
$ GO_SERVER_SYSTEM_PROPERTIES="-Dplugin.cd.go.contrib.elasticagent.kubernetes.log.level=debug" ./server.sh
```


[1]: images/plugin_settings.png     "Kubernetes Plugin settings"
[2]: images/profiles_page.png  "Elastic profiles"
[3]: images/profile.png "Create elastic profile"
[4]: images/pipeline.png  "Pipeline"
[5]: images/quick-edit.png  "Quick edit"
[6]: images/configure-job.png  "Configure a job"