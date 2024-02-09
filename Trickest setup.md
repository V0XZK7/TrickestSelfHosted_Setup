Setup process for a Self Hosted debian machine for the trickest.io platform.
https://trickest.io/dashboard/settings/fleet
https://docs.trickest.io/trickest-documentation/tutorials/using-self-hosted-machines

On an debian VM with a minimal install (No GUI & only the SSH module installed): 

```
su - root
apt update && upgrade
apt install curl ufw sudo rsyslog
ufw allow 3000/tcp
# if you access your server via SSH, open port 22
ufw allow 22/tcp
ufw enable
nano .bashrc

### Add the following lines
export TRICKEST_CLIENT_AUTH_ID="YourAuthID"
export TRICKEST_CLIENT_AUTH_SECRET="YourAuthSecret"
### Save & exit

curl https://trickest.io/download/agent/latest/init -so init.sh
chmod +x init.sh
./init.sh
systemctl enable trickest-agent.service
reboot
```

Make sure you also enabled port forwarding on your gateway, allowing incoming connections to port 3000 and redirecting it to your VM
