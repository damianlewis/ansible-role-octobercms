# Ansible Role: October CMS
Role for installing and configuring October CMS.

## Requirements
None.

## Role Variables
Available variables are listed below, along with their default values.

```yaml
octobercms_deploy: no
octobercms_deploy_repo: ''
octobercms_deploy_version: master
octobercms_deploy_depth: 0
octobercms_deploy_path: /var/www/octobercms
octobercms_deploy_deployment_key_path: ~/.ssh/id_octobercms_deployment
```
Deploying an existing October CMS application from a Git repository.
- `octobercms_deploy:boolean` - Set this to true and both `octobercms_build_from_installer` and `octobercms_build_from_composer` to false to clone from a Git repository.
- `octobercms_deploy_repo:string` - Specifies the URL of the repository.
- `octobercms_deploy_version:string` - Specifies the version to install. Can be a branch or tag name.
- `octobercms_deploy_depth:int` - Specifies the number of revisions to truncate the cloned repository. A value of `0` will download all revisions.
- `octobercms_deploy_path:string` - Specifies where the repository will be cloned to.
- `octobercms_deploy_deployment_key_path:string` - Specifies the path to the SSH Git deployment key. Required when working with private repositories.

```yaml
octobercms_build_from_installer: yes
octobercms_installer_path: "{{ octobercms_deploy_path }}"
```
Installing October using the native installer.
- `octobercms_build_from_installer:boolean` - Set this to true and `octobercms_build_from_composer` to false to install using the native installer.
- `octobercms_installer_path:string` - Specifies where October will be installed.

```yaml
octobercms_build_from_composer: no
octobercms_composer_project_path: "{{ octobercms_deploy_path }}"
octobercms_composer_install: no
octobercms_composer_no_dev: yes
```
Installing October using the Composer.
- `octobercms_build_from_composer:boolean` - Set this to true and `octobercms_build_from_installer` to false to install using Composer.
- `octobercms_composer_project_path:string` - Specifies where October will be installed.
- `octobercms_composer_install:boolean` - Specifies whether `composer install` should be run after October has been installed.
- `octobercms_composer_no_dev:boolean` - Specifies whether the installation of required dev packages should be disabled.

```yaml
octobercms_root_path: "{{ octobercms_deploy_path }}"
octobercms_owner: "{{ ansible_ssh_user }}"
```
Configuration settings.
- `octobercms_root_path:string` - Specifies where October will be installed.
- `octobercms_owner:string` - Specifies the user that will have ownership of the October installation.

```yaml
octobercms_app_name: October CMS
octobercms_app_url: http://localhost
octobercms_app_key: ''
octobercms_app_debug: no
```
Optional settings for configuring the application.
- `octobercms_app_name:string` - Specifies the name for the application.
- `octobercms_app_url:string` - Specifies the base URL used by the application.
- `octobercms_app_key:string` - Specifies the encryption key the application should use.
- `octobercms_app_debug:boolean` - Specifies whether debug mode is enabled.

```yaml
octobercms_cms_edge_updates: no
octobercms_cms_disable_core_updates: "{{ octobercms_build_from_composer | default(no) }}"
octobercms_cms_backend_uri: backend
octobercms_cms_backend_timezone: UTC
octobercms_cms_enable_routes_cache: yes
octobercms_cms_enable_assets_cache: yes
octobercms_cms_database_templates: no
octobercms_cms_enable_csrf: yes
```
Optional settings for configuring October.
- `octobercms_cms_edge_updates:boolean` - Set this to true to download and use development copies of the core files and plugins.
- `octobercms_cms_disable_core_updates:boolean` - Set this to true to disable core updates from being delivered by the October gateway.
- `octobercms_cms_backend_uri:string` - Specifies the URL name used for accessing backend pages.
- `octobercms_cms_backend_timezone:string` - Specifies the default setting for the backend user's timezone.
- `octobercms_cms_enable_routes_cache:boolean` - Specifies if route caching is enabled. Recommended to disable during development, and enable for production mode.
- `octobercms_cms_enable_assets_cache:boolean` - Specifies if asset caching is enabled. Recommended to disable during development, and enable for production mode.
- `octobercms_cms_database_templates:boolean` - Specifies whether the theme templates are stored in the database instead of the filesystem.
- `octobercms_cms_enable_csrf:boolean` - Specifies whether CSRF protection is enabled.

```yaml
octobercms_database_connection: mysql
octobercms_database_name: 'database' or MySQL, PostgreSQL and SQL Server / 'storage/database.sqlite' for SQLite
octobercms_database_prefix: ''
```
Settings for configuring a database for use with October.
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
octobercms_remove_demo: no
```
Additional October settings.
- `octobercms_use_dotenv_config:boolean` - Set this to true to convert base configuration to DotEnv file.
- `octobercms_remove_demo:boolean` - Set this to true to remove demo theme and plugin.

## Dependencies
None.

## Example Playbook
```yaml
- hosts: server
  become: yes

  vars:
    octobercms_owner: www-data
    octobercms_app_debug: no
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