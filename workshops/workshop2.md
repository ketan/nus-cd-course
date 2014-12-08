**Institute of Systems Science  
National University of Singapore**



# NICF – Agile Continuous Delivery



# Workshop2

# Automated build of sample application by Continuous Integration Server











**Copyright 2014 ThoughtWorks. The contents contained in this document may not be reproduced in any form or by any means, without the written permission of ISS and NUS, other than for the purpose for which it has been supplied.**







**Objective: To set-up & configure a continuous integration (CI) server to run an automated build script.**

**Software:**

**Jenkins**

**What you will learn:**

- How to integrate a Continuous integration server with version control and your build scripts
- Basic Continuous Integration server configuration
- Basic Continuous Integration Server reporting



**Instructions to Continuous Integration (CI) server on build machine**

1. Start the virtual box that we created from previous exercise

vagrant up

1. Login into the box

vagrant ssh build

1. Install Jenkins server by running following commands. For installing Jenkins on other platforms refer the Jenkins installation page (https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins)wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add - sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ >/etc/apt/sources.list.d/jenkins.list'sudo apt-get update sudo apt-get install jenkins

1. You should have Jenkins server running. Verify by visiting http://localhost:8080 on your web browser.

 
**Instructions to run build with CI server**

1. Open the jenkins home page. http://localhost:8080
2. Goto "Manage Jenkins" link on the left nav bar
3. Goto "Manage Plugins"
4. Click on Available tab
5. Search for "Git plugin" and click "Install without restart". This will allow us to run build using out github repository.
6. Once plugin is installed go back to home page http://localhost:8080
7. Click on "Create new job"
8. Name the job as "ant\_jetty". This is to identify the project, you can name it anything you like.
9. Choose "Build a free-style software project" from the list of options.
10. Click Ok.
11. In the Source Control Management section select Git.
12. Add your github repository url that you created in previous exercise. https://github.com/your\_name/cd\_linux.git

 
1. Goto Build section
2. Click on "Add build step" and select "Invoke ant".
3. In the targets mention "test"


1. Click on "Save"
2. Go back to home page (http://localhost:8080)
3. You should see your project on home page


1. Click on green play button on the right and your build should start running
2. Once the build passes the color of bubble on the left should turn blue and you should see the sunshine.

