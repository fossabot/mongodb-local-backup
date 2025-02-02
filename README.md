# MongoDB Local Backup
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fcatfishlty%2Fmongodb-local-backup.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fcatfishlty%2Fmongodb-local-backup?ref=badge_shield)

A tool can back up your MongoDB data in Local File system.

## Usage
### 1. define config file
#### 1.1 config file type
`MLB` support 3 types of config files, they're `json`, `toml` and `yaml`.
And here're the example of the config files: [json](), [toml](), [yaml]()

#### 1.2 config file have several fields
| key | value | required | description |
| --- | :-- | :--: | :-- |
| mongo | C:\Program Files\MongoDB\Tools\100\bin\mongoexport.exe | Y | specific 'mongoexport' path |
| host | 127.0.0.1 | Y | MongoDB service host |
| port | 127.0.0.1 | Y | MongoDB service port |
| username | test | N | MongoDB service username for authentication, use with password, unset or set to null means no authentication |
| password | test | N | MongoDB service password for authentication, use with username, unset or set to null means no authentication
| target | 'must be an array' | Y | define which db and collection to export |
| db | 'must be an object' | Y | define which db to export |
| collection | 'must be an array' | Y | define which collections in this db to export |
| prefix | mongodb-local-backup | N | define the prefix of the exported data file names |
| type | json/csv | Y | define the export data file format |
| output | E:\mongo_backup\ | Y | define the directory where store the export data files.
| cron | */1 * * * * | N | define when run the export task, it will work only with command include '-d' option.| 

#### 1.3 config file example
[config.json]()
```json
{
  "mongo": "C:\\Program Files\\MongoDB\\Tools\\100\\bin\\mongoexport.exe",
  "host": "127.0.0.1",
  "port": 27017,
  "username": null,
  "password": null,
  "target": [
    {
      "db": "test",
      "collection": [
        "test",
        "test1"
      ]
    }
  ],
  "Prefix": "mongodb-local-backup-json",
  "Type": "json",
  "Output": "E:\\mongo_backup\\",
  "Cron": "*/1 * * * *"
}
```

[config.toml]()
```toml
# Define the path of mongoexport executable
mongo = "C:\\Program Files\\MongoDB\\Tools\\100\\bin\\mongoexport.exe"
# MongoDB host
host = "127.0.0.1"
# MongoDB port
port = 27017
# username of MongoDB connection
# username =
# password of MongoDB connection
# password =
# prefix is the prefix of exported data file name.
prefix = "mongodb-local-backup-toml"
#
type = "json"
output = "E:\\mongo_backup\\"
cron = "*/1 * * * *"
# define the MongoDB db and collections in target, mlb can do the backup for multiple dbs and collections.
[[target]]
db = "test"
collection = ["test", "test1"]
```

[config.yaml]()
```yaml
mongo: C:\\Program Files\\MongoDB\\Tools\\100\\bin\\mongoexport.exe
host: 127.0.0.1
port: 27017
target:
  -
    db: test
    collection:
      - test
      - test1
Prefix: "mongodb-local-backup-yaml"
Type: json
Output: "E:\\mongo_backup\\"
Cron: '*/1 * * * *'
```

### 2. Run command
#### 2.1 Run in Windows
```cmd
# one time
./mlb.exe -c config.json -f json
./mlb.exe -c config.toml -f toml
./mlb.exe -c config.yml -f yaml
./mlb.exe -c config.yaml -f yaml

# cron job
./mlb.exe -c config.json -f json -d
./mlb.exe -c config.toml -f toml -d
./mlb.exe -c config.yml -f yaml -d
./mlb.exe -c config.yaml -f yaml -d
```
#### 2.2 Run in Linux/Darwin
```bash
# one time
mlb -c config.json -f json
mlb -c config.toml -f toml
mlb -c config.yml -f yaml
mlb -c config.yaml -f yaml

# cron job
mlb -c config.json -f json -d
mlb -c config.toml -f toml -d
mlb -c config.yml -f yaml -d
mlb -c config.yaml -f yaml -d
```

## Feature plans
### 1. Service
The service is about the `Service` in `Windows`, `Linux` and `MacOS`. With the `Service`, `mlb` can run in background and do the backup tasks automatically.

### 2. Notification
Aim to send message to IM software such as `Telegram`,`Bark`, `WXWorks`, `DingTalk` and so on.

## Contribution
If you have some great ideas, plz submit issue and let me know :D

Wecome to PR~

## Background
Why did I design this tool?
A few months before, the data in MongoDB Standalone is broken by the hard disk failure, so I lost my data and can't not backup. So if you want to keep your data safe, it's better to use MongoDB ReplicaSet or backup more often.

## Thanks
1. [github.com/BurntSushi/toml](https://github.com/BurntSushi/toml) MIT Licence
2. [github.com/alexflint/go-arg](https://github.com/alexflint/go-arg) BSD-2-Clause License
3. [github.com/asaskevich/govalidator](https://github.com/asaskevich/govalidator) MIT Licence
4. [github.com/commander-cli/cmd](https://github.com/commander-cli/cmd) MIT Licence
5. [github.com/go-co-op/gocron](https://github.com/go-co-op/gocron) MIT Licence
6. [github.com/go-ozzo/ozzo-validation/v4](https://github.com/go-ozzo/ozzo-validation) MIT Licence
7. [github.com/gorhill/cronexpr](https://github.com/gorhill/cronexpr) GPL v3/APL v2
8. [github.com/sirupsen/logrus](https://github.com/sirupsen/logrus) MIT Licence
9. [github.com/valyala/fasttemplate](https://github.com/valyala/fasttemplate) MIT Licence


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fcatfishlty%2Fmongodb-local-backup.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fcatfishlty%2Fmongodb-local-backup?ref=badge_large)