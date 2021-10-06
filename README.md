# Terraform for Katai AWS Infrastructure

This template is used to build the AWS Infrastructure for katai Dev/Prod Environments.

## Description

Infrastructure setup using Terraform version 0.12.24 with provider version 2.52.0. Here, we creating the AWS Dev/Prod infrastructure using a single terraform code by passing the vars during terraform apply. We are using the AWS region us-east-1 for both Prod/dev environment.

## Getting Started

### Dependencies

* The terraform version 0.12.24 installed in the machine
* We need to manually create the AWS S3 bucket katai-terraform-state-bucket in us-east-1 region.
* Create the following AWS key pairs and keep it in a safe place.

```
dev-katai.pem
prod-katai.pem
```

### Installing

* Clone the repo

```
git clone git@bitbucket.org:remotereality/kataicloudautomation.git
```

* Switch to the branch katai-aws-infra-terraform

```
git checkout katai-aws-infra-terraform
```

### Terraform commands execution

* Initialize the terraform using the below command
```
terraform init
```

* We are building the the AWS infrastructure using terraform workspace feature and we have to create the different workspaces for Dev and Prod environments. Here, we choosing the environment as Dev.

To list the current workspaces, Run the below command

```
terraform workspace list
```

To create new workspace, Run the below command

```
terraform workspace new dev
```

Once, the new workspace is successfully created, make sure that you are in the newly created workspace. 

To check the current terraform workspace

```
terraform workspace list
```

To see the current terraform state, Run the below command

```
terraform state list
```

Terraform plan for dev environemnt

```
terraform plan -input=false -var-file=dev.tfvars
```




## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release

## License

This project is licensed under the [NAME HERE] License - see the LICENSE.md file for details

## Acknowledgments

Inspiration, code snippets, etc.
* [awesome-readme](https://github.com/matiassingers/awesome-readme)
* [PurpleBooth](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
* [dbader](https://github.com/dbader/readme-template)
* [zenorocha](https://gist.github.com/zenorocha/4526327)
* [fvcproductions](https://gist.github.com/fvcproductions/1bfc2d4aecb01a834b46)
