# Institute of Systems Science National University of Singapore


# NICF - Agile Continuous Delivery


# Workshop 5

Automated deployment to multiple environments

**Objective**: To deploy an application to multiple environments in a build pipeline.

**Software**: Jenkins

## What you will learn

> Automated deployment to multiple environments using a Continuous Integration server with Build Pipeline capabilities

## Instructions to install Jenkins plugins needed for the exercise

* Start up the build machine so that we can see the Jenkins home page
vagrant up
* Go to Jenkins home page by visiting http://localhost:8080
* Go to "Manage Jenkins"
* Go to "Manage plugins"
* Go to "Available" tab
* Find and install "Build Pipeline Plugin" from list of available plugins

## Instructions to setup a build pipeline

* Go to Jenkins home page (http://localhost:8080)
* Click on "+" button next to "All"
* Name the view as "pipeline"
* Select "Build Pipeline View"
* Press "Ok"
* Mark the "Always allow manual trigger on pipeline steps" option as "YES"
* Press "Ok"
* You should see a pipeline view with "ant_jetty"
* Now we will deploy to staging right after our ant_jetty job passes
* Go to home page
* Click on ant_jetty job
* Go to Configure
* In the "Post-build Action" section click on "Add post-build action" button
* Select "Build other projects"
* Type in the deploy job name i.e. "deploy_to_staging"
* Save the configuration
* Go to Jenkins home page (http://localhost:8080)
* Click on the "pipeline" tab
* Trigger the "ant_jetty" job on Jenkins home page.
* Wait for job to complete and see what happens.
* Once the job is complete you should see that it automatically triggered "deploy to staging" job

## Exercise:

> Add another job for deploy to production, that runs on port 6060 and include that as the last step of the pipeline. Make sure that it doesn't run automatically after "deploy_to_staging" job.

**Hint**: In "Post-build Action" section of deploy_to_staging job configuration select "Build other projects (manual step)" instead of "Build other projects"
