login_defs
==========

Ansible role which helps to manage the `/etc/login.defs` file.

The configuration of the role is done in such way that it should not be necessary
to change the role for any kind of configuration. All can be done either by
changing role parameters or by declaring completely new configuration as a
variable. That makes this role absolutely universal. See the examples below for
more details.

Please report any issues or send PR.


Examples
--------

```
---

# Example of how to use it without any changes
- hosts: myhost
  roles:
    - login_defs

# Example of how to change the default configuration
- hosts: myhost
  vars:
    # Change the value of the PASS_MIN_DAYS parameter
    login_defs_config_pass_min_days: 7
  roles:
    - login_defs

# Example of how to add a custom configuration
- hosts: myhost
  vars:
    # Add parameter MAIL_FILE into the configuration
    login_defs_config__custom:
      mail_file: .mail
  roles:
    - login_defs

# Example of how to remove a parameter from the default configuration
- hosts: myhost
  vars:
    # Remove parameter PASS_MIN_LEN from the configuration
    login_defs_config_pass_min_len: null
  roles:
    - login_defs
```


Role variables
--------------

List of variables used by the role:

```
# Location of the login.defs file
login_defs_file: /etc/login.defs
# Owner/group/mode of the login.defs file
login_defs_owner: root
login_defs_group: root
login_defs_mode: 0644

# Default values of the default configuration
login_defs_config_mail_dir: /var/spool/mail
login_defs_config_pass_max_days: 99999
login_defs_config_pass_min_days: 0
login_defs_config_pass_min_len: 5
login_defs_config_pass_warn_age: 7
login_defs_config_uid_min: 500
login_defs_config_uid_max: 60000
login_defs_config_gid_min: 500
login_defs_config_gid_max: 60000
login_defs_config_create_home: "yes"
login_defs_config_umask: "077"
login_defs_config_usergroups_enab: "yes"
login_defs_config_encrypt_method: MD5
login_defs_config_md5_crypt_enab: "yes"

# Default configuration
login_defs_config__default:
  mail_dir: "{{ login_defs_config_mail_dir }}"
  pass_max_days: "{{ login_defs_config_pass_max_days }}"
  pass_min_days: "{{ login_defs_config_pass_min_days }}"
  pass_min_len: "{{ login_defs_config_pass_min_len }}"
  pass_warn_age: "{{ login_defs_config_pass_warn_age }}"
  uid_min: "{{ login_defs_config_uid_min }}"
  uid_max: "{{ login_defs_config_uid_max }}"
  gid_min: "{{ login_defs_config_gid_min }}"
  gid_max: "{{ login_defs_config_gid_max }}"
  create_home: "{{ login_defs_config_create_home }}"
  umask: "{{ login_defs_config_umask }}"
  usergroups_enab: "{{ login_defs_config_usergroups_enab }}"
  encrypt_method: "{{ login_defs_config_encrypt_method }}"
  md5_crypt_enab: "{{ login_defs_config_md5_crypt_enab }}"

# Custom configuration
login_defs_config__custom: {}

# Final cofiguration
login_defs_config: "{{
    login_defs_config__default.update(login_defs_config__custom)
  }}{{
    login_defs_config__default
  }}"
```


Dependencies
------------

- [`config_encoder_filters`](https://github.com/jtyr/ansible-config_encoder_filters)


License
-------

MIT


Author
------

Jiri Tyr
