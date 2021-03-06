# Reference
<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

**Classes**

* [`vsftpd`](#vsftpd): This class configures a vsftpd server.  It ensures that the appropriate files are in the appropriate places and synchronizes the external mat
* [`vsftpd::config`](#vsftpdconfig): This class provides a method for setting up the main body of /etc/vsftpd/vsftpd.conf.  * The rest of the parameters can be found on the vsftp
* [`vsftpd::config::firewall`](#vsftpdconfigfirewall): This class sets up the appropriate IPtables rules based on the value of $fw_rules.  By default, it will allow access only to localhost, you w
* [`vsftpd::config::tcpwrappers`](#vsftpdconfigtcpwrappers): Sets up tcpwrappers for vsfptd.
* [`vsftpd::install`](#vsftpdinstall): Installs vsftpd and optionally manages the vsftpd group and user.
* [`vsftpd::service`](#vsftpdservice): Ensures the vsftpd service is running.
* [`vsftpd::users`](#vsftpdusers): Manages the vsftpd group and user.

## Classes

### vsftpd

This class configures a vsftpd server.  It ensures that the appropriate
files are in the appropriate places and synchronizes the external
materials.

One thing to note is that local users are forced to SSL for security
reasons.

#### Parameters

The following parameters are available in the `vsftpd` class.

##### `trusted_nets`

Data type: `Simplib::Netlist`

A whitelist of subnets (in CIDR notation) permitted access.

Default value: simplib::lookup('simp_options::trusted_nets', { 'default_value' => ['127.0.0.1','::1'] })

##### `firewall`

Data type: `Boolean`

If true, use SIMP's ::iptables to manage firewall rules to accommodate <%= metadata.name %>.

Default value: simplib::lookup('simp_options::firewall', { 'default_value' => false })

##### `pki`

Data type: `Variant[Enum['simp'],Boolean]`

* If 'simp', include SIMP's pki module and use pki::copy to manage
  application certs in /etc/pki/simp_apps/vsftpd/x509
* If true, do *not* include SIMP's pki module, but still use pki::copy
  to manage certs in /etc/pki/simp_apps/vsftpd/x509
* If false, do not include SIMP's pki module and do not use pki::copy
  to manage certs.  You will need to appropriately assign a subset of:
  * app_pki_dir
  * app_pki_key
  * app_pki_cert
  * app_pki_ca
  * app_pki_ca_dir

Default value: simplib::lookup('simp_options::pki', { 'default_value' => false })

##### `tcpwrappers`

Data type: `Boolean`

If true, use SIMP's ::tcpwrappers to configure TCP Wrappers to
accommodate <%= metadata.name %> and set 'tcp_wrappers' value in
vsftpd.conf to true.

Default value: simplib::lookup('simp_options::tcpwrappers', { 'default_value' => false })

##### `haveged`

Data type: `Boolean`

If true, include ::haveged to assist with entropy generation.

Default value: simplib::lookup('simp_options::haveged', { 'default_value' => false })

##### `cipher_suite`

Data type: `Array[String]`

OpenSSL cipher suite to use.
If you are not using this with ::simp_options and the server is in FIPS
mode, you need to set this to a FIPS-compliant cipher suite, (e.g.,
['FIPS', '!LOW']).
Corresponds to ssl_ciphers in vsftpd.conf.

Default value: simplib::lookup('simp_options::openssl::cipher_suite', { 'default_value' => ['DEFAULT','!MEDIUM'] })

##### `package_ensure`

Data type: `String`

The ensure status of the vsftpd package

Default value: simplib::lookup('simp_options::package_ensure', { 'default_value' => 'installed' })

##### `vsfptd_user`

Set the user for the vsftpd service.

##### `vsftpd_group`

Data type: `String`

Set the group for the vsftpd service and files.

Default value: 'ftp'

##### `manage_user`

Data type: `Boolean`

Manage vsftpd user.

Default value: `true`

##### `vsftpd_uid`

Data type: `Integer`

Integer.  UID of the vsftpd user.

Default value: 14

##### `vsftpd_gid`

Data type: `Integer`

Integer. GID of the vsftpd group.

Default value: 50

##### `manage_group`

Data type: `Boolean`

Manage vsftpd group.

Default value: `true`

##### `ftp_data_port`

Data type: `Simplib::Port`



Default value: 20

##### `listen_address`

Data type: `Optional[Simplib::IP::V4]`



Default value: `undef`

##### `listen_ipv4`

Data type: `Boolean`



Default value: `true`

##### `listen_port`

Data type: `Simplib::Port`



Default value: 21

##### `local_enable`

Data type: `Boolean`



Default value: `true`

##### `pasv_enable`

Data type: `Boolean`



Default value: `true`

##### `pasv_max_port`

Data type: `Optional[Simplib::Port]`



Default value: `undef`

##### `pasv_min_port`

Data type: `Optional[Simplib::Port]`



Default value: `undef`

##### `ssl_enable`

Data type: `Boolean`



Default value: `true`

##### `require_ssl_reuse`

Data type: `Boolean`



Default value: `true`

##### `userlist_deny`

Data type: `Boolean`



Default value: `true`

##### `userlist_enable`

Data type: `Boolean`



Default value: `true`

##### `user_list`

Data type: `Array[String]`



Default value: ['root','bin','daemon','adm','lp','sync','shutdown','halt','mail','news','uucp','operator','games','nobody']

##### `pam_service_name`

Data type: `String`



Default value: 'vsftpd'

##### `validate_cert`

Data type: `Boolean`



Default value: `true`

##### `vsftpd_user`

Data type: `String`



Default value: 'ftp'

### vsftpd::config

This class provides a method for setting up the main body of
/etc/vsftpd/vsftpd.conf.

* The rest of the parameters can be found on the vsftpd.conf man page *

#### Parameters

The following parameters are available in the `vsftpd::config` class.

##### `pki`

* If 'simp', include SIMP's pki module and use pki::copy to manage
  application certs in /etc/pki/simp_apps/vsftpd/x509
* If true, do *not* include SIMP's pki module, but still use pki::copy
  to manage certs in /etc/pki/simp_apps/vsftpd/x509
* If false, do not include SIMP's pki module and do not use pki::copy
  to manage certs.  You will need to appropriately assign a subset of:
  * app_pki_dir
  * app_pki_key
  * app_pki_cert
  * app_pki_ca
  * app_pki_ca_dir

##### `app_pki_external_source`

Data type: `String`

* If pki = 'simp' or true, this is the directory from which certs will be
  copied, via pki::copy.  Defaults to /etc/pki/simp/x509.

* If pki = false, this variable has no effect.

Default value: simplib::lookup('simp_options::pki::source', { 'default_value' => '/etc/pki/simp/x509' })

##### `app_pki_dir`

Data type: `Stdlib::Absolutepath`

This variable controls the basepath of $app_pki_key, $app_pki_cert,
$app_pki_ca, $app_pki_ca_dir, and $app_pki_crl.
It defaults to /etc/pki/simp_apps/vsftpd/pki.

Default value: '/etc/pki/simp_apps/vsftpd/x509'

##### `app_pki_key`

Data type: `Stdlib::Absolutepath`

Path and name of the private SSL key file

Default value: "${app_pki_dir}/private/${::fqdn}.pem"

##### `app_pki_cert`

Data type: `Stdlib::Absolutepath`

Path and name of the public SSL certificate

Default value: "${app_pki_dir}/public/${::fqdn}.pub"

##### `app_pki_ca`

Data type: `Stdlib::Absolutepath`

Path and name of the CA.

Default value: "${app_pki_dir}/cacerts/cacerts.pem"

##### `allow_anon_ssl`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `anon_mkdir_write_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `anon_other_write_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `anon_upload_enable`

Data type: `Boolean`



Default value: `true`

##### `anon_world_readable_only`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `anonymous_enable`

Data type: `Boolean`



Default value: `true`

##### `ascii_download_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `ascii_upload_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `async_abor_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `background`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `check_shell`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `chmod_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `chown_uploads`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `chroot_list_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `chroot_local_user`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `connect_from_port_20`

Data type: `Boolean`



Default value: `true`

##### `deny_email_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `dirlist_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `dirmessage_enable`

Data type: `Boolean`



Default value: `true`

##### `download_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `dual_log_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `force_dot_files`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `force_anon_data_ssl`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `force_anon_logins_ssl`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `force_local_data_ssl`

Data type: `Boolean`



Default value: `true`

##### `force_local_logins_ssl`

Data type: `Boolean`



Default value: `true`

##### `guest_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `hide_ids`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `listen_ipv6`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `lock_upload_files`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `log_ftp_protocol`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `ls_recurse_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `mdtm_write`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `no_anon_password`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `no_log_lock`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `one_process_model`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `passwd_chroot_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `pasv_addr_resolve`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `pasv_promiscuous`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `port_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `port_promiscuous`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `reverse_lookup_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `run_as_launching_user`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `secure_email_list_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `session_support`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `setproctitle_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `ssl_sslv2`

Data type: `Boolean`



Default value: `false`

##### `ssl_sslv3`

Data type: `Boolean`



Default value: `false`

##### `ssl_tlsv1`

Data type: `Boolean`



Default value: `false`

##### `ssl_tlsv1_1`

Data type: `Boolean`



Default value: `false`

##### `ssl_tlsv1_2`

Data type: `Boolean`



Default value: `true`

##### `syslog_enable`

Data type: `Boolean`



Default value: `true`

##### `text_userdb_names`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `tilde_user_enable`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `use_localtime`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `use_sendfile`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `userlist_file`

Data type: `Stdlib::Absolutepath`



Default value: '/etc/vsftpd/user_list'

##### `userlist_log`

Data type: `Boolean`



Default value: `true`

##### `virtual_use_local_privs`

Data type: `Optional[Boolean]`



Default value: `undef`

##### `write_enable`

Data type: `Boolean`



Default value: `true`

##### `xferlog_enable`

Data type: `Boolean`



Default value: `true`

##### `xferlog_std_format`

Data type: `Boolean`



Default value: `true`

##### `accept_timeout`

Data type: `Optional[Integer]`



Default value: `undef`

##### `anon_max_rate`

Data type: `Optional[Integer]`



Default value: `undef`

##### `anon_umask`

Data type: `Optional[Simplib::Umask]`



Default value: `undef`

##### `connect_timeout`

Data type: `Optional[Integer]`



Default value: `undef`

##### `data_connection_timeout`

Data type: `Optional[Integer]`



Default value: `undef`

##### `delay_failed_login`

Data type: `Optional[Integer]`



Default value: `undef`

##### `delay_successful_login`

Data type: `Optional[Integer]`



Default value: `undef`

##### `file_open_mode`

Data type: `Optional[Simplib::Umask]`



Default value: `undef`

##### `idle_session_timeout`

Data type: `Optional[Integer]`



Default value: `undef`

##### `local_max_rate`

Data type: `Optional[Integer]`



Default value: `undef`

##### `local_umask`

Data type: `Simplib::Umask`



Default value: '022'

##### `max_clients`

Data type: `Optional[Integer]`



Default value: `undef`

##### `max_login_fails`

Data type: `Optional[Integer]`



Default value: `undef`

##### `max_per_ip`

Data type: `Optional[Integer]`



Default value: `undef`

##### `trans_chunk_size`

Data type: `Optional[Integer]`



Default value: `undef`

##### `anon_root`

Data type: `Optional[String]`



Default value: `undef`

##### `banned_email_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `banner_file`

Data type: `Stdlib::Absolutepath`



Default value: '/etc/issue.net'

##### `chown_username`

Data type: `Optional[String]`



Default value: `undef`

##### `chroot_list_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `cmds_allowed`

Data type: `Optional[Array[String]]`



Default value: `undef`

##### `deny_file`

Data type: `Optional[String]`



Default value: `undef`

##### `dsa_cert_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `dsa_private_key_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `email_password_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `hide_file`

Data type: `Optional[String]`



Default value: `undef`

##### `listen_address6`

Data type: `Optional[Simplib::IP::V6]`



Default value: `undef`

##### `local_root`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `message_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `nopriv_user`

Data type: `Optional[String]`



Default value: `undef`

##### `pasv_address`

Data type: `Optional[Simplib::Host]`



Default value: `undef`

##### `validate_cert`

Data type: `Boolean`



Default value: $::vsftpd::validate_cert

##### `secure_chroot_dir`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `user_config_dir`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `user_sub_token`

Data type: `Optional[String]`



Default value: `undef`

##### `vsftpd_log_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `xferlog_file`

Data type: `Optional[Stdlib::Absolutepath]`



Default value: `undef`

##### `min_uid`

Data type: `String`



Default value: '500'

### vsftpd::config::firewall

This class sets up the appropriate IPtables rules based on the value of
$fw_rules.

By default, it will allow access only to localhost, you will need to
define an array at fw_rules to add additional hosts.

Localhost is always listed as a host that is allowed to access the system.

### vsftpd::config::tcpwrappers

Sets up tcpwrappers for vsfptd.

### vsftpd::install

Installs vsftpd and optionally manages the vsftpd group
and user.

### vsftpd::service

Ensures the vsftpd service is running.

### vsftpd::users

Manages the vsftpd group and user.

