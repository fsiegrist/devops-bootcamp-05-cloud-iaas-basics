## Notes on the videos
<br />

<details>
<summary>Video: Setup Server on DigitalOcean</summary>
<br />

Create an account on [DigitalOcean](https://cloud.digitalocean.com/registrations/new). You will have to register a payment method and pay USD 5 for verification purposes.

On DigitalOcean servers (virtual machines) are called `Droplets`.

Create your first Droplet:
- Choose Create > Droplets
- Select the closes region (Frankfurt)
- Choose image (Ubuntu 22.10 x64)
- Choose size (Droplet Type 'Basic')
- Choose CPU options (Regular, $4/month -> 512 MB)
- Choose authentication method (SSH Key -> click on 'Add SSH key' and paste your public key from ~/.ssh/ into the form (use `pbcopy < ~/.ssh/id_rsa.pub` to copy the key to the clipboard) and give it a name, e.g. name of the local machine)
- Click on 'Create Droplet'

To be able to connect to the server via ssh, we need to open the port 22 on the server.
- Click on the Droplet to open the details
- Click on 'Networking' > Firewalls Edit > Create Firewall
- Enter a name (e.g. droplet-firewall)
- Under 'Inbound Rules' select type SSH and replace AllIPv4 and AllIPv6 with the IP address of your machine (e.g. use [https://www.whatsmyip.org/](https://www.whatsmyip.org/) to determine your IP address)
- Click on 'Create Firewall'
- To add this rule to your Droplet, click on the rule, click on the 'Droplets' tab, click on 'Add Droplets' and type in the beginning of the Droplet's name to find and select it, click on 'Add Droplet'

SSH into the server:
- copy the Droplet's IP address
- execute `ssh root@<droplet-ip-address>`

Install Java:
- `apt update`
- `apt install openjdk-8-jre-headless`

</details>

*****

<details>
<summary>Video: Deploy and run application artifact on Droplet</summary>
<br />

Clone https://github.com/nanuchi/java-react-example.git

Build the application:
- `cd java-react-example`
- `./gradlew build`

Copy the application to the server:
- `scp build/libs/java-react-example.jar root@<droplet-ip-address>:/root`

Start the application on the server:
- `ssh root@<droplet-ip-address>`
- `java -jar java-react-example.jar`

The application starts and prints out: "Tomcat started on port(s): 7071 (http)". To open this port for browsers from any IP address, add another rule of type "Custom", tcp, port 7071, for any IP adresses to the droplet-firewall you created before.

Open the application in your browser calling `http://<droplet-ip-address>:7071`

To run the application in the background, start it executing `java -jar java-react-example.jar &`.
Use `ps aux` and `netstat -tlnp` (install it first using `apt install net-tools`) to get the process PID and the port.

</details>