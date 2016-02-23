# Lab: Installing the CLI

## Prerequisites

You should receive the following from the instructor:

* Public and private IP's of the virtual machine on which the CLI is going to be installed
* Private key to use in order to access that virtual machine

Copy the private key, provided by the instructor, to the file system on the machine you're going to use
to connect to the various VM's (most likely, that would be your laptop).

**NOTE**: if you are accessing the VM's from Linux, make sure that the private key file has restrictive enough
permissions on it, to avoid being rejected by SSH (`0400` or `0600` would do):

```bash
chmod 0400 <pem_file>
```

### Creating your own CLI VM

If you don't have a CLI VM provided to you, or you would like to use your own image:

* Use a CentOS 7.0 image
* Install the following packages (using `yum`):
  * `unzip`
  * `git`
  * `wget`

  **NOTE**: These packages are not needed for the Cloudify CLI; they are needed for the completion of the labs.

## Preparing your CLI VM

`ssh` into your CLI VM, and run the following commands:

```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python get-pip.py
```

The above commands download the `pip` installer and run it.

**NOTE**: For CentOS/RHEL machines, EPEL contains `pip`; however, it is of an older version that is not supported
by Cloudify.

```
curl -J -O http://repository.cloudifysource.org/org/cloudify3/3.3.1/sp-RELEASE/cloudify-centos-Core-cli-3.3.1-sp_b310.x86_64.rpm
sudo yum install -y cloudify-centos-Core-cli-3.3.1-sp_b310.x86_64.rpm
```

The above commands download the CLI RPM package, and install it.

### Clone the training labs

```bash
git clone -b 3.3.1 https://github.com/cloudify-cosmo/cloudify-training-labs
```

**NOTE**: an alternative clone URL may be provided by the instructor.

### Activate the `cfy` virtual environment

```bash
source /opt/cfy/env/bin/activate
```

The command above activates the Cloudify CLI *virtual environment*. The virtual environment remains in effect until you
either deactivate it (using the `deactivate` command), or log out.

For simplicity, execute the following command to ensure that the virtual environment is activated automatically upon
logging in:

```bash
echo "source /opt/cfy/env/bin/activate" >> ~/.bash_profile
```

### Check Cloudify's version

```bash
cfy --version
```

The output should be similar to the following:

```
Cloudify CLI 3.3.1
```