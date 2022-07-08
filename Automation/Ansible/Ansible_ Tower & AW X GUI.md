1. **Access**:
![fc054e1a0d9deec75b62b14cb0d8fd42.png](../../_resources/fc054e1a0d9deec75b62b14cb0d8fd42.png)

**Organisations:**
![d52a0e3995e0547b5018a787e5958793.png](../../_resources/d52a0e3995e0547b5018a787e5958793.png)

**USERS**
![310452676986a4c0a31b42e7ec212ed0.png](../../_resources/310452676986a4c0a31b42e7ec212ed0.png)

**TEAMS**
![ebbaf94cc9b578dd64b64c06d8395b24.png](../../_resources/ebbaf94cc9b578dd64b64c06d8395b24.png)

# Resources
![90f6cde5494e1216005fe6827f0580e2.png](../../_resources/90f6cde5494e1216005fe6827f0580e2.png)
**INVENTORIES**
![ce9c7635b3b57a2644863f7654582fdc.png](../../_resources/ce9c7635b3b57a2644863f7654582fdc.png)

![248aedd902285e70f34d7f6924309611.png](../../_resources/248aedd902285e70f34d7f6924309611.png)

**Populate with hosts:**
![4c331529d835dafe5de39d581e9d3936.png](../../_resources/4c331529d835dafe5de39d581e9d3936.png)

**CREDENTIALS**
![4ca0e76440c8a9487917d041428382d3.png](../../_resources/4ca0e76440c8a9487917d041428382d3.png)

![acbb68d436473ec632c16df9e56cc1bd.png](../../_resources/acbb68d436473ec632c16df9e56cc1bd.png)


# Projects
**Create Project**
![6cf15ed5119a24aaccd88205f491c522.png](../../_resources/6cf15ed5119a24aaccd88205f491c522.png)

**Job Temlates**
![0a90f788332181df22edfbb3c15987a2.png](../../_resources/0a90f788332181df22edfbb3c15987a2.png)


# Controlling Ansible Tower with the API
**From cli**
 ```
curl -X GET 192.168.0.62/api/ -k
{"description":"AWX REST API","current_version":"/api/v2/","available_versions":{"v2":"/api/v2/"},"oauth2":"/api/o/","custom_logo":"","custom_login_info":"","login_redirect_override":""}
```

**Web GUI**
![99ef08e2fd310215a4c7f1363ec3b6c8.png](../../_resources/99ef08e2fd310215a4c7f1363ec3b6c8.png)

# Troubleshooting 
Controling and checking Ansible tower Services
`ansible-tower-serice status` - Check if the service running properly
`ansible-tower-serice start/stop/restart`

Towe Web aplication is a collection of Django-based compenents managed by supervisord
`supervisord status`

Change the password for the built-in admin superuser
`awx-manage changepassword admin`

Configuration:
`/etc/tower/settings.py`

A number of key data files are kept in the `/var/lib/awx/projects`
```shell
/var/lib/awx/projects   # where files are pulled directly from source control 
/var/lib/awx/job_status # stores job status output from playbook run
/var/lib/awx/public/static # is the static root direcotry for the Django applications
```

Log files
```shell
/var/log/tower
tower.log
task_system.log
setup*.log
```
Django-based aplications
`/var/log/supervisord.log`

**Common Troubleshooting Scenarios**
Playbook stays in "Pending" state:
- Ensure that Ansible Tower has enough memory available.
- Use supervisord status to make sure the Django applications are running.
- Ensure that /var has at least 1 GB of free space.
- Try ansible-tower-service restart

Provided hosts list is empty ("Skipping: No Hosts Matched"):
- Make sure the hosts declaration in your play matches the group or host names in the inventory.
- Make sure group names have no spaces in them. Underscores are valid.
- If you specified a limit in the job template, make sure its syntax is valid and matches something in your inventory.