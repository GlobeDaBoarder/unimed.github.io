# UniMed Baclk-end wiki
UniMed is an Andersen lab project in the healthcare domain. it is one of the leading projects in the whole laboratory, including technologies like AWS services and OpenAPI generator plugin. The following documentation aims to provide the most essential information to newcomers on how the application works, how to set it up and how to use it.

## SSH connection and cloning the repository
First of all, we would want to be able to  clone the repository locally. UniMed uses CodeCommit (an AWS service), as a remote repository. In order to perform cloning, the SSH key will have to be added to the AWS user.

### 1. If you do not have an AWS user, please ask DevOps to provide you with one
### 2. Go to the AWS console: 

https://eu-central-1.console.aws.amazon.com/console/home?region=eu-central-1#. Make sure that the region is selected as ***eu-central-1***

### 3. Login with provided credentials (they are provided by DevOps)
### 4. Go to the IAM service, by searching for it in the search bar
   ![image](https://github.com/GlobeDaBoarder/unimed.github.io/assets/74022878/216a42b9-333b-440f-900f-a0a51470f8b3)
### 5. On the left select ***Access management -> Users***
### 6. Select your user
### 7. At the top, select ***"Security credentials"***
### 8. Scroll down until you find ***"SSH public keys for AWS CodeCommit"***

### 9. At this point, if you don't have any SSH keys on your machine, generate one.

For Linux machines or Windows with [WSL](https://learn.microsoft.com/en-us/windows/wsl/install):
- To generate keys:
``` bash
ssh-keygen
```
- To view and copy public key:
``` bash
cat <<name of public key (id_rsa.pub by default>>
```
- Add key by pressing ***"Upload SSH public key"***

Once uploaded, you will be able to see it like this:
![image](https://github.com/GlobeDaBoarder/unimed.github.io/assets/74022878/31b6325b-7df9-4a4b-9bbf-8d6e658c7392)


### 10. In order to clone the repository, an ***"SSH key ID"*** has to be added to `config` file in the corresponding `~/.ssh`  folder on your local system
If you don't have a config file already, run:
``` bash
cd ~/.ssh
touch config    
```

Then add the following
``` config
Host git-codecommit.*.amazonaws.com
  User <<APKAEIBAERJR2EXAMPLE>>
  IdentityFile <<~/.ssh/codecommit_rsa>>
```
Where `User` is going to be your ***"SSH key ID"***
And `IdentityFile` is the path to the private ssh key file

### 11. Try testing your configuration:
``` bash
ssh git-codecommit.us-east-2.amazonaws.com
```

If you succeed, you will see:
```
You have successfully authenticated over SSH...
```
    
### 12. clone the repository of UniMed:
``` bash
git clone ssh://git-codecommit.eu-central-1.amazonaws.com/v1/repos/UniMedBackend
```
    
For a more detailed description of the process reference [AWS documentation](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-ssh-unixes.html)


## OpenAPI plugin
