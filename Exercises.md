## Exercises
<br />

<details>
<summary>Exercise 0: Clone Git Repository</summary>
<br />

**Tasks:**

- clone the git repository `git@gitlab.com:devops-bootcamp3/node-project.git`
- create your own project/git repo from it

**Steps to solve the tasks:**

```sh
git clone git@gitlab.com:devops-bootcamp3/node-project.git
cd node-project

# remove remote repo reference
rm -rf .git
# create your own local repository and commit its content
git init 
git add .
git commit -m "Initial commit"

# create git repository on GitHub push your newly created local repository to it
git remote add origin git@github.com:fsiegrist/devops-bootcamp-05-cloud-iaas-basics.git
# rename master branch of original Gitlab repository to main (default on GitHub)
git branch -M main
# push your newly created local repository to it
git push -u origin main
```

</details>

******

<details>
<summary>Exercise 1: Package NodeJS App</summary>
<br />

**Tasks:**

To have just 1 file, you create an artifact from the Node App. So you do the following:
- Package your Node app into a tar file (npm pack)

**Steps to solve the tasks:**

```sh
cd app
npm pack
```
This creates a tar file called `bootcamp-node-project-1.0.0.tgz`.

</details>

******

<details>
<summary>Exercise 2: Create a new server</summary>
<br />

**Tasks:**

Your company uses DigitalOcean as Infrastructure as a Service platform, instead of having on-premise servers. So you:
- Create a new droplet server on DigitalOcean

**Steps to solve the tasks:**

Create a droplet:
- Login to your account on [DigitalOcean](https://cloud.digitalocean.com/login).
- Choose Create > Droplets
- Select the closest region (Frankfurt)
- Choose image (Ubuntu 22.10 x64)
- Choose size (Droplet Type 'Basic')
- Choose CPU options (Regular, $4/month -> 512 MB)
- Choose authentication method (SSH Key -> click on 'Add SSH key' and paste your public key from ~/.ssh/ into the form (on a Mac use `pbcopy < ~/.ssh/id_rsa.pub` to copy the key to the clipboard) and give it a name, e.g. name of the local machine)
- Click on 'Create Droplet'

To be able to connect to the server via ssh, open the port 22 on the server:
- Click on the droplet to open the details
- Click on 'Networking' > Firewalls Edit > Create Firewall
- Enter a name (e.g. droplet-firewall)
- Under 'Inbound Rules' select type SSH and replace AllIPv4 and AllIPv6 with the IP address of your machine (e.g. use [https://www.whatsmyip.org/](https://www.whatsmyip.org/) to determine your IP address)
- Click on 'Create Firewall'
- To add this rule to your droplet, click on the rule, click on the 'Droplets' tab, click on 'Add Droplets' and type in the beginning of the droplet's name to find and select it, click on 'Add Droplet'

SSH into the server:
- copy the Droplet's IP address
- open your local machine's console/terminal and execute `ssh root@<droplet-ip-address>`

</details>

******

<details>
<summary>Exercise 3: Prepare server to run Node App</summary>
<br />

**Tasks:**

Now you have a new fresh server nothing installed on it. Because you want to run a NodeJS application you need to install Node and npm on it:
- Install nodejs & npm on it

**Steps to solve the tasks:**

```sh
# ssh into the server
ssh root@<droplet-ip-address>
# install nodejs and npm
apt install -y nodejs npm
```

</details>

******

<details>
<summary>Exercise 4: Copy App and package.json</summary>
<br />

**Tasks:**

Having everything prepared for the application, you finally:
- Copy your simple Nodejs app tar file and package.json to the droplet

**Steps to solve the tasks:**

```sh
# on local machine in folder <project_root>, execute:
scp app/bootcamp-node-project-1.0.0.tgz root@<droplet-ip-address>:/root

# the file package.json is already contained in the packed tar file we just copied into the droplet
# so there's no need to copy it separately
```

</details>

******

<details>
<summary>Exercise 5: Run Node App</summary>
<br />

**Tasks:**

Start the node application in detached mode (npm install and node server.js commands)

**Steps to solve the tasks:**

```sh
# ssh into the server on DigitalOcean
ssh root@<droplet-ip-address>

# unpack the copied tar file (z=unzip and x=untar)
tar zxvf bootcamp-node-project-1.0.0.tgz

# unpacking the tar file leaves a folder called package containing the files of the original app folder
cd package
# install dependencies
npm install
# run the application in the background
node server.js &
# the server now listens on port 3000 (ps aux | grep node; netstat -tlnp)
```

</details>

******

<details>
<summary>Exercise 6: Access from browser - configure firewall</summary>
<br />

**Tasks:**

You see that the application is not accessible through the browser, because all ports are closed on the server. So you:
- Open the correct port on Droplet
- and access the UI from browser

**Steps to solve the tasks:**

The application is running on port 3000. To open this port for browsers from any IP address, login to your account on [DigitalOcean](https://cloud.digitalocean.com/login) and add another rule of type "Custom", TCP, port 3000, for any IP adresses to the firewall ('droplet-firewall') created in exercise 2.

Now the application can be accessed in the browser under `http://<droplet-ip-address>:3000`

******
