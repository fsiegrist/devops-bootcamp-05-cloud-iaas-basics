# DevOps Bootcamp
## Module 05 "Cloud and IaaS Basics"
<br />

This project contains notes related to the videos and exercises in Module 05 "Cloud and IaaS Basics" of Nana Janashia's [DevOps Bootcamp](https://www.techworld-with-nana.com/devops-bootcamp).

It also contains the NodeJS application the exercises of this module are based on.

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

### Test
The project uses jest library for tests (see "test" script in package.json).
There is one test (server.test.js) in the project that checks whether the main index.html file exists in the project. 

To run the nodejs test, execute:

    npm run test

Make sure to download jest library before running test, otherwise jest command defined in package.json won't be found:

    npm install

In order to see failing test, remove index.html or rename it and run tests.