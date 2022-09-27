*Simple three tier application using new technologies.*
# AWS Three Tier Application
Simple three tier application. The web application requests the api, which then makes a query to the connected database system. The application can only work if all components are configured correctly.
```
  ┌──────────────┐       ┌──────────────┐      ┌──────────────┐
  │              │       │              │      │              │
  │              │       │              │      │              │
  │              │       │              │      │              │
  │     web      ├──────►│     api      ├─────►│   database   │
  │              │       │              │      │              │
  │              │       │              │      │              │
  │              │       │              │      │              │
  └──────────────┘       └──────────────┘      └──────────────┘
```
## Web
Simple web application written with NodeJS. The application starts the webserver on port `8080`.

### Configuration
The web application can be configured with several environment variables listed below:
|Env Variable|Description|Mandatory|
|---|---|---|
|MODULE_NAME|Module Name|Yes|
|GROUP_NAME|Group Name|Yes|
|API_HOST|API Host Address|Yes|
|API_PORT|API Host Port|Yes|

### Develop
1. Install packages
    ```bash
    $ npm install
    ```
2. Start server
    ```bash
    $ npm start
    ```

## API
Simple api application written in Go. The application starts the webserver on port `8000`.

|Path|Description|
|---|---|
|`/time`|Makes a query to get the time from the connected database.|
|`/healthz`|Delivers a response which indicates the health of the application.|

### Configuration
The api application can be configured with several environment variables or directly over dedicated files. Environment variables will have precedence over the dedicated files. 

The following environment variables / file paths can be used:
|Env Variable|Filepath|Description|Mandatory|
|---|---|---|---|
|LOG_PATH|`/var/config/log_path`|Log File Path|No (defaults to: `/var/log/logs.log`)|
|DEBUG|`/var/config/debug`|Boolean Value|No (when set to true all logs will be printed to `stdout`)|
|AWS_REGION|not available|AWS Region is necessary for the AWS SDK|Yes|

The following variables have to be defined in the AWS Parameter Store:
|Parameter Store Variable|Description|Mandatory|
|---|---|---|---|
|/cldinf/dbUrl|Database Host IP or Domain Name|Yes|
|/cldinf/dbName|Database Name|Yes|
|/cldinf/dbUser|Database User|Yes|
|/cldinf/dbPassword|Database Password|Yes|

### Develop 
1. Install dependencies
    ```bash
    $ go mod tidy
    ```
2. Start Application
    ```bash
    $ go run main.go
    ```

### Build
```bash
$ cd api
$ go build -a -o ./bin/
```

## Database
For the database a single `PostgreSQL` database is used.  
  
Have a look at the [Docker Hub](https://hub.docker.com) for the current tags and images.
# threetierapp
