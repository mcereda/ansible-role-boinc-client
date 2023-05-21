# Boinc client

Install and configure the BOINC client on a target host.

Installation is done using the `package` module for simplicity unless the target distribution required differently.<br />
`apt` and `pacman` require their cache to be built before a package can be installed, so their respective modules are used instead.

Only a couple of settings are available for the client's configuration; see the [role variables] for more information.

Users in the `boinc` group can usually read but not write files; use the `boinc_set_files_group_writable` variable to change this.

This role has **also** been validated on vagrant boxes.

## Requirements

None.

## Role Variables

Variable name                         | Type       | Default value                                             | Description
--------------------------------------|------------|-----------------------------------------------------------|------------
`boinc_acct_mgr_password`             | string     | null                                                      | the account manager's password
`boinc_acct_mgr_url`                  | url        | <http://bam.boincstats.com>                               | the account manager's URL
`boinc_acct_mgr_username`             | string     | null                                                      | the account manager's username
`boinc_add_user_to_the_boinc_group`   | boolean    | false                                                     | wether to add the current ansible user to the `boinc` group
`boinc_allow_remote_gui_rpc`          | boolean    | false                                                     | wether to allow remote gui rpc connections
`boinc_apt_install_recommends`        | boolean    | same as `boinc_headless`                                  | on apt-based systems, wether to install recommended packages
`boinc_attach_to_acct_mgr`            | boolean    | false                                                     | wether to start the client to an account manager
`boinc_config_dir_by_os_family`       | dictionary | see the [main variables]                                  | the default configuration directory, categorized by `ansible_os_family`
`boinc_config_dir`                    | string     | the (dynamic) os family's default configuration directory | usually the same as `boinc_data_dir` unless the system has it differently (e.g. debian)
`boinc_data_dir_by_system`            | dictionary | see the [main variables]                                  | the default data directory, categorized by `ansible_system`
`boinc_data_dir`                      | string     | the (dynamic) system's default data directory             | see [BOINC Data directory]
`boinc_enable_opencl_integration`     | boolean    | false                                                     | wether to enable opencl integrations; will **not** install drivers or other non-boinc packages
`boinc_enable_virtualbox_integration` | boolean    | false                                                     | wether to enable virtualbox integrations; will **not** install virtualbox or other non-boinc packages
`boinc_groups`                        | list       | zero or more of [`render`,`video`,`virtualbox`]           | additional groups the `boinc` user is member of
`boinc_gui_rpc_auth_password`         | string     | ansible-generated password                                | the password to use to connect to the client
`boinc_headless`                      | boolean    | false                                                     | wether to install the manager and other gui utilities
`boinc_packages_by_pkg_mgr`           | dictionary | see the [main variables]                                  | the (dynamic) list of packages to install for each package manager
`boinc_remote_hosts`                  | list       | []                                                        | the list of hosts for which remote gui rpc is allowed; only fqdns or ip addresses work here
`boinc_set_files_group_writable`      | boolean    | false                                                     | wether to set all files writable to boinc users
`boinc_start_at_boot`                 | boolean    | true                                                      | wether to start the client at boot

## Dependencies

None.

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: mcereda.ansible-role-boinc-client
      vars:
        boinc_allow_remote_gui_rpc: true
        boinc_remote_hosts:
          - faraday.lan
          - '192.168.1.157'
        boinc_gui_rpc_auth_password: 'horse battery staple'
        boinc_attach_to_acct_mgr: true
        boinc_acct_mgr_username: jbgood
        boinc_acct_mgr_password: delorean
```

## License

MIT

## Sources

- [Installing BOINC]
- [BOINC][arch wiki boinc] page on the [Arch Wiki]
- [BOINC Data directory]

[role variables]: #role-variables

[main variables]: vars/main.yml

[arch wiki]: https://wiki.archlinux.org

[arch wiki boinc]: https://wiki.archlinux.org/?title=BOINC
[boinc data directory]: https://boinc.berkeley.edu/wiki/BOINC_Data_directory
[installing boinc]: https://boinc.berkeley.edu/wiki/Installing_BOINC
