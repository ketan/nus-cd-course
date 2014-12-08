**Institute of Systems Science National University of Singapore**

# NICF – Agile Continuous Delivery



# Workshop 1

# Create automated build

**Copyright 2014 ThoughtWorks. The contents contained in this document may not be reproduced in any form or by any means, without the written permission of ISS and NUS, other than for the purpose for which it has been supplied.**



**Objective: To familiarize and work with build scripts and version control.**



**Software(s) Used:**

**Java Development Kit, Git, Ant**



**What you will learn:**

- The basics of using version control software
- Basic Ant build file structure
- Running Ant scripts

**Notes:**

- Participants should be able to fork a public Github project and check it out

**Basic flow:**

- Checkout git repository
- Bring up server, check whether it is accessible
- Modify build file to add a target (test if app web server is running?)

**Instructions to setup build machine using vagrant**

1. Open a command prompt
2. Create a folder "workshop1" under the D:\workshops folder and cd into it

D:

cd workshops

mkdir workshop1

cd workshop1

1. Add box file to vagrant, using following command

vagrant box add build d:\boxes\lucid32.box

1. Download the zip file from the following location, and unzip it to the workshop1 folder

http://bit.ly/1e4Fz8l

1. Start build server

vagrant up

1. ssh into the build server

vagrant ssh build

**You should have a build server ready with required packages installed (jdk, ant, maven etc.)**

**Instructions to run build on the sample project**

1. Fork the git repository containing the sample project by following the instructions below.
2. Log into your GitHub account or create a personal account at http://github.com/join
3. Go to https://github.com/nus-continuous-delivery/cd\_linux in your browser and fork the repository by clicking on the 'fork' button in the top right corner.
4. Check that you are logged into your build server
5. Clone your git repository 

git clone [https://github.com/your\_name/cd\_linux.git](https://github.com/your_name/cd_linux.git)

1. Go into the cloned repository

cd cd-linux

1. Run the build for this sample project, using ant. Run the following command

ant

1. You should see the "Build Successful" message



**Instructions to verify that app is working (manually)**

1. Run the app server on build machine

ant run

1. Open a browser and see if the app is working. Go to following url

[http://localhost:9090/time](http://localhost:9090/time)

1. You should see the current date and time in the browser.


**Instructions to verify that app is working (using build)**

1. Stop the running app (^C)
2. Open the build.xml file
3. To make sure that the app runs in the background add following attribute to java node in "run" target

spawn="true"

1. Run the "test" target to verify that the test target is running. What happens? Why?

ant test

1. Modify the target "test" to run junit by removing the <fail/> task and uncommenting the <junit> task. 

1. Run the "test" target to verify that the app is working

ant test

1. You should see "Build Successful" message. What is happening here?
2. Commit and push your changes to Github repository. Follow the on screen instructions to set up your git username and email. You'll need your Github credentials in order to push.

**Exercise:**

1. Change the url in the java code from /time to /datetime.
