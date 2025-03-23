# Configuration et mise en place d'un cloud

## Installation et configuration du CLI

* [Installer le client git](https://git-scm.com/) 
  * Nous allons utiliser GitBash pour nos commandes ec2
* [Installation du CLI - v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Configuration du CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html#getting-started-quickstart-existing)
* [Gestion des profiles](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-format-profile)

  ```
  [output final]
  
  aws configure 
  AWS Access Key ID [None]: key
  AWS Secret Access Key [None]: key2
  Default region name [None]: eu-central-1
  ```


## Prise en main ec2

Attention:
* Vous devez utiliser la v2 du CLI

### Affichez la liste des VPCS

* [lien vers la doc describe-vpcs](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/describe-vpcs.html)

* quel est la liste des vpcs ?

```bash
aws ec2 describe-vpcs --profile devopsteam03 --output table --region eu-central-1
```

```
[OUTPUT]
-----------------------------------------------------------
|                      DescribeVpcs                       |
+---------------------------------------------------------+
||                         Vpcs                          ||
|+----------------------+--------------------------------+|
||  CidrBlock           |  10.0.0.0/16                   ||
||  DhcpOptionsId       |  dopt-05854b009a610ac91        ||
||  InstanceTenancy     |  default                       ||
||  IsDefault           |  False                         ||
||  OwnerId             |  709024702237                  ||
||  State               |  available                     ||
||  VpcId               |  vpc-0a22d771f16ae549d         ||
|+----------------------+--------------------------------+|
|||               BlockPublicAccessStates               |||
||+------------------------------------------+----------+||
|||  InternetGatewayBlockMode                |  off     |||
||+------------------------------------------+----------+||
|||               CidrBlockAssociationSet               |||
||+----------------+------------------------------------+||
|||  AssociationId |  vpc-cidr-assoc-0fad6e9a11ccae331  |||
|||  CidrBlock     |  10.0.0.0/16                       |||
||+----------------+------------------------------------+||
||||                  CidrBlockState                   ||||
|||+-------------------+-------------------------------+|||
||||  State            |  associated                   ||||
|||+-------------------+-------------------------------+|||
|||                        Tags                         |||
||+----------------------+------------------------------+||
|||  Key                 |  Name                        |||
|||  Value               |  vpc-i346                    |||
||+----------------------+------------------------------+||

```
### Affichez la liste des subnets

* [lien vers la doc describe-subnets](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-subnets.html)

* quel est la liste des subnets ?

```bash
aws ec2 describe-subnets --profile devopsteam03 --output table --region eu-central-1
```

```
[output]
------------------------------------------------------------------------------------------------------------
|                                              DescribeSubnets                                             |
+----------------------------------------------------------------------------------------------------------+
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.10.0/28                                                           ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0c409522b892fc4bf  ||
||  SubnetId                    |  subnet-0c409522b892fc4bf                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+---------------------------+--------------------------------------------------------------------------+||
|||  Key                      |  Name                                                                    |||
|||  Value                    |  subnet-10.0.10.0/28                                                     |||
||+---------------------------+--------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.4.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-02d0c07be4b48422c  ||
||  SubnetId                    |  subnet-02d0c07be4b48422c                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.4.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.2.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-06924d9bed0d3f9fa  ||
||  SubnetId                    |  subnet-06924d9bed0d3f9fa                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.2.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.8.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-04000c6ac17aa87cd  ||
||  SubnetId                    |  subnet-04000c6ac17aa87cd                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.8.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.99.0/28                                                           ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-026ee5b4de5a53a01  ||
||  SubnetId                    |  subnet-026ee5b4de5a53a01                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+---------------------------+--------------------------------------------------------------------------+||
|||  Key                      |  Name                                                                    |||
|||  Value                    |  subnet-10.0.99.0/28                                                     |||
||+---------------------------+--------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  10                                                                     ||
||  CidrBlock                   |  10.0.0.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-007585998051b2c4a  ||
||  SubnetId                    |  subnet-007585998051b2c4a                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------------+-------------------------------------------------------------------+||
|||  Key                             |  Name                                                             |||
|||  Value                           |  public-subnet                                                    |||
||+----------------------------------+-------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.6.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0abac7e48b2a18a65  ||
||  SubnetId                    |  subnet-0abac7e48b2a18a65                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.6.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.1.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0fc3126df64eea2b9  ||
||  SubnetId                    |  subnet-0fc3126df64eea2b9                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.1.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.5.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-092ced6aa04603165  ||
||  SubnetId                    |  subnet-092ced6aa04603165                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.5.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.3.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0aaee76144e27a3dd  ||
||  SubnetId                    |  subnet-0aaee76144e27a3dd                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.3.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.9.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0ab631f69a314e92d  ||
||  SubnetId                    |  subnet-0ab631f69a314e92d                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.9.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1a                                                          ||
||  AvailabilityZoneId          |  euc1-az2                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.7.0/28                                                            ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-01cfa9e1ea9fb3d90  ||
||  SubnetId                    |  subnet-01cfa9e1ea9fb3d90                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+----------------------------+-------------------------------------------------------------------------+||
|||  Key                       |  Name                                                                   |||
|||  Value                     |  subnet-10.0.7.0/28                                                     |||
||+----------------------------+-------------------------------------------------------------------------+||


```
### Créer une table de routage

* [lien vers la doc create-route-table](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route-table.html)

* comment créer une table de routage ?

```bash
aws ec2 create-route-table --vpc-id vpc-0a22d771f16ae549d --profile devopsteam03 --output table
```
```
[output]
-------------------------------------------------------------------------
|                           CreateRouteTable                            |
+------------------+----------------------------------------------------+
|  ClientToken     |  bd6620d2-f5dd-49ed-9fe0-808ba84e7e83              |
+------------------+----------------------------------------------------+
||                             RouteTable                              ||
|+---------------+--------------------------+--------------------------+|
||    OwnerId    |      RouteTableId        |          VpcId           ||
|+---------------+--------------------------+--------------------------+|
||  709024702237 |  rtb-07bf97cd343c65b4c   |  vpc-0a22d771f16ae549d   ||
|+---------------+--------------------------+--------------------------+|
|||                              Routes                               |||
||+-----------------------+------------+--------------------+---------+||
||| DestinationCidrBlock  | GatewayId  |      Origin        |  State  |||
||+-----------------------+------------+--------------------+---------+||
|||  10.0.0.0/16          |  local     |  CreateRouteTable  |  active |||
||+-----------------------+------------+--------------------+---------+||
```
### Associer une table de routage

* [lien vers la doc associate-route-table](https://docs.aws.amazon.com/cli/latest/reference/ec2/associate-route-table.html)

* comment associer une table de routage à un sous-réseau?

```bash
aws ec2 associate-route-table --route-table-id rtb-07bf97cd343c65b4c --subnet-id subnet-0aaee76144e27a3dd --profile devopsteam03 --output table
```
```
[output]
-------------------------------------------------
|              AssociateRouteTable              |
+----------------+------------------------------+
|  AssociationId |  rtbassoc-0a41421456eb54417  |
+----------------+------------------------------+
||              AssociationState               ||
|+----------------+----------------------------+|
||  State         |  associated                ||
|+----------------+----------------------------+|
```

### Créer une route en direction du serveur SSH

* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
aws ec2 create-route --route-table-id rtb-07bf97cd343c65b4c --destination-cidr-block 0.0.0.0/0 --gateway-id igw-059306bf876cf19f6 --profile devopsteam03
```
```
[output]
{
    "Return": true
}
```

### Ajout tagname pour la table de routage

* [lien vers la doc create-tags](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-tags.html)

* comment créer et ajouter un tage à la table de routage?
```bash
aws ec2 create-tags --resources rtb-07bf97cd343c65b4c --tags Key=Name,Value=Group03 --profile devopsteam03 --region eu-central-1
```
```
```

### Créer un groupe de sécurité sous-réseau
* [lien vers la doc create-security-group](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-security-group.html)

* comment créer un groupe de sécurité de sous-réseau ?

```bash
aws ec2 create-security-group --group-name securgrp-i346-devopsteam03 --description "securgrp-i346-devopsteam03" --profile devopsteam03 --region eu-central-1 --vpc-id vpc-0a22d771f16ae549d

```
```
{
    "GroupId": "sg-086f8ce047d5b890b",
    "SecurityGroupArn": "arn:aws:ec2:eu-central-1:709024702237:security-group/sg-086f8ce047d5b890b"
}
```

### Créer et mettre en ligne des clès privés
* [lien vers la doc create-key-pairs](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/create-key-pair.html)

* comment créer une paire de clés ?

```
aws ec2 create-key-pair --key-name KEY-I346-SUB-DEVOPSTEAM03 --key-type rsa --key-format pem --region eu-central-1 --profile devopsteam03 --output text > KEY-I346-SUB-DEVOPSTEAM03.pem  
```
```
```
Nous avons obtenu un fichier .pem contenant notre clé privée

### Déployer une instance linux
* [lien vers la doc run-instance](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/run-instances.html)

* comment lancer une instance linux ?

```bash
aws ec2 run-instances --image-id ami-0584590e5f0e97daa --instance-type t2.micro --key-name KEY-I346-SUB-DEVOPSTEAM03 --subnet-id subnet-0aaee76144e27a3dd --security-group-ids sg-086f8ce047d5b890b --private-ip-address 10.0.3.10 --region eu-central-1 --profile devopsteam03 --output table
```
```
-----------------------------------------------------------------------------
|                               RunInstances                                |
+-------------------------------+-------------------------------------------+
|  OwnerId                      |  709024702237                             |
|  ReservationId                |  r-0e32059885aab2260                      |
+-------------------------------+-------------------------------------------+
||                                Instances                                ||
|+--------------------------+----------------------------------------------+|
||  AmiLaunchIndex          |  0                                           ||
||  Architecture            |  x86_64                                      ||
||  ClientToken             |  d05a8306-9853-44ad-bf80-c5e94717698d        ||
||  CurrentInstanceBootMode |  legacy-bios                                 ||
||  EbsOptimized            |  False                                       ||
||  EnaSupport              |  True                                        ||
||  Hypervisor              |  xen                                         ||
||  ImageId                 |  ami-0584590e5f0e97daa                       ||
||  InstanceId              |  i-0036e5e28eddfcd86                         ||
||  InstanceType            |  t2.micro                                    ||
||  KeyName                 |  KEY-I346-SUB-DEVOPSTEAM03                   ||
||  LaunchTime              |  2025-03-19T10:31:43+00:00                   ||
||  PrivateDnsName          |  ip-10-0-3-11.eu-central-1.compute.internal  ||
||  PrivateIpAddress        |  10.0.3.11                                   ||
||  PublicDnsName           |                                              ||
||  RootDeviceName          |  /dev/xvda                                   ||
||  RootDeviceType          |  ebs                                         ||
||  SourceDestCheck         |  True                                        ||
||  StateTransitionReason   |                                              ||
||  SubnetId                |  subnet-0aaee76144e27a3dd                    ||
||  VirtualizationType      |  hvm                                         ||
||  VpcId                   |  vpc-0a22d771f16ae549d                       ||
|+--------------------------+----------------------------------------------+|
|||                   CapacityReservationSpecification                    |||
||+---------------------------------------------------------+-------------+||
|||  CapacityReservationPreference                          |  open       |||
||+---------------------------------------------------------+-------------+||
|||                              CpuOptions                               |||
||+-------------------------------------------------------+---------------+||
|||  CoreCount                                            |  1            |||
|||  ThreadsPerCore                                       |  1            |||
||+-------------------------------------------------------+---------------+||
|||                            EnclaveOptions                             |||
||+--------------------------------------+--------------------------------+||
|||  Enabled                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                          MaintenanceOptions                           |||
||+-----------------------------------------+-----------------------------+||
|||  AutoRecovery                           |  default                    |||
||+-----------------------------------------+-----------------------------+||
|||                            MetadataOptions                            |||
||+-------------------------------------------------+---------------------+||
|||  HttpEndpoint                                   |  enabled            |||
|||  HttpProtocolIpv6                               |  disabled           |||
|||  HttpPutResponseHopLimit                        |  1                  |||
|||  HttpTokens                                     |  optional           |||
|||  InstanceMetadataTags                           |  disabled           |||
|||  State                                          |  pending            |||
||+-------------------------------------------------+---------------------+||
|||                              Monitoring                               |||
||+-----------------------------+-----------------------------------------+||
|||  State                      |  disabled                               |||
||+-----------------------------+-----------------------------------------+||
|||                           NetworkInterfaces                           |||
||+------------------------------+----------------------------------------+||
|||  Description                 |                                        |||
|||  InterfaceType               |  interface                             |||
|||  MacAddress                  |  0a:8f:10:b3:eb:6d                     |||
|||  NetworkInterfaceId          |  eni-09560c21bad3ff022                 |||
|||  OwnerId                     |  709024702237                          |||
|||  PrivateIpAddress            |  10.0.3.11                             |||
|||  SourceDestCheck             |  True                                  |||
|||  Status                      |  in-use                                |||
|||  SubnetId                    |  subnet-0aaee76144e27a3dd              |||
|||  VpcId                       |  vpc-0a22d771f16ae549d                 |||
||+------------------------------+----------------------------------------+||
||||                             Attachment                              ||||
|||+----------------------------+----------------------------------------+|||
||||  AttachTime                |  2025-03-19T10:31:43+00:00             ||||
||||  AttachmentId              |  eni-attach-0ff14ac342090b092          ||||
||||  DeleteOnTermination       |  True                                  ||||
||||  DeviceIndex               |  0                                     ||||
||||  NetworkCardIndex          |  0                                     ||||
||||  Status                    |  attaching                             ||||
|||+----------------------------+----------------------------------------+|||
||||                               Groups                                ||||
|||+-------------------+-------------------------------------------------+|||
||||  GroupId          |  sg-086f8ce047d5b890b                           ||||
||||  GroupName        |  securgrp-i346-devopsteam03                     ||||
|||+-------------------+-------------------------------------------------+|||
||||                              Operator                               ||||
|||+-------------------------------------+-------------------------------+|||
||||  Managed                            |  False                        ||||
|||+-------------------------------------+-------------------------------+|||
||||                         PrivateIpAddresses                          ||||
|||+-----------------------------------------+---------------------------+|||
||||  Primary                                |  True                     ||||
||||  PrivateIpAddress                       |  10.0.3.11                ||||
|||+-----------------------------------------+---------------------------+|||
|||                               Operator                                |||
||+--------------------------------------+--------------------------------+||
|||  Managed                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                               Placement                               |||
||+-------------------------------------+---------------------------------+||
|||  AvailabilityZone                   |  eu-central-1c                  |||
|||  GroupName                          |                                 |||
|||  Tenancy                            |  default                        |||
||+-------------------------------------+---------------------------------+||
|||                         PrivateDnsNameOptions                         |||
||+------------------------------------------------------+----------------+||
|||  EnableResourceNameDnsAAAARecord                     |  False         |||
|||  EnableResourceNameDnsARecord                        |  False         |||
|||  HostnameType                                        |  ip-name       |||
||+------------------------------------------------------+----------------+||
|||                            SecurityGroups                             |||
||+--------------------+--------------------------------------------------+||
|||  GroupId           |  sg-086f8ce047d5b890b                            |||
|||  GroupName         |  securgrp-i346-devopsteam03                      |||
||+--------------------+--------------------------------------------------+||
|||                                 State                                 |||
||+-----------------------------+-----------------------------------------+||
|||  Code                       |  0                                      |||
|||  Name                       |  pending                                |||
||+-----------------------------+-----------------------------------------+||
|||                              StateReason                              |||
||+----------------------------------+------------------------------------+||
|||  Code                            |  pending                           |||
|||  Message                         |  pending                           |||
||+----------------------------------+------------------------------------+||

```

### Déployer une instance windows
* [lien vers la doc run-instance](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/run-instances.html)

* comment lancer une instance windows ?

```bash
aws ec2 run-instances --image-id ami-045114d716addc65d --instance-type t3.micro --key-name KEY-I346-SUB-DEVOPSTEAM03 --subnet-id subnet-0aaee76144e27a3dd --security-group-ids sg-086f8ce047d5b890b --private-ip-address 10.0.3.10 --region eu-central-1 --profile devopsteam03 --output table
```
```
-----------------------------------------------------------------------------
|                               RunInstances                                |
+-------------------------------+-------------------------------------------+
|  OwnerId                      |  709024702237                             |
|  ReservationId                |  r-02e8d063aba9ede5c                      |
+-------------------------------+-------------------------------------------+
||                                Instances                                ||
|+--------------------------+----------------------------------------------+|
||  AmiLaunchIndex          |  0                                           ||
||  Architecture            |  x86_64                                      ||
||  BootMode                |  uefi                                        ||
||  ClientToken             |  d9c6e8a3-b635-4f6f-b7ed-5aed8adda954        ||
||  CurrentInstanceBootMode |  uefi                                        ||
||  EbsOptimized            |  False                                       ||
||  EnaSupport              |  True                                        ||
||  Hypervisor              |  xen                                         ||
||  ImageId                 |  ami-045114d716addc65d                       ||
||  InstanceId              |  i-02722195c013be8b5                         ||
||  InstanceType            |  t3.micro                                    ||
||  KeyName                 |  KEY-I346-SUB-DEVOPSTEAM03                   ||
||  LaunchTime              |  2025-03-18T14:50:32+00:00                   ||
||  Platform                |  windows                                     ||
||  PrivateDnsName          |  ip-10-0-3-10.eu-central-1.compute.internal  ||
||  PrivateIpAddress        |  10.0.3.10                                   ||
||  PublicDnsName           |                                              ||
||  RootDeviceName          |  /dev/sda1                                   ||
||  RootDeviceType          |  ebs                                         ||
||  SourceDestCheck         |  True                                        ||
||  StateTransitionReason   |                                              ||
||  SubnetId                |  subnet-0aaee76144e27a3dd                    ||
||  VirtualizationType      |  hvm                                         ||
||  VpcId                   |  vpc-0a22d771f16ae549d                       ||
|+--------------------------+----------------------------------------------+|
|||                   CapacityReservationSpecification                    |||
||+---------------------------------------------------------+-------------+||
|||  CapacityReservationPreference                          |  open       |||
||+---------------------------------------------------------+-------------+||
|||                              CpuOptions                               |||
||+-------------------------------------------------------+---------------+||
|||  CoreCount                                            |  1            |||
|||  ThreadsPerCore                                       |  2            |||
||+-------------------------------------------------------+---------------+||
|||                            EnclaveOptions                             |||
||+--------------------------------------+--------------------------------+||
|||  Enabled                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                          MaintenanceOptions                           |||
||+-----------------------------------------+-----------------------------+||
|||  AutoRecovery                           |  default                    |||
||+-----------------------------------------+-----------------------------+||
|||                            MetadataOptions                            |||
||+-------------------------------------------------+---------------------+||
|||  HttpEndpoint                                   |  enabled            |||
|||  HttpProtocolIpv6                               |  disabled           |||
|||  HttpPutResponseHopLimit                        |  2                  |||
|||  HttpTokens                                     |  required           |||
|||  InstanceMetadataTags                           |  disabled           |||
|||  State                                          |  pending            |||
||+-------------------------------------------------+---------------------+||
|||                              Monitoring                               |||
||+-----------------------------+-----------------------------------------+||
|||  State                      |  disabled                               |||
||+-----------------------------+-----------------------------------------+||
|||                           NetworkInterfaces                           |||
||+------------------------------+----------------------------------------+||
|||  Description                 |                                        |||
|||  InterfaceType               |  interface                             |||
|||  MacAddress                  |  0a:87:73:34:9d:6b                     |||
|||  NetworkInterfaceId          |  eni-012050d96f1a13a2c                 |||
|||  OwnerId                     |  709024702237                          |||
|||  PrivateIpAddress            |  10.0.3.10                             |||
|||  SourceDestCheck             |  True                                  |||
|||  Status                      |  in-use                                |||
|||  SubnetId                    |  subnet-0aaee76144e27a3dd              |||
|||  VpcId                       |  vpc-0a22d771f16ae549d                 |||
||+------------------------------+----------------------------------------+||
||||                             Attachment                              ||||
|||+----------------------------+----------------------------------------+|||
||||  AttachTime                |  2025-03-18T14:50:32+00:00             ||||
||||  AttachmentId              |  eni-attach-011fc8475344d508b          ||||
||||  DeleteOnTermination       |  True                                  ||||
||||  DeviceIndex               |  0                                     ||||
||||  NetworkCardIndex          |  0                                     ||||
||||  Status                    |  attaching                             ||||
|||+----------------------------+----------------------------------------+|||
||||                               Groups                                ||||
|||+-------------------+-------------------------------------------------+|||
||||  GroupId          |  sg-086f8ce047d5b890b                           ||||
||||  GroupName        |  securgrp-i346-devopsteam03                     ||||
|||+-------------------+-------------------------------------------------+|||
||||                              Operator                               ||||
|||+-------------------------------------+-------------------------------+|||
||||  Managed                            |  False                        ||||
|||+-------------------------------------+-------------------------------+|||
||||                         PrivateIpAddresses                          ||||
|||+-----------------------------------------+---------------------------+|||
||||  Primary                                |  True                     ||||
||||  PrivateIpAddress                       |  10.0.3.10                ||||
|||+-----------------------------------------+---------------------------+|||
|||                               Operator                                |||
||+--------------------------------------+--------------------------------+||
|||  Managed                             |  False                         |||
||+--------------------------------------+--------------------------------+||
|||                               Placement                               |||
||+-------------------------------------+---------------------------------+||
|||  AvailabilityZone                   |  eu-central-1c                  |||
|||  GroupName                          |                                 |||
|||  Tenancy                            |  default                        |||
||+-------------------------------------+---------------------------------+||
|||                         PrivateDnsNameOptions                         |||
||+------------------------------------------------------+----------------+||
|||  EnableResourceNameDnsAAAARecord                     |  False         |||
|||  EnableResourceNameDnsARecord                        |  False         |||
|||  HostnameType                                        |  ip-name       |||
||+------------------------------------------------------+----------------+||
|||                            SecurityGroups                             |||
||+--------------------+--------------------------------------------------+||
|||  GroupId           |  sg-086f8ce047d5b890b                            |||
|||  GroupName         |  securgrp-i346-devopsteam03                      |||
||+--------------------+--------------------------------------------------+||
|||                                 State                                 |||
||+-----------------------------+-----------------------------------------+||
|||  Code                       |  0                                      |||
|||  Name                       |  pending                                |||
||+-----------------------------+-----------------------------------------+||
|||                              StateReason                              |||
||+----------------------------------+------------------------------------+||
|||  Code                            |  pending                           |||
|||  Message                         |  pending                           |||
||+----------------------------------+------------------------------------+||
```

### Configurer accès SSH (tunnel à la DMZ)
* [lien vers la doc connect-linux-inst-ssh](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-linux-inst-ssh.html)

* comment configurer le tunnel SSH ?

```bash
ssh devopsteam03@52.59.181.213 -i KEY-I346-DMZ-DEVOPSTEAM03.pem -L 23:10.0.3.11:22 -L 3399:10.0.3.10:3389
```
```
Linux ip-10-0-0-10 6.1.0-31-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.128-1 (2025-02-07) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Wed Mar 19 12:02:17 2025 from 193.5.240.9
```

### Autoriser le groupe de sécurité
* [lien vers la doc authorize-security-group-ingress](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/authorize-security-group-ingress.html)

* comment autoriser l'accès au groupe de sécurité ?

```bash
aws ec2 authorize-security-group-ingress --group-id sg-086f8ce047d5b890b --ip-permissions "IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges=[{CidrIp=10.0.0.0/28,Description=SSH-FROM-DMZ}]" --region eu-central-1 --profile devopsteam03 --output table
```
```
---------------------------------------------------------------------------------------------------------------
|                                        AuthorizeSecurityGroupIngress                                        |
+------------------------------------------------------------+------------------------------------------------+
|  Return                                                    |  True                                          |
+------------------------------------------------------------+------------------------------------------------+
||                                            SecurityGroupRules                                             ||
|+----------------------+------------------------------------------------------------------------------------+|
||  CidrIpv4            |  10.0.0.0/28                                                                       ||
||  Description         |  SSH-FROM-DMZ                                                                      ||
||  FromPort            |  22                                                                                ||
||  GroupId             |  sg-086f8ce047d5b890b                                                              ||
||  GroupOwnerId        |  709024702237                                                                      ||
||  IpProtocol          |  tcp                                                                               ||
||  IsEgress            |  False                                                                             ||
||  SecurityGroupRuleArn|  arn:aws:ec2:eu-central-1:709024702237:security-group-rule/sgr-043a33f1a601a6cb3   ||
||  SecurityGroupRuleId |  sgr-043a33f1a601a6cb3                                                             ||
||  ToPort              |  22                                                                                ||
|+----------------------+------------------------------------------------------------------------------------+|
```

### Obtenir le mot de passe Windows
* [lien vers la doc get-password-data](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/get-password-data.html)

* comment obtenir le mot de passe de notre instance Windows ?

```bash
aws ec2 get-password-data --instance-id i-02722195c013be8b5 --priv-launch-key KEY-I346-SUB-DEVOPSTEAM03.pem --profile devopsteam03 --region eu-central-1
```
```
{
    "InstanceId": "i-02722195c013be8b5",
    "Timestamp": "2025-03-18T14:56:59+00:00",
    "PasswordData": "****"
}
```

### Tester les accès linux inbound
* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
```
```
[output]
```

### Tester les accès linux outbound
* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
```
```
[output]
```

### Tester les accès windows inbound
* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
```
```
[output]
```

### Tester les accès windows outbound
* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
```
```
[output]
```

### Start ec2
* [lien vers la doc start-instances](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/start-instances.html)

* comment démarré son instance ec2 ?

```bash
aws ec2 start-instances --instance-ids i-0036e5e28eddfcd86 --profile devopsteam03 --region eu-central-1
```
```
{
    "StartingInstances": [
        {
            "InstanceId": "i-0036e5e28eddfcd86",
            "CurrentState": {
                "Code": 0,
                "Name": "pending"
            },
            "PreviousState": {
                "Code": 80,
                "Name": "stopped"
            }
        }
    ]
}
```

### Stop ec2
* [lien vers la doc stop-instances](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/stop-instances.html)

* comment stoper une instance ?

```bash
aws ec2 stop-instances --instance-ids i-0036e5e28eddfcd86 --profile devopsteam03 --region eu-central-1
```
```
{
    "StoppingInstances": [
        {
            "InstanceId": "i-0036e5e28eddfcd86",
            "CurrentState": {
                "Code": 64,
                "Name": "stopping"
            },
            "PreviousState": {
                "Code": 16,
                "Name": "running"
            }
        }
    ]
}
```

### Terminate ec2
* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
```
```
[output]
```

### Nettoyer ce que l'on a fait 
* [lien vers la doc create-route](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-route.html)

* comment créer une route qui target le serveur ssh ?

```bash
```
```
[output]
```





# Liste de question révisions test

### 1. à quoi sert un vpc ?

### 2. pourquoi utiliser des sous réseaux et pas directement le vpc?

### 3. pourquoi ne pas connecter le sous réseau privé directement au net ?

### 4. quel est le mot clé pour associer une route table à un subnet ?

### 5. à quoi sert une route table ?

### 6. qu'est ce que c'est une route ?

### 7. quel est la différence entre s3 et ec2 ?

### 8. à quoi sert ec2

### 9. quel est la différenec entre un cloud privé et un cloud communautaire ?

### 10. quel est l'erreur dans cette commande : aws ec2 create-route-table --vpcid vpc-0a22d771f16ae549d --profile devopsteam03 --output table
