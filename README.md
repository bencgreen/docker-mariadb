# Docker MariaDB

![build](https://github.com/bencgreen/docker-mariadb/workflows/build/badge.svg)

[Docker Repository](https://hub.docker.com/r/bcgdesign/mariadb)

I've been using [webhippie](https://github.com/dockhippie/mariadb)'s MariaDB image for a while, but I wanted to manage backups in a different way, and use the latest version of [MariaDB](https://mariadb.org/).

So this was originally a fork of that, with a different backup script to store backups by date rather than index.  However it is now substantially different, using my own [Alpine](https://hub.docker.com/r/bcgdesign/alpine-s6) base image, with a clean install of the [S6 Overlay](https://github.com/just-containers/s6-overlay).

## Backups

Backups are stored:

* in the `/var/lib/backup` volume
* in subfolders by date and time (yyMMddhhmm)
* every eight hours

The following environment variables are available for the backups:

```bash
BACKUP_COMPRESS_FILES = 0 # Set to '1' to gzip the SQL backup files
BACKUP_KEEP_FOR_DAYS = 14 # Backups will be kept for this many days
```

## Volumes

* /etc/mysql/conf.d
* /var/lib/mysql
* /var/lib/backup

## Ports

* 3306

## MariaDB Environment Variables

```bash
# Required
MARIADB_ROOT_PASSWORD =
```

```bash
# Recommended - to create your own database and user automatically
MARIADB_DATABASE =
MARIADB_USERNAME =
MARIADB_PASSWORD =
```

```bash
# Defaults
MARIADB_BINLOG_FORMAT = mixed
MARIADB_CHARACTER_SET_SERVER = utf8
MARIADB_COLLATION_SERVER = utf8_general_ci
MARIADB_DEFAULT_CHARACTER_SET = utf8
MARIADB_EXPIRE_LOGS_DAYS = 28 # Set to 0 so logs never expire
MARIADB_INNODB_BUFFER_POOL_SIZE = 16M
MARIADB_INNODB_DATA_FILE_PATH = ibdata1:10M:autoextend
MARIADB_INNODB_FLUSH_LOG_AT_TRX_COMMIT = 1
MARIADB_INNODB_LOCK_WAIT_TIMEOUT = 50
MARIADB_INNODB_LOG_BUFFER_SIZE = 8M
MARIADB_INNODB_LOG_FILE_SIZE = 5M
MARIADB_INNODB_USE_NATIVE_AIO = 1
MARIADB_KEY_BUFFER_SIZE = 16M
MARIADB_KEY_BUFFER_SIZE = 20M
MARIADB_LOG_BIN = mysql-bin # Set to 0 to disable binary logging
MARIADB_MAX_ALLOWED_PACKET = 16M
MARIADB_MAX_ALLOWED_PACKET = 1M
MARIADB_MAX_CONNECTIONS = 151
MARIADB_MYISAM_SORT_BUFFER_SIZE = 8M
MARIADB_NET_BUFFER_SIZE = 8K
MARIADB_READ_BUFFER = 2M
MARIADB_READ_BUFFER_SIZE = 256K
MARIADB_READ_RND_BUFFER_SIZE = 512K
MARIADB_SERVER_ID = 1
MARIADB_SORT_BUFFER_SIZE = 20M
MARIADB_SORT_BUFFER_SIZE = 512K
MARIADB_TABLE_OPEN_CACHE = 64
MARIADB_WRITE_BUFFER = 2M
```

## Authors

* [Ben Green](https://github.com/bencgdreen)
* [Thomas Boerger](https://github.com/tboerger)

## License

> MIT

## Copyright

> Copyright (c) 2020 Ben Green <https://bcgdesign.com>  
> Unless otherwise stated
