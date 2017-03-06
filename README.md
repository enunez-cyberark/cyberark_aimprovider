cyberark_aimprovider
====================

Role to install/uninstall CyberArk's AIM Credential Provider.

Requirements
------------

- CyberArk Privileged Account Security Web Services SDK.
- If modules not accesible from Ansible core, please use enunez-cyberark.cyberark_modules from galaxy.

Role Variables
--------------
```
# CyberArk's Privileged Account Security Web Services SDK api base URL
rest_api_url: ""

# Whether to validate certificates for REST api calls
validate_certs: true

# Zip file with distribution of AIM Provider
zip_file_name: ""

# Folder name within the ZIP file that will be used by default is taken from zip file name.
folder_name: '{{zip_file_name.split("/")[-1].split("-Rls")[0]}}'

# CyberArk location for App Provider user to be created
app_provider_user_location: "\\Applications"

# CyberArk Vault Address
vault_address: ""

# Whether to use shared logon authentication
use_shared_logon_authentication: false

# State
state: "present"
```

Dependencies
------------

None.


Example Playbook
----------------

**Note**: 
- As the role will include the galaxy user, you can create a symbolic link as follows:
```
ln -s /etc/ansible/roles/enunez-cyberark.cyberark_aimprovider cyberark_aimprovider
```
- If using cyberark_modules, make sure to uncomment the lines in the provide test/example playbooks

1) Install CyberArk AIM Provider.

```
---
- hosts: all

  roles:

    #- role: cyberark_modules # Include cyberark_modules if needed

    - role: cyberark_aimprovider
      api_base_url: "https://components.cyberark.local"
      validate_certs: false
      zip_file_name: "/tmp/binaries/RHELinux x64-Rls-v9.8.zip"
      vault_address: "10.0.1.10"
      use_shared_logon_authentication: true
```

2) Uninstall CyberArk AIM Provider.
```
---
- hosts: all

  roles:

    #- role: cyberark_modules # Include cyberark_modules if needed

    - role: cyberark_aimprovider
      api_base_url: "https://components.cyberark.local"
      use_shared_logon_authentication: true
      state: "absent"
      validate_certs: false
```

License
-------

MIT

Author Information
------------------

- Edward Nunez (edward.nunez@cyberark.com)
