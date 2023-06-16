eks-admin tools
==============
This tool is for EKS cluster.

If you're interested in infrastructure as Code(IaC), I would recommend using Terraform.  
This tool is specifically designed for learning about EKS.

## Installation
### Homebrew
```
brew tap masa0221/tap && brew install eks-admin
```

### Manual install
```sh
sudo curl -s https://raw.githubusercontent.com/masa0221/eks-operations/HEAD/eks-admin -o /usr/local/bin/eks-admin && chmod +x /usr/local/bin/eks-admin
```

## How to use

### 1. Set up an SSO account on AWS
Enable the AWS Identity Center and create permission sets for both AWS administrator and EKS administrator.


### 2. Configure the ./eks-admin file 
You can modify parameters for EKS operation in the ./eks-admin file.


### 3. Create an EKS cluster
#### 3.1 Generate the required policies
```
eks-admin login eksadmin
```
NOTE: This step is necessary to obtain the eksadmin identity.

```
eks-admin policy generate
```

#### 3.2 Create the EKS creator role and attach the policy for the EKS creator
```
eks-admin login admin
```
NOTE: This step is necessary to operate IAM resourece

```
eks-admin role create 
```
NOTE: This command involves three steps. First, we're create the role, then we creating the policy to attach to the role. Finally, we attach the policy to the role.
The role created in this step is configured to only allow the eksadmin to assume it.

#### 3.3 Create an EKS cluster
```
eks-admin login eksadmin
```
NOTE: The eksadmin is the only role that can assume the intented role.

```
eks-admin cluster up
```
NOTE: It takes approximately 15 minutes.


### 4. Delete EKS cluster
```
eks-admin cluster down
```
 

## Ref.
- [A quick path to Amazon EKS single sign-on using AWS SSO | Containers](https://aws.amazon.com/jp/blogs/containers/a-quick-path-to-amazon-eks-single-sign-on-using-aws-sso/)
- [AWS SSO を用いた Amazon EKS への迅速なシングルサインオン | Amazon Web Services ブログ](https://aws.amazon.com/jp/blogs/news/a-quick-path-to-amazon-eks-single-sign-on-using-aws-sso/)


## NOTE
I TAKE NO RESPOSIBILITY FOR ANY CONSEQUENCES OR ACTIONS THAT MAY OCCUR FROM USING THIS TOOL. IF YOU WISH TO USE IT, PLEASE MAKE SURE YOU UNDERSTAND WHAT IT DOES BEFORE PROCEEDING.
