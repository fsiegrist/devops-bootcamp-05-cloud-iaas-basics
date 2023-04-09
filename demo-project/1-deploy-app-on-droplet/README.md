## Demo Project - Deploying an Application on a DigitalOcean Server

### Topics of the Demo Project
Create a server and deploy an application on DigitalOcean.

### Technologies Used
- DigitalOcean
- Linux
- Java
- Gradle

### Project Description
- Setup and configure a server on DigitalOcean
- Create and configure a new Linux user on the Droplet (Security best practice)
- Deploy and run a Java Gradle application on Droplet

#### Steps to setup and configure a server on DigitalOcean
**Step 1:** Create Droplet\
Login to your account on [DigitalOcean](https://cloud.digitalocean.com/login) and do the following:
- Choose Create > Droplets
- Select the closest region (Frankfurt)
- Choose image (Ubuntu 22.10 x64)
- Choose size (Droplet Type 'Basic')
- Choose CPU options (Regular, $4/month -> 512 MB)
- Choose authentication method (SSH Key -> click on 'Add SSH key' and paste your public key from ~/.ssh/ into the form (on a Mac use `pbcopy < ~/.ssh/id_rsa.pub` to copy the key to the clipboard) and give it a name, e.g. name of the local machine)
- Click on 'Create Droplet'

**Step 2:** Open port 22 for SSH
- Click on the droplet to open the details
- Click on 'Networking' > Firewalls Edit > Create Firewall
- Enter a name (e.g. droplet-firewall)
- Under 'Inbound Rules' select type SSH and replace AllIPv4 and AllIPv6 with the IP address of your machine (e.g. use [https://www.whatsmyip.org/](https://www.whatsmyip.org/) to determine your IP address)
- Click on 'Create Firewall'
- To add this rule to your droplet, click on the rule, click on the 'Droplets' tab, click on 'Add Droplets' and type in the beginning of the droplet's name to find and select it, click on 'Add Droplet'

**Step 3:** Install Java
```sh
# ssh into the server
ssh root@<droplet-ip-address>

# install Java:
apt update
apt install openjdk-8-jre-headless
```

#### Steps to create and configure a new Linux user on the droplet
```sh
# ssh into the server
ssh root@<droplet-ip-address>

# reate a new user
adduser fesi

# add that user to the sudo group
usermod -aG sudo fesi

# exit the droplet
exit

# copy your public key (from local ~/.ssh folder) to the clipboard
pbcopy < ~/.ssh/id_rsa.pub

# ssh again into the server
ssh root@<droplet-ip-address>

# switch to user fesi
su - fesi

# create a file ~/.ssh/authorized_keys and paste the copied public into that file
mkdir .ssh
sudo vim .ssh/authorized_keys # paste the copied key and save the file

# exit user fesi and droplet
exit
exit
```

Now we can ssh into the droplet as user `fesi`.

#### Steps to deploy and run a Java Gradle application on the droplet
**Step 1:** Clone application repo\
`git clone https://github.com/nanuchi/java-react-example.git`

**Step 2:** Build the application
```sh
cd java-react-example
./gradlew build
```

**Step 3:** Copy the application to the server\
`scp build/libs/java-react-example.jar fesi@<droplet-ip-address>:/home/fesi`

**Step 4:** Start the application on the server
```sh
# ssh into the server as user fesi
ssh fesi@<droplet-ip-address>

# run the java application in the background
java -jar java-react-example.jar &
```

**Step 5:** Open application port\
The application starts and prints out: "Tomcat started on port(s): 7071 (http)". To open this port for browsers from any IP address, add another rule of type "Custom", TCP, port 7071, for any IP adresses to the droplet-firewall created before.

**Step 6:** Open app in browser\
Open your browser and navigate to `http://<droplet-ip-address>:7071`
