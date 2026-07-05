# Velociraptor Server

Create the VM, install the server then log in for the first time. For convenience I use secure shell to operate the system natively.

##  Secure Shell
SSH in from my host machine:
```
ssh -L 8889:localhost:8889 username@<VM-IP>
```

Then execute everything from here.

## Installing Velociraptor

- Download
```cd /tmp
wget https://github.com/Velocidex/velociraptor/releases/download/v0.75/velociraptor-v0.75.7-linux-arm64
wget https://github.com/Velocidex/velociraptor/releases/download/v0.75/velociraptor-v0.75.7-linux-arm64.sig
```
Reasons for using this version of velociraptor instead of latest at time of writing 0.76.6 "There is a bug with the velociraptor debian server command - please use an earlier release". Did intially use v0.76.6 however many issues with setup persisted hence change.

- verify SHA256 checksum
```
echo "0867711982a4bca1b53325ac82b439a585aa9a8a5af9476f364cf2719a44b84c  velociraptor-v0.75.7-linux-arm64" | sha256sum -c -
```

- verified ok
```
velociraptor-v0.75.7-linux-arm64: OK
```

- gpg signature added
```
gpg --keyserver keys.openpgp.org --recv-keys 0572F28B4EF19A043F4CBBE0B22A7FB19CB6CFA1
```

- verified
```
gpg --verify velociraptor-v0.75.7-linux-arm64.sig velociraptor-v0.75.7-linux-arm64
```

- make executable and move
```
sudo mv velociraptor-v0.75.7-linux-arm64 /usr/local/bin/velociraptor
sudo chmod 755 /usr/local/bin/velociraptor
```

- checked if working
```
velociraptor version
```

## Configuring Velociraptor

- Generate a server configuration
```
sudo mkdir -p /etc/velociraptor
sudo velociraptor --config /etc/velociraptor/server.config.yaml config generate -i
```
- Page 1
Select: Self Signed SSL
Choose: Linux

- Page 2
Keep default

- Page 3
Replace IP with ubuntu server IP.

- Page 4
Create user and password
Username: admin
Password: *******
Afterwards just press enter leaving all input blank so the wizard knows we are finished.

- Page 6
Choosing where to save the config file.
Overide with the following 
```
/etc/velociraptor/server.config.yaml
```

## Start Velociraptor

Runs the server in foreground
```
sudo velociraptor --config /etc/velociraptor/server.config.yaml frontend -v
```

- GUI is ready 
https://127.0.0.1:8889/
- Frontend is ready
https://192.168.*.*:8000/

- Can now access GUI in web browser using above address, accept risk, input credentials, should now be able to see the dashboard which indicates fully functional

## Create Permanence For Reboots

- Generate the server .deb package (uses your existing config)
```
sudo mkdir -p /tmp/velociraptor_server.deb
sudo velociraptor --config /etc/velociraptor/server.config.yaml debian server --output /tmp/velociraptor_server.deb
```

- Install the freshly built package
```
sudo dpkg -i /tmp/velociraptor_server.deb/velociraptor-server-0.75.7.arm64.deb

```
- Fix permissions on the datastore (this is the only thing the .deb can't do automatically)
```
sudo chown -R velociraptor:velociraptor /opt/velociraptor
```

- Start the real service
```
sudo systemctl daemon-reload
sudo systemctl enable --now velociraptor_server.service
```

- Final check
```
sudo systemctl status velociraptor_server.service
```

- Reboot then check status again
```
sudo reboot
```

- Pulled client config file for endpoint deployement.

# Windows Endpoint

- Added the client config file into program files along with Velociraptor installalation file.
- Ran velociraptor executable and endpoint visibility went live.