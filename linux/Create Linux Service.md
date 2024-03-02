# Create Linux Service

## path to Linux services

```bash
cd /etc/systemd/system/
```

## create .service file

**example file:**

```bash
[Unit]
Description=<Description of service usage>
After=<After which service this service should be started>

[Service]
Type=<Type of service>
User=<Username>
Group=<Groupname>
WorkingDirectory=<Start directory of the service execution> 
ExecStart=<Execution command>
Restart=<Restart options if services switching off>
Environment=<Set enviroment variables>

[Install]
WantedBy=<under which target should this service be activated>
```

| Guidelines       | Explaination                                                                                                                                                                                                           |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Description      | Short explaination of the service.                                                                                                                                                                                     |
| After            | Specifies after which other services or targets this service should be started.                                                                                                                                        |
| Type             | Startmode of the service. `simple` is the default value, other values are `forking`, `idle`, `oneshot`, `dbus` or `notify`.                                                                                            |
| User             | User under which service should run.                                                                                                                                                                                   |
| Group            | Group under which service should run.                                                                                                                                                                                  |
| WorkingDirectory | After start the service will change to working directory before executing the `ExecStart`                                                                                                                              |
| ExecStart        | The full path to the executable and additional parameters.                                                                                                                                                             |
| Restart          | Sets the behaviour after the serivce gets shut down. Values are `no`, `on-success`, `on-failure`, `always`, `on-abort`, `on-watchdog` and `on-abnormal`                                                                |
| Enviroment       | Sets enviroment variables for the service.                                                                                                                                                                             |
| WantedBy         | Specifies the target under which the service is to be activated and started when `systemctl enable` is executed. `multi-user.target` for a system service and `graphical.target` for a service with graphical interface | 

## Guideline `Type`

| Startmode | Explaination                                                                                                                                              |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `simple`  | Default value, systemd expects the main process stays in the foreground                                                                                   |
| `forking` | Used for services that fork themselves as part of their startup process. systemd considers the service started as soon as the parent process is finished. |
| `oneshot` | Used for one-time executions. After the execution is done the service will shut down.                                                                     |
| `dbus`    | For services that send a signal on the D-Bus system message bus to signal their readiness.                                                                |
| `notify`  | Service signals its readiness by sending a message to systemd via a special notify interface.                                                             |
| `idle`    | Service will be started after all standard services are started. The use serves to avoid resource collisions.                                             |

## Guideline `Restart`

| Restart option | Explaination                                                                          |
| -------------- | ------------------------------------------------------------------------------------- |
| `no`           | Service will not be restarted automatically                                           |
| `always`       | Service will always be restarted                                                      |
| `on-success`   | Service will only restart if it was ended with exit status code 0                     |
| `on-failure`   | Service will restart when it was ended because of an error, timeout or sigkill signal |
| `on-abnormal`  | Service will restart when it was ended because of timeout or signal                   |
| `on-abort`     | Service is restarted if it has been terminated by an uncaught signal                  |
| `on-watchdog`  | Service is restarted when the watchdog timer runs out                                 | 

## Activate and Start the Service

### reload the systemd daemon 

```bash
systemctl daemon-reload
```

### start the service

```bash
systemctl start <service name>
```

### activate service at system startup

```bash
systemctl enable <service name>
```