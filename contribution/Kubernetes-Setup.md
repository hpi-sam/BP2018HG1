Forwarded k8s ports:
* -M 2000 80:80
* -M 2002 22:9000
* -M 2004 4822:4822 (not needed anymore)
* -M 20020 443:443
* -M 2008 8080:8080

Example command: `sudo autossh -M 20008 -f -N -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -R 8080:172.22.15.254:8080 root@128.199.32.154`

### When server went down:
1. Enter `sudo wpa_cli` and enter `scan` to reconnect to network. Then enter `q` to escape the CLI.  
 You might have to restart wpa_supplicant with `wpa_supplicant -c /etc/wpa_supplicant.conf -D wired -i eno1`  
2. Afterwards redeploy kubespray with: `ansible-playbook -i inventory/mycluster/hosts.ini --become --become-user=root cluster.yml  --extra-vars='ansible_become_pass=our Password here´
3. Reopen all the ports listed above
4. If you are having problems with creating the autossh tunnels: list all open autossh connections: `ps aux | grep ssh` and kill everything that has autossh in its name or otherwise connects to our forwarding server IP with `sudo kill -9 PROCESS_ID`
