## How to setup SSH access to the GitHub repo

* cd ssh
* ssh-keygen -t rsa -f id_rsa-octopress
* Install the deploy key on the [GitHub repo](https://developer.github.com/guides/managing-deploy-keys/#deploy-keys)

## Build the image
* docker build -t octopress/octopress .

## Run the container
* docker run -d --name octopress -p 4000:4000 octopress/octopress
