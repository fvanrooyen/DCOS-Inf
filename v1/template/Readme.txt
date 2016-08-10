#AWS DC/OS Deployment
#Built the base VPC
$ bash ./zen.sh intrepid
#Update parameters file
#Launch the cluster 
aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name intrepid --template-body https://s3-us-west-2.amazonaws.com/dcosor2/main.json --parameters file://main-att.json

#Add more private nodes

aws cloudformation create-stack --capabilities CAPABILITY_IAM --stack-name intrepid --template-body https://s3-us-west-2.amazonaws.com/dcosor2/privagent.json --parameters file://addprivagents.json
#Add more private nodes
aws cloudformation update-stack --capabilities CAPABILITY_IAM --stack-name intrepid --template-body https://s3-us-west-2.amazonaws.com/dcosor2/pubagent.json --parameters file://addpubagents.json

Upgrading
https://dcos.io/docs/1.7/administration/upgrading/