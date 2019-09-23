# Create an Account
Go to the Console (console.aws.amazon.com)
Using region us-west-1
Go to Elastic Beanstalk service

# Go to ElasticBeanstalk & create an EB Application
Select "Create New Application" in console
Application name: django-ws

# Create an EB Environment
Create an environment

Select environment tier: Web server environment
Leave default environment name
Platform: Preconfigured platform: Docker
Application code: sample application
Select Configure more options

Custom Configuration
Load balancer: Application load balancer

select Network configuration 
VPC: default VPC
Load balancer settings: Visibility Public Select both subnets for instances and both for load balancer subnets
Leave everything else as default

select instances
modify security group
use Django-WS-env

Select "Create environment"

When the environment boot up completes, you should see "Congratulations" when you navigate to the environment url (<custom name>.us-west-1.elasticbeanstalk.com)

Note that this environment is NOT in the AWS Free tier because it is using an Application load balancer. This is required for a websocket application. We will shut down environment while not in use. 

# Go to ElastiCache
Services —> Elasticache
Create new ElastiCache cluster
* Redis
* size t2.micro
* name: django-ws
* select two subnets
* place URL in REDIS_HOST variable in settings.py

# Configure EB CLI
install eb-cli

From chat_project directory
eb init --it
us-west-1
select application django-ws and environment Django-WS-env

eb ssh --setup

# change permission on start_app
chmod +x start_app.sh

# deploy
eb deploy


# Dockerrun.aws.json (if needed)
{
 "AWSEBDockerrunVersion": "1",
 "Ports": [
    {
      "ContainerPort": 8080
    }
  ],
 "Logging": "/var/eb_log"
}
