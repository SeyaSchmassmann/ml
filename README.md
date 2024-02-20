# Machine Learning FS 2024

This repository is used for the distribution of the graded assignments for the Machine Learning module @ FHNW in FS2024 for the Studiengang Informatik.  

This README contains information about how to work on the assignments and how to hand them in.


## Assignments

The assignments are placed in individual directories. The following table lists the planned release and due dates:

| Graded Assignment | Released               | Due by                           |
|-------------------|------------------------|----------------------------------|
| 1                 | Montag, 04. März 2024  | Montag, 25. März 2024, 23:59 Uhr |
| 2                 | Montag, 15. April 2024 | Montag, 6. Mai 2024, 23:59 Uhr   |
| 3                 | Montag, 20. Mai 2024   | Montag, 10. Juni 2024, 23:59 Uhr |


The assignments will be graded and will make up the course grade.


The following instructions show how to work on the assignments and how to hand them in.


## Working on the assignments

The assignments are released as Jupyter Notebooks. You can work on them in
[**JupyterLab**](https://jupyter.org/). We provide you with two options to work on the assignments using JupyterLab and a standardized software stack:

- A) on a hosted JupyterLab server
- B) on your own device

**Important: for the graded assignments, only submissions that run / execute without error in this stack will be graded.**


### Option A : JHub 

We provide you with the online platform JHub at [https://jhub.cs.technik.fhnw.ch](https://jhub.cs.technik.fhnw.ch). **Select the image** `sgi_ml_fs2024` when starting the service.

(Please be aware that on JHub only files that are in `/home/jovyan/work/persistent/` are safe from being deleted, when your server is being restarted, which can also occur due to maintenance reasons.)

If you want to use this option, proceed as follows:


#### 1. Fork this repository

Fork this repository to your own user space by pressing the fork button on the upper right.  

**Add @marco.willi as a maintainer to your fork**. If you don't do this I won't see your submissions.

**Set visibility of your fork to Private**. In your fork go to "Settings -> General -> Visibility, .. -> Project Visibility" and set to _Private_.


#### 2. Clone your fork to your workspace in JHub

You can use an access API token to avoid having to type your username and password, as well as having to confirm logins with 2FA.

To use an API token, on GitLab in your fork of the repository:

"Settings->Access Tokens"

1. Enter a name for your access token
2. Select an expiration date well after this course ends
3. Select the maintainer role
4. Select "api" under scopes
5. Create token and save it  (`MY_ACCESS_TOKEN`)
6. Find the address of your repo without the https prefix (`MY_REPO_FORK_ADDRESS_NO_HTTPS`)


Open a terminal window in JupyterLab, `cd` into `/home/jovyan/work/persistent`.

```
cd /home/jovyan/work/persistent
```

Then you can clone the repository with the following command:

```
git clone https://api:MY_ACCESS_TOKEN@MY_REPO_FORK_ADDRESS_NO_HTTPS
```

example:

```
git clone https://api:thisisnotaRealtoken@gitlab.fhnw.ch/marco.willi/ml_assignments_fs2024.git
```

You might also have to set your user name and email once (replace accordingly):

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```


#### 3. Submitting assignments

You can now edit files in the clone of your fork on JHub. Whenever you want to
upload something to your Repo on GitLab you need to 'commit' and 'push' it in the terminal:

```
# commit MY_FILE
git commit MY_FILE -m 'my commit message'

# push all commits to the server
git push
```

**By pushing your commits to your personal fork on GitLab you will submit the
(graded) Assignments! The last commit before the deadline will be graded.**

#### 4. Fetching new assignments 

To fetch new assignments from the assigments/upstream repo do as follows:

```
# add original repo as remote upstream 
git remote add upstream https://gitlab.fhnw.ch/ml/courses/ml/ml_fs2024/ml_assignments_fs2024.git

# now whenever you want to merge the changes from the remote upstream repo,
# ie the one you forked from, you can do:
git pull upstream main
```

.. and add some merge message in case you have to merge.

You can use the api token name/password when prompted for a username/password.



### Option B : Local setup


#### 1. Install Docker on your computer

Depending on your operating system you have to install docker in different ways.  

You'll find detailed instructions here: https://docs.docker.com/get-docker


#### 2. Pull the Docker image

```
# login to the FHNW GitLab docker registry first
docker login cr.gitlab.fhnw.ch -u registry_pull -p byydHirZEAHaws7Gt5tv
```

Select the image tag: 'latest' for x86 (standard) and 'latest-arm' for arm (Mac):
```
IMAGE_TAG=latest
```

```
# now pull the image
docker pull cr.gitlab.fhnw.ch/ml/courses/ml/ml_fs2024/ml_assignments_fs2024:${IMAGE_TAG}
```

#### 3. Fork this repository

Fork this repository to your own user space by pressing the fork button on the upper right.

**Add @marco.willi as a maintainer to your fork**. If you don't do this I won't see your submissions.

**Set visibility of your fork to Private**. In your fork go to "Settings -> General -> Visibility, .. -> Project Visibility" and set to _Private_.

#### 4. Clone your fork to your computer. 

A simple way to clone your repository and to authenticate yourself is to use an API token.

To use an API token do the following on GitLab in your fork of the repository:

"Settings->Access Tokens"

1. Enter a name for your access token
2. Select an expiration date well after this course ends
3. Select the maintainer role
4. Select "api" under scopes
5. Create token and save it  (`MY_ACCESS_TOKEN`)
6. Find the address of your repo without the https prefix (`MY_REPO_FORK_ADDRESS_NO_HTTPS`)

Then you can clone the repository into your ml directory (`MY_ML_DIR`) using:

```
git clone https://api:MY_ACCESS_TOKEN@MY_REPO_FORK_ADDRESS_NO_HTTPS MY_ML_DIR
```


example:

```
git clone https://api:thisisnotaRealtoken@gitlab.fhnw.ch/marco.willi/ml_assignments_fs2024.git
```



#### 5. Start a ml container on your machine

```
# Define Image Tag
IMAGE_TAG=latest

# Replace 'MY_ML_DIR' with your local code directory
docker run -d \
    -p 8877:8888 \
    --user root \
    -v MY_ML_DIR:/home/jovyan/work/ \
    --name=ml_fs2024 \
    cr.gitlab.fhnw.ch/ml/courses/ml/ml_fs2024/ml_assignments_fs2024:${IMAGE_TAG} start.sh jupyter lab --LabApp.token=''
```

#### 6. Check that your container is running

```
docker ps -a
```

#### 7. Connect to your container through your browser

Enter `http://localhost:8877/lab` in your browser.


#### 8. Restart

If you later on need to restart your container you can just run

```
docker start ml_fs2024
```


#### 9. Submitting assignments

You can now edit files in the clone of your fork on your local machine.
Whenever you want to upload something to your Repo on GitLab you need to 'commit' and 'push' it:

```
# commit MY_FILE
git commit MY_FILE -m 'my commit message'

# push all commits to the server
git push
```

**By pushing your commits to your personal fork on GitLab you will submit the
(graded) Assignments! The last commit before the deadline will be graded.**


#### 10. Fetching new assignments 

To fetch new assignments from the assigments/upstream repo do as follows:

```
# add original repo as remote upstream 
git remote add upstream git@gitlab.fhnw.ch:ml/courses/ml/ml_fs2024/ml_assignments_fs2024.git

# now whenever you want to merge the changes from the remote upstream repo, ie
the one you forked from, you can do:
git pull upstream main
```

.. and add some merge message in case you have to merge.

You can use the api token name/password when prompted for a username/password.
