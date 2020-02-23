# Rasp-test

Provisioning and stuff, on a rasp!

Running on your hardware:
* cp hosts/production hosts/production and modifiy inventory and group_vars accordingly
* Run:
```
ansible-playbook -i hosts/production/inventory playbook.yml
```

Running on Vagrant:
* Simply `vagrant up`
* Re-run with:
```
ansible-playbook -i hosts/staging/inventory playbook.yml
```
