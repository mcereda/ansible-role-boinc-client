# Boinc client

FIXME

The role has been validated on vagrant boxes.

## Requirements

None.

## Role Variables

Variable name                       | Type    | Default value                                   | Description
------------------------------------|---------|-------------------------------------------------|------------
add_ansible_user_to_boinc_users     | boolean | false                                           | wether to add the current ansible user to the `boinc` group
boinc_config_dir                    | string  | the os family's default configuration directory | usually the same as `boinc_data_dir` unless the system has it differently (e.g. debian)
boinc_data_dir                      | string  | the system's default data directory             | see [BOINC Data directory]
boinc_enable_opencl_integration     | boolean | false                                           | wether to enable opencl integrations
boinc_enable_virtualbox_integration | boolean | false                                           | wether to enable virtualbox integrations
boinc_groups                        | list    | zero or more of ['render','video','virtualbox'] | additional groups the `boinc` user is member of
boinc_set_files_group_writable      | boolean | false                                           | wether to set all files writable to boinc users
boinc_headless                      | boolean | false                                           | wether to install the manager and other gui utilities
boinc_allow_remote_gui_rpc          | boolean | false                                           | wether to allow remote gui rpc connections
boinc_gui_rpc_auth_password         | string  | ansible-generated password                      | the password to use to connect to the client
boinc_remote_hosts                  | list    | []                                              | the list of hosts for which remote gui rpc is allowed; only fqdns or ip addresses work here
boinc_apt_install_recommends        | boolean | same as `boinc_headless`                        | on apt-based systems, wether to install recommended packages

## Dependencies

None.

## Example Playbook

FIXME

## License

MIT

## Sources

- [Installing BOINC]
- [BOINC][arch wiki boinc] page on the [Arch Wiki]
- [BOINC Data directory]

[arch wiki]: https://wiki.archlinux.org

[arch wiki boinc]: https://wiki.archlinux.org/?title=BOINC
[boinc data directory]: https://boinc.berkeley.edu/wiki/BOINC_Data_directory
[installing boinc]: https://boinc.berkeley.edu/wiki/Installing_BOINC
