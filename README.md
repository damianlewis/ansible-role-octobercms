# Ansible Role: OctoberCMS
Role for installing and configuring OctoberCMS.

## Requirements
None.

## Role Variables
Available variables are listed below, along with their default values.

```yaml
octobercms_build_from_installer: yes
octobercms_build_from_composer: no
octobercms_root_path: /var/www/octobercms/web
octobercms_owner: "{{ ansible_ssh_user }}"
```
Installation settings.
- `octobercms_build_from_installer:boolean` - Set this to true and `octobercms_build_from_composer` to false to install OctoberCMS using the native installer.
- `octobercms_build_from_composer:boolean` - Set this to true and `octobercms_build_from_installer` to false to install OctoberCMS using Composer.
- `octobercms_root_path:string` - Specifies where OctoberCMS will be installed.
- `octobercms_owner:string` - Specifies the user that will have ownership of the OctoberCMS installation.

```yaml
octobercms_app_name: October CMS
octobercms_app_debug: no
octobercms_app_url: http://localhost
```
Optional settings for configuring the application.
- `octobercms_app_name:string` - Specifies the name for the application.
- `octobercms_app_debug:boolean` - Specifies whether debug mode is enabled.
- `octobercms_app_url:string` - Specifies the base URL used by the application.

```yaml
octobercms_database_connection: mysql
octobercms_database_name: 'database' or MySQL, PostgreSQL and SQL Server / 'storage/database.sqlite' for SQLite
octobercms_database_prefix: ''
```
Settings for configuring a database for use with OctoberCMS.
- `octobercms_database_connection:string` - Specifies which database connection to use. Possible options are `sqlite`, `mysql`, `pgsql` and `sqlsrv`.
- `octobercms_database_name:string` - Specifies the name of database.
- `octobercms_database_prefix:string` - Specifies a prefix which is added to the database table names.

```yaml
octobercms_database_host: localhost
octobercms_database_port: 3306 for MySQL / 5432 for PostgreSQL / 1433 for SQL Server
octobercms_database_user: root
octobercms_database_password: ''
```
Additional settings for configuring the database. (MySQL, PostgreSQL and SQL Server)
- `octobercms_database_host:string` - Specifies the host where the database is located.
- `octobercms_database_port:int` - Specifies the port for accessing the database.
- `octobercms_database_user:string` - Specifies the database user.
- `octobercms_database_password:string` - Specifies the database user password.

```yaml
octobercms_database_charset: 'utf8mb4' for MySQL / 'utf8' for PostgreSQL
```
Additional settings for configuring the database. (MySQL, PostgreSQL)
- `octobercms_database_charset:string` - Specifies the character set for the database.

```yaml
octobercms_database_collation: utf8mb4_unicode_ci
```
Additional settings for configuring the database. (MySQL)
- `octobercms_database_collation:string` - Specifies the collation used for the database.

```yaml
octobercms_database_schema: public
```
Additional settings for configuring the database. (PostgreSQL)
- `octobercms_database_schema:string` - Specifies the schema used for the database.

```yaml
octobercms_use_dotenv_config: no
```
Converting to DotEnv configuration.
- `octobercms_use_dotenv_config:boolean` - Set this to true to make use of a DotEnv file for configuration.

## Dependencies
None.

## Example Playbook
```yaml
- hosts: server
  become: yes

  vars:
    octobercms_owner: www-data
    octobercms_app_debug: 'false'
    octobercms_app_url: https://example.com
    octobercms_database_name: octobercms
    octobercms_database_user: octobercms_user
    octobercms_database_password: secret

  tasks:
  - import_role:
      name: damianlewis.octobercms
```

## License
MIT

## Author
Damian Lewis