# Web Server Using Amazon EC2

This example deploys a simple AWS EC2 virtual machine running a Python web server.

## Deploying the App

To deploy your infrastructure, follow the below steps.

### Prerequisites

1. [Install Pulumi](https://www.pulumi.com/docs/get-started/install/)
2. [Configure AWS Credentials](https://www.pulumi.com/docs/intro/cloud-providers/aws/setup/)

### Steps

After cloning this repo, from this working directory, run these commands:

1. Pulumi login

   ```bash
   pulumi login file:///home/nurcahyo/Projects/Personal/pulumi-malang-cloud/states
   ```

1. Initiate new pulumi projects

   ```bash
   $ pulumi new aws-typescript -g --dir webserver2
   $ cd webserver2
   $ npm i
   ```

1. Create a new stack, which is an isolated deployment target for this example:

   ```bash
   $ pulumi stack init
   ```

1. Set the required configuration variables for this program:

   ```bash
   $ pulumi config set aws:region us-east-1
   ```

1. Stand up the VM, which will also boot up your Python web server on port 80:

   ```bash
   $ pulumi up
   ```

1. After a couple minutes, your VM will be ready, and two stack outputs are printed:

   ```bash
   $ pulumi stack output
   Current stack outputs (2):
   OUTPUT          VALUE
   publicHostName  ec2-53-40-227-82.compute-1.amazonaws.com
   publicIp        53.40.227.82
   ```

1. Thanks to the security group making port 80 accessible to the 0.0.0.0/0 CIDR block (all addresses), we can curl it:

   ```bash
   $ curl $(pulumi stack output publicIp)
   Hello, World!
   ```

1. From there, feel free to experiment. Simply making edits and running `pulumi up` will incrementally update your VM.

1. Afterwards, destroy your stack and remove it:

   ```bash
   $ pulumi destroy --yes
   $ pulumi stack rm --yes
   ```
