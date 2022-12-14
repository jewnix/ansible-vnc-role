# Role Name
Simple role to configures a VNC server for multiple users.

## Requirements
This role was only tested on CentOS 8 Stream, and ansible vbersion 2.12.10.

### Role Variables
`vnc_users`: A list of users, displays and password for each user. Variable under this var are as follows
`user`: The user name which will be used to configure the settings for that user.
`display_id`: The X window for that user
`vnc_password`: The password to add using the `vncpasswd` for that user.
`vnc_ports`: List of ports to open in `firewalld` to allow access to the VNC users. The ports will usually be `5901` for the user using display `:1`, and so on.
`enable_firewalld`: You can set this to `False` if you don't want the playbook to make changes to `firewalld`. Defalts to `True`.
`firewalld_zone`: The firewalld zone to add the ports to.
You can find an example of these variable in this repo.
`additional_packages`: A list of additional packages to install. 
`install_utilities`: This will install the packages listed in the `additional_packages`.
`install_chrome`: Add the google chrome repo and installs chrome.

### Tasks
This role includes various tasks.
`configure_os.yml`: Here are some OS configuratios that make the VNC experience a bit better.
`configure_firewall.yml`: This configures firewalld to allow to open ports when `enable_firewalld` is set to `True`.
`install_packages.yml`: This installs some essential packages. You can add a list of packages you want to install in `host_vars` or `group_vars`. The default list can be found in `vars/main.yml`.
`configure_vnc.yml`: This configures the users and passwords for the VNC users, and enables the services.
