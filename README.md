# PHP 5.5 SCL

An Ansible role to install PHP 5.5 from the Software Collections Library.

## Requirements

This role is designed to install PHP 5.5 from the SCL. It could be used to install and configure the default PHP version too, however it hasn't been developed / tested
for that. As it's developed for SCL it will only support RHEL family operating systems

## Role Variables

### `php55_scl_install_scl_repo`

Should this role install the Software Collections Library repo? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`


### `php55_scl_scl_utils_packages`

List of packages to install for SCL utils

The packages will only be installed if `php55_scl_install_scl_repo` is set to `yes`|`true`

Default value:
```
  - scl-utils
```

### `php55_scl_scl_repo_url`

Full URL of the RPM to install if `php55_scl_install_scl_repo` is set to `yes`|`true`

Default value: `"https://www.softwarecollections.org/en/scls/rhscl/php55/epel-{{ ansible_distribution_major_version }}-{{ ansible_architecture }}/download/rhscl-php55-epel-{{ ansible_distribution_major_version }}-{{ ansible_architecture }}.noarch.rpm"`

### `php55_scl_install_php`

Should this role install the PHP packages? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`


### `php55_scl_php_packages`

List of packages this role should install

Packages are only installed if `php55_scl_install_php` is set to `yes`|`true`

Default value:
```
  - php55
  - php55-php-cli
```

### `php55_scl_configure`

Should this role manage the configuration of PHP? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`


### `php55_scl_timezone`

Timezone to set in the php.ini file

Default value: `UTC`

### `php55_scl_configure_options`
      
List of configuration files and options to insert

Will only be added if `php55_scl_configure is `yes`|`true`

```
- file: /absolute/file/path.ini
  values:
    - { section: ini_section, key: config_key, value: config_value }
    - { section: ini_section, key: config_key2, value: another_value }
- file: /another/config/file.ini
  values:
    - { section: ini_section, key: config_key, value: value }
```

Default value:
```
  - file: /opt/rh/php55/root/etc/php.ini
    values:
      - { section: date, key: date.timezone, value: "{{ php55_scl_timezone }}" }
```

### `php55_scl_backup_ini_files`

Should the role create a backup of the ini files before overwriting? Valid values are `yes`, `true`, `no` or `false`

Default value: `yes`

### `php55_scl_enable_globally`

Should we enable PHP 5.5 for all users? Valid values are `yes`, `true`, `no` or `false`

Default value: `no`

### `php55_scl_profile_d_directory`

Absolute path to the profile.d directory.

This is used to add a script that will enable PHP 5.5 for all users if `php55_scl_enable_globally` is `yes`|`true`

Default value: `/etc/profile.d`

## Dependencies

The role itself does not have any dependencies, however, you cannot run PHP 5.5 from SCL in any Apache other than the 2.4 version from SCL. Luckily I created a
role for that too - [https://galaxy.ansible.com/detail#/role/6261](https://galaxy.ansible.com/detail#/role/6261)

Even though CentOS 7 ships with Apache 2.4, you must use the SCL version with the SCL version on PHP 5.5 (CentOS 7 still only ships PHP 5.4 by default)

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: unfinisheddev.php-55-scl }

## License
-------

MIT

## Author Information

Role created by [Dave Kirk](http://unfinisheddev.com)