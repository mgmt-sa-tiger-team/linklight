# Exercise 4-2: Creating a Tower Job Template - User Template

## Table of Contents

- [Objective](#objective)
- [Guide](#guide)
- [Playbook Output](#playbook-output)
- [Solution](#solution)

# Objective

Demonstrate a vendor agnostic job template for user creation.  This job will configure a specified user through a survey.

This exercise will differ from the previous exercise by automating the creation of the survey.  We will use a supplied survey specification file (`user.json`) and playbook (`userjob.yml`) to quickly provision the job into Ansible Tower.

# Guide

## Step 1:

Make sure you are on the control node terminal (accessed either through SSH or RDP). Navigate to the `~/tower_setup` directory:

```
[studentX@ansible ~]$ cd ~/tower_setup/

```

From here, you can inspect the two files, `user.json` and `userjob.yml`. `userjob.yml` is a playbook that populates Ansible Tower with a Job template called `CONFIGURE USER`, which will add a new user to your routers. The playbook uses the contents of `user.json` to automatically create a survey that will ask for user information (username, password/SSH key, privilege level).


## Step 2:

Launch the job with the `ansible-playbook` command.

```
[studentX@ansible tower-setup]$ ansible-playbook userjob.yml
```

## Playbook Output

Here is the Playbook output:

```
[studentX@ansible tower-setup]$ ansible-playbook userjob.yml

PLAY [TOWER CONFIGURATION IN PLAYBOOK FORM] ************************************

TASK [CREATE USER JOB TEMPLATE] ************************************************
changed: [ansible]

PLAY RECAP *********************************************************************
ansible                    : ok=1    changed=1    unreachable=0    failed=0    skipped=0
```

## Step 3

Click the Templates button the left menu.

![templates button](images/template.png)

The Template menu will displays the new **CONFIGURE USER** job template.

![configure user job template](images/userjob.png)

Click the rocket button to launch the job.

![rocket button](images/rocket.png)

## Step 4

Fill out the survey, click the green **NEXT** button, then click the green **LAUNCH** button.

![user survey](images/user-survey.png)

Feel free to use whatever you want!

When the job launches you will go to the **Job Details View** which will look like this:

![job details view](images/running.png)

# Verify

Login to the routers to verify the user was created

```
[student1@ansible ~]$ ssh rtr1
```

then look for the user

```
rtr1#show run | i username ansible
username ansible secret 5 $1$qroK$DkZ4Z71o/ZSbifb8yRiza.
```

# Solution
You have finished this exercise.  

You have
 - created a job template for creating users on network devices
 - launched the job template from the Ansible Tower UI
 - looked under the covers on the control node to see where the Playbooks are being stored

[Click here to return to the exercise list](../)
