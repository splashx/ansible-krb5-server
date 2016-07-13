Role Name
=========

This is a general Kerberos ansible role which installs and configure Kerberos KDC and Kerberos Admin Server and extra modules (PKINIT, OTP, SASL and LDAP support)

The templates are based on krbkdc 1.13 so if you're using a newer version of Kerberos and settings are missing, pull request.

If you wish to not install 

Requirements
------------

The role will install the requirements for SALS, OTP and PKINIT by default. 
If you're not using these modules, overwrite `krb5_pkg_modules` in the playbook. 

Role Variables
--------------

The variables have nomenclature `kr5_kdc_[tag]`, where `[tag]` is the bracketless value of tags in the official [MIT Kerberos documentation](http://web.mit.edu/kerberos/krb5-current/doc/admin/conf_files/kdc_conf.html)

Note empty defaults here means MIT Kerberos defaults will apply. Check the [documentation](http://web.mit.edu/kerberos/krb5-1.14/doc/admin/conf_files/kdc_conf.html#kdcdefaults) for MIT Kerberos defaults. 

* `krb5-kdc`: [default value: `true`]: install the MIT Kerberos Key Server (KDC)
* `krb5-ldap-plugin`: [default value: `true`]: install the MIT Kerberos key server (KDC) LDAP plugin
* `krb5-admin-server`: [default value: `true`]: install the MIT Kerberos Admin Server 
* `krb5-pkinit`: [default value: `true`]: install the PKINIT plugin for MIT Kerberos
* `krb5-otp`: [default value: `true`]: install the OTP plugin for MIT Kerberos
* `krb5-k5tls`: [default value: `false`]: install TLS plugin for MIT Kerberos
* `krb5-sals-support`: [default value: `true`]: install support for SALS with Kerberos

* `krb5kdc_kdcdefaults.`: maps to MIT Kerberos `[kdcdefaults]` tag (kdc.conf)  
  * `acl_file`: [default value: `""`]  
  * `database_module`: [default value: `""`] 
  * `database_name`: [default value: `""`] 
  * `default_principal_expiration`: [default value: `""`] 
  * `default_principal_flags`: [default value: `[""]`] 
  * `dict_file`: [default value: `""`] 
  * `host_based_services`: [default value: `[""]`] 
  * `iprop_enable`: [default value: `""`] 
  * `iprop_master_ulogsize`: [default value: `""`] 
  * `iprop_slave_poll`: [default value: `""`] 
  * `iprop_port`: [default value: `""`]
  * `iprop_resync_timeout`: [default value: `""`]
  * `iprop_logfile`: [default value: `""`]
  * `kadmind_port`: [default value: `""`]
  * `key_stash_file`: [default value: `""`]
  * `kdc_max_dgram_reply_size`: [default value: `""`]
  * `kdc_ports`: [default value: `number[]`: 
  * `kdc_tcp_ports`: [default value: `number[]`: 
  * `master_key_name`: [default value: `""`]
  * **`master_key_type`: [default value: `"aes256-cts-hmac-sha1-96"`]** 
  * `max_life`: [default value: `""`]
  * `max_renewable_life`: [default value: `""`]
  * `no_host_referral`: [default value: `""`]
  * **`des_crc_session_supported`: [default value: `false`]** 
  * `reject_bad_transit`: [default value: `""`]
  * **`restrict_anonymous_to_tgt`: [default value: `true`]** 
  * **`supported_enctypes`: [default value: `["aes256-cts-hmac-sha1-96", "normal camellia256-cts-cmac", "normal aes128-cts-hmac-sha1-96", "normal camellia128-cts-cmac", "normal" ]`]** 


* `krb5kdc_realms.` (dictionary): maps to MIT Kerberos `[realms]` tag (kdc.conf)
  * `{n}`. - supports multiple realms
    * **`name` (required) [default value: `"REALM.COM"`]**: A REALM name. 
    * `acl_file`: [default value: `""`]  
    * `database_module`: [default value: `""`]
    * `database_name`: [default value: `""`]
    * `default_principal_flags`: [default value: `[""]`]
    * `dict_file`: [default value: `""`]
    * `host_based_services`: [default value: `[""]`]
    * `iprop_enable`: [default value: `""`]
    * `iprop_master_ulogsize`: [default value: `""`]
    * `iprop_slave_poll`: [default value: `""`]
    * `iprop_port`: [default value: `""`]
    * `iprop_resync_timeout`: [default value: `""`]
    * `iprop_logfile`: [default value: `""`]
    * `kadmind_port`: [default value: `""`]
    * `key_stash_file`: [default value: `""`]
    * `kdc_ports`: [default value: `[""]`]
    * `kdc_tcp_ports`: [default value: `[""]`]
    * `master_key_name`: [default value: `""`]
    * `master_key_type`: **[default value: `"aes256-cts-hmac-sha1-96"`]**
    * `max_life`: [default value: `""`]
    * `max_renewable_life`: [default value: `""`]
    * `no_host_referral`: [default value: `[""]`]
    * `des_crc_session_supported`: [default value: `""`]
    * `reject_bad_transit`: [default value: `""`]
    * **`restrict_anonymous_to_tgt`: [default value: `"true"`]**
    * `supported_enctypes`: [default value: `[""]`]
    * `pkinit_allow_upn`: [default value: `""`]
    * `pkinit_anchors`: [default value: `[""]`]
    * `pkinit_dh_min_bits`: [default value: `""`]
    * `pkinit_eku_checking`: [default value: `""`]
    * `pkinit_identity`: [default value: `""`]
    * `pkinit_kdc_ocsp`: [default value: `""`]
    * `pkinit_pool`: [default value: `""`]
    * `pkinit_require_crl_checking`: [default value: `""`]
    * `pkinit_revoke`: [default value: `""`]


* `krb5kdc_dbdefaults.`: maps to MIT Kerberos `[dbdefaults]` tag (kdc.conf)  
  * `ldap_kerberos_container_dn`: [default value: `""`]
  * `ldap_kdc_dn`: [default value: `""`]
  * `ldap_kdc_sasl_authcid`: [default value: `""`]
  * `ldap_kdc_sasl_authzid`: [default value: `""`]
  * `ldap_kdc_sasl_mech`: [default value: `""`]
  * `ldap_kdc_sasl_realm`: [default value: `""`]
  * `ldap_kadmind_dn`: [default value: `""`]
  * `ldap_kadmind_sasl_authcid`: [default value: `""`]
  * `ldap_kadmind_sasl_authzid`: [default value: `""`]
  * `ldap_kadmind_sasl_mech`: [default value: `""`]
  * `ldap_kadmind_sasl_realm`: [default value: `""`]
  * `ldap_service_password_file`: [default value: `""`]
  * `ldap_servers`: [default value: `""`]
  * `ldap_conns_per_server`: [default value: `""`]


  * `krb5kdc_dbmodules.` (dictionary): maps to MIT Kerberos `[dbmodules]` tag (kdc.conf)
    * `{n}`. - supports multiple dbmodules
      * **`name` (required) [default value: `"REALM.COM"`]**
      * `database_name`: [default value: `""`]
      * `db_library`: [default value: `""`]
      * `db_module_dir`: [default value: `""`]
      * `disable_last_success`: [default value: `""`]
      * `disable_lockout`: [default value: `""`]
      * `ldap_conns_per_server`: [default value: `""`]
      * `ldap_kadmind_dn`: [default value: `""`]
      * `ldap_kadmind_sasl_authcid`: [default value: `""`]
      * `ldap_kadmind_sasl_authzid`: [default value: `""`]
      * `ldap_kadmind_sasl_mech`: [default value: `""`]
      * `ldap_kadmind_sasl_realm`: [default value: `""`]
      * `ldap_kdc_dn`: [default value: `""`]
      * `ldap_kdc_sasl_authcid`: [default value: `""`]
      * `ldap_kdc_sasl_authzid`: [default value: `""`]
      * `ldap_kdc_sasl_mech`: [default value: `""`]
      * `ldap_kdc_sasl_realm`: [default value: `""`]
      * `ldap_kerberos_container_dn`: [default value: `""`]
      * `ldap_servers`: [default value: `""`]
      * `ldap_service_password_file`: [default value: `""`]
      * `unlockiter`: [default value: `""`]


  * `krb5kdc_otp.` (dictionary): maps to MIT Kerberos `[otp]` tag (kdc.conf)
    * `{n}`. - supports multiple otp token types
      * `retries`: [default value: `""`]
      * `secret`: [default value: `""`]
      * `server`: [default value: `""`]
      * `strip_realm`: [default value: `""`]
      * `timeout`: [default value: `""`]

Dependencies
------------

none

Example Playbook
----------------

Note the usage of two realms (REALM.COM and REALM2.COM) and how REALM2.COM uses the database_module value "REALM.COM". The realm "REALM.COM" doesn't require explicit value for database_value because the MIT kerberos defaults the value to the realm name. 
```
- hosts: kdc-slave
  become: yes
  vars:
    krb5kdc_kdcdefaults:
      - kdc_max_dgram_reply_size: 4096
        default_principal_flags:
            - flags:
                - "+proxy"
                - "+preauth"
                - "-renewable"
                - "+postdateable"
                - "+forwardable"
                - "+tgt-based"
                - "+proxiable"
                - "+dup-skey"
                - "+allow-tickets"
                - "+service"
        host_based_services:
            - services:
                - '*'
        kadmind_port: 749
        kdc_ports: 
            - number: 
                - 88
        kdc_tcp_ports: 
            - number: 
                - 88
        master_key_type: "aes256-cts-hmac-sha1-96"
        max_life: "24h"
        no_host_referral: 
            - hosts: 
                - hostA
                - hostnameB
        des_crc_session_supported: false
        restrict_anonymous_to_tgt: true
        supported_enctypes: 
            - types: 
                - "aes256-cts-hmac-sha1-96"
                - "normal camellia256-cts-cmac"
                - "normal aes128-cts-hmac-sha1-96"
                - "normal camellia128-cts-cmac"
                - "normal"

    krb5kdc_dbdefaults:
      - ldap_kerberos_container_dn: "cn=krbContainer,dc=example,dc=com"

    krb5kdc_dbmodules:
      - name: "REALM.COM"
        db_library: "kldap"
        ldap_kdc_dn: "cn=admin,dc=example,dc=com"
        ldap_kadmind_dn: "cn=admin,dc=example,dc=com"
        ldap_service_password_file: /etc/krb5kdc/service.keyfile
        ldap_servers:
          - hostname:
              - "ldaps://ldap01.example.com"
              - "ldaps://ldap02.example.com"
        ldap_conns_per_server: 5

    krb5kdc_realms:
    - name: "REALM.COM"
      database_name: "/var/lib/krb5kdc/principal"
      admin_keytab: "FILE:/etc/krb5kdc/kadm5.keytab"
      acl_file: "/etc/krb5kdc/kadm5.acl"
      key_stash_file: "/etc/krb5kdc/stash"
      kdc_ports:
          - number:
              - 88
      kdc_tcp_ports:
          - number:
              - 88
      master_key_type: "aes256-cts-hmac-sha1-96"
      restrict_anonymous_to_tgt: true

      - name: "REALM2.COM"
        database_name: "/var/lib/krb5kdc/principal"
        admin_keytab: "FILE:/etc/krb5kdc/kadm5.keytab"
        acl_file: "/etc/krb5kdc/kadm5.acl"
        key_stash_file: "/etc/krb5kdc/stash"
        kdc_ports:
            - number:
                - 88
        kdc_tcp_ports:
            - number:
                - 88
        default_principal_flags:
            - flags:
                - '-proxy'
                - "+preauth"
                - "-renewable"
                - "+postdateable"
                - "+forwardable"
                - "+tgt-based"
                - "+proxiable"
                - "+dup-skey"
                - "+allow-tickets"
                - "+service"   
        max_life: "10h 0m 0s"
        database_module: "REALM.COM"
        max_renewable_life: "7d 0h 0m 0s"
        master_key_type: "aes256-cts-hmac-sha1-96"
        restrict_anonymous_to_tgt: true
        pkinit_identity: "PKCS11:/usr/local/lib/libetpkcs11.so"
        pkinit_anchors: 
            - location:
              - "FILE:/etc/ssl/certs/ca-certificates.crt"

    krb5kdc_otp:
        - name: "DEFAULT"
          server: "10.10.10.200:1812"
          secret: /etc/krb5kdc/radius.secret
          strip_realm: true
          timeout: 5

  roles:
      - { role:  ansible-krb5-kdc, tags: ["ansible-krb5-kdc "] }
```

License
-------

BSD

Author Information
------------------

Diogenes Santos de Jesus