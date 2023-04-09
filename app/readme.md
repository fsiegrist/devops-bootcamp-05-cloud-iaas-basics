This is the NodeJS application the exercises of module 05 "Cloud and IaaS Basics" of Nana Janashia's [DevOps Bootcamp](https://www.techworld-with-nana.com/devops-bootcamp) are based on.

The project uses jest library for tests (see "test" script in package.json).
There is one test (server.test.js) in the project that checks whether the main index.html file exists in the project. 

To run the nodejs test, execute:
```sh
npm run test
```

Make sure to download jest library before running test, otherwise jest command defined in package.json won't be found:
```sh
npm install
```

In order to see failing test, remove index.html or rename it and run tests.