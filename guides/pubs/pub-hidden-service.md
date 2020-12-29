# Step by step guide: setting up a Tor Pub

This guide will step you through setting up an SSB Pub and a web server as a Tor hidden service accessed via a .onion URL.

This guide assumes you are basically familiar with a Linux environment.

## 1. Set up the Server

Pub servers -- even hidden ones -- need a static, publicly-reachable IP address.
The easiest way to get a public server is by renting a virtual server from businesses such as [Amazon](https://aws.amazon.com/), [Linode](https://www.linode.com/), or [Digital Ocean](https://www.digitalocean.com/).

This guide assumes the server is running Fedora Linux.

### SSH access
Set up an SSH key with your provider and enable [SSH-only access](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-2).

### Firewall
Setup your firewall. Incoming ports to keep open:
```
TCP 22   # ssh So you can get to your box :) Remove when done configuring
TCP 8008 # ssb This can be any port, just be consistent
TCP 80   # if you want a webpage for your pub
```

### .ssb Storage Volume
If you plan to encrypt the SSD data at rest, or you wish to be able to back it up and grow it easily, you may wish to add block storage with your VPS now.

Once you have added it through your provider's website, mount the storage. We'll link the SSB directory to this volume in a later step.
```
mkdir -p /mnt/mypub_ssb_storage
mount -o discard,defaults,noatime /dev/disk/{storage-dir} /mnt/mypub_ssb_storage
echo '/dev/disk/{storage-dir} /mnt/mypub_ssb_storage ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

### Automation and examples use these
`sudo dnf install nano`

### Pick up latest updates
`sudo dnf update`

## 2. Set up Tor services

See the [official Tor project Hidden Service guide](https://2019.www.torproject.org/docs/tor-onion-service.html.en) for mode background.

### Install Tor packages
`sudo dnf install libevent libevent-devel openssl openssl-devel zlib zlib-devel tor`

### [Configure](https://helpmanual.io/man5/torrc/) /etc/tor/torrc
`sudo nano /etc/tor/torrc`

Search for and change, uncomment, or add these two lines:
```
RunAsDaemon 1
DataDirectory /var/lib/tor
```

Now add these 4 lines for our Hidden Service:
```
HiddenServiceDir /var/lib/tor/ssb_hs/
HiddenServiceVersion 3
HiddenServicePort 8008 127.0.0.1:8008
HiddenServicePort 80   127.0.0.1:80
```

Now save and quit nano.

### Set up hidden service directory
```
sudo mkdir /var/lib/tor/ssb_hs
sudo chown toranon:toranon /var/lib/tor/ssb_hs
sudo chmod 700 /var/lib/tor/ssb_hs
```

### Vanity address
If you want a "vanity" Tor address, you can run [mkp224o](https://github.com/cathugger/mkp224o) to try zillions of combinations and find one you like.

Copy these 3 files from your mkp224o output directory into the hidden service directory
```
sudo cp hostname /var/lib/tor/ssb_hs
sudo cp hs_ed25519_public_key /var/lib/tor/ssb_hs
sudo cp hs_ed25519_secret_key /var/lib/tor/ssb_hs
cd /var/lib/tor/ssb_hs
chmod 600 hostname hs_ed25519_public_key hs_ed25519_secret_key
chown toranon:toranon hostname hs_ed25519_public_key hs_ed25519_secret_key
```

If you don't want a vanity address, just leave the directory blank. Tor will set it up with a random .onion address and public/secret keypair.

### Start up tor services
```
systemctl start tor
systemctl enable tor
```

## 3. Set up web server
This way your Pub can have a nice welcome page.

### Install nginx
`sudo dnf install nginx`

### [Secure](https://geekflare.com/nginx-webserver-security-hardening-guide/) nginx.conf
`sudo nano /etc/nginx/nginx.conf`

Add the following 6 lines in the nginx.conf "server" section:
```
if ($request_method !~ ^(GET|HEAD|POST)$ )
{
return 405;
}
add_header X-Frame-Options "SAMEORIGIN";
add_header X-XSS-Protection "1; mode=block";
```

Save and quit nano.

### Create your webpages
Pages are served from `/usr/share/nginx/html`
Update the HTML there; remove anything that you don't use.

### Start the webserver
```
systemctl start nginx
systemctl enable nginx
```

Now you should be able to navigate [Tor Browser](https://www.torproject.org/download/) on your laptop or PC to your .onion url, and see your page.


## 4. Set up SSB itself

Create a dedicated SSB group `ssbpubs` and Pub user [hce](https://en.wikipedia.org/wiki/Finnegans_Wake#Humphrey_Chimpden_Earwicker_%28HCE%29) . 
```
sudo groupadd ssbpubs
sudo useradd hce -c "Pub user server for SSB pub" -g ssbpubs -m -s /usr/bin/bash -p {your-password}
su - hce
echo "umask 077" >> ~/.bashrc
```

The following is basically a condensed summary of the regular [pub setup](setup-a-pub.md)

### Install NPM
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | bash
nvm install 10
nvm alias default 10
```

### Install/update ssb-server
```
npm install -g ssb-server
npm install -g ssb-config
```

### Setup SSB storage
The .ssb directory holds all the data, and will get big.
If you had set up block storage, link to it here.
```
sudo chown hce:ssbpubs /mnt/mypub_ssb_storage
mkdir -p /mnt/mypub_ssb_storage/.ssb
ln -s /mnt/mypub_ssb_storage/.ssb $HOME/.ssb
```

### Configure SSB for Tor
Create file ~/.ssb/config with these contents:
```
{
  "allowPrivate": "true",
  "host": "127.0.0.1",
  "incoming": {
    "net":  [{ "host": "127.0.0.1", "port": 8008, "scope": "public", "transform": "shs" }]
  },
  "outgoing": {
    "onion": [{ "transform": "shs" }]
  }
}
```

### Start up SSB
`nohup ssb-server start --host 127.0.0.1 >& ~/ssb_server.log &`

Now let's verify it's working, and get your public key:
```
% ssb-server whoami
{
  "id": "@5h3PV3hVBTYmQn2iDZdkA8nx7PSem9co3rsOmZOyyCM=.ed25519"
}
```

Note, your private key is in `~/.ssb/secret`

### Set up your Pub profile

If you have a logo or picture, send it to "ssb-server blobs.add". This returns the SSB file-id you can use set it as your Pub profile pic.
```
cat my-ssb-logo.png | ssb-server blobs.add
ssb-server publish --type about --about {id-from-whoami} --name "My Pub" --image {fileid-from-blobs.add}
ssb-server publish --type post --text "My First Post!"
```

Request for HTTP/SSB bridges to please not serve webpages of your public posts
`sbot publish --type about --about {id-from-whoami} --no-publicWebHosting`

Announce yourself to the world as a Pub!
`ssb-server publish --type pub --address.key {feedId} --address.host {pub-address.onion} --address.port 8008`

### Invite people to the Pub
Run this command to create an invite that can be used 100 times. Adjust the number as you wish.
`ssb-server invite.create 100`

This creates output like
```
127.0.0.1:8008:@5hTpvduvbDyMLI2dezDKa7ne7PSem9co3RsOmZoyyCM=.ed25519~yUcWRzpoUMjBeQMZC8319Uy4Ohq9JbYK9Iyv9ng7O1k=
```
Replace the IP address 127.0.0.1 with your .onion url

Patchwork is able to accept .onion invites.

## 5. Keep SSB running

Maintaining your hidden SSB Pub is no different than doing so as a surface web Pub.
* Periodically update packages with `sudo dnf update`
* Keep the ssb-server process running

Please follow the remainder of the usual Pub setup instructions, starting with [Create a run-server.sh script](setup-a-pub.md#4.%32Create%32a%32run-server.sh%32script)

