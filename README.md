Pusher - Git-based deployment tool
==================================

**Note:** This is still in development

Set-up
------

The Pusher configuration is stored in `.pusher` in the root of the project.  It's a YAML file

    environments:
      staging: user@server1.example.com:/var/www
      live: user@server2.example.com:/var/www
    handlers:
      post-deploy: ./tools/post-deploy
      test-deploy: ./tools/test-deploy

Environments:

Each environment is defined as a git remote.  Each environment will be set up as a remote on your local repository, and a branch will be created for that environment.

Handlers:

Each handler is a shell comamnd

Each environment gets a branch

	 * Environments: these are defined as git remotes
 * 

Setting up an environment

    pusher init-environment staging
    pusher init-environment live

Usage
-----

Creating a hotfix

    # First, commit your fix to the stable branch
    git checkout live
    git checkout 1a2b3c

    # Now run pusher
    pusher hotfix
    # Pusher will recommend a version and print a change summary for you to use to get approval
    # When you have approval, deploy it
    pusher deploy live v1.2.3   

Creating a release

    # First, merge your changes to the staging branch
    git checkout staging
    git merge master

    # Now run pusher
    pusher release
    # Pusher will recommend a version and print a change summary for you to use to get approval

    # When you have approval, deploy it to staging
    pusher deploy staging v1.2.3   

    # When it's been tested and approved, deploy it to live
    pusher deploy live v1.2.3

Roll back

    pusher deploy staging v1.2.1
    pusher deploy staging v1.2.2
    pusher deploy staging v1.2.3

    pusher rollback staging
    # Now v1.2.2 is on staging

    pusher rollback staging
    # Now v1.2.1 is on staging

Show current status

    pusher environments
    # Lists all the environments, their current versions, and whether they are "dirty" (local uncommitted changes)

    pusher versions
    # Lists all versions and whether they are on any particular environment
