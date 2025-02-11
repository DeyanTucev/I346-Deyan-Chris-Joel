# Laboratoire S3

## Installation et configuration du CLI

* [Installer le client git](https://git-scm.com/)
  * Git bash vous embarque de nombreuses commandes Linux utiles pour s'entrainer avec S3 (cat, grep, touch, ls)
* [Installation du CLI - v2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [Configuration du CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-quickstart.html#getting-started-quickstart-existing)
  * Les clés vous ont été partagées par oneDrive
* [Gestion des profiles](https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html#cli-configure-files-format-profile)
  * Vous devez créer un profile du nom de votre équipe et l'utiliser pour toute les futures commandes
  ```
  aws configure 
  AWS Access Key ID [None]: key
  AWS Secret Access Key [None]: key2
  Default region name [None]: eu-central-1
  ```

## IAM Policy

Voici la "policy" qui vous a été attribuée:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListAllMyBuckets",
            "Resource": "arn:aws:s3:::*"
        },
        {
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
            ],
            "Resource": "arn:aws:s3:::devopsteam<XX>-i346/*" //XX -> devopsteam number
        }
    ]
}
```

## Exploiter un S3

Attention:
* Vous devez utiliser la v2 du CLI
* Le client offre soit la commande s3, soit s3api. En priorité vous devez essayer "s3".

### Créer un bucket

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* Le bucket existe-t-il ?

```bash
aws s3 ls --profile devopsteam03-i346 | grep "devopsteam*"
```

```
[OUTPUT]
2025-01-27 22:23:30 devopsteam01-i346
2025-01-27 22:28:03 devopsteam02-i346
2025-01-27 22:28:05 devopsteam03-i346
2025-01-27 22:28:06 devopsteam04-i346
2025-01-27 22:28:08 devopsteam05-i346
2025-01-27 22:28:09 devopsteam06-i346
2025-01-27 22:28:11 devopsteam07-i346
2025-01-27 22:28:13 devopsteam08-i346
2025-01-27 22:28:14 devopsteam09-i346
2025-01-27 22:28:16 devopsteam10-i346
2025-02-03 19:32:33 devopsteam99-i346
```

* Créer un bucket (via un compte admin)

```bash
aws s3 mb s3://devopsteam99-i346 --region eu-central-1 --profile s3-admin
```

```
[OUTPUT]
make_bucket: devopsteam99-i346
```


### Uploader un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3 ls s3://devopsteam03-i346 --profile devopsteam03
```

```
[OUTPUT]
An error occurred (AccessDenied) when calling the ListObjectsV2 operation: User: arn:aws:iam::709024702237:user/devopsteam03-i346 
is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::devopsteam03-i346" because no identity-based policy allows the s3:ListBucket action

```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 cp U:\test.txt s3://devopsteam03-i346 --profile devopsteam03

```

```
[OUTPUT]
upload: U:\test.txt to s3://devopsteam03-i346/test.txt

```

### Uploader un répertoire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object --bucket devopsteam03-i346 --key dossierTest dossierTest --profile devopsteam03

```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:40:53+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}


```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
 aws s3 cp --recursive U:\dossierTest s3://devopsteam03-i346 --profile devopsteam03
```
l'output était vide, donc pour vérifier que le dossier avait bien été créé j'ai upload un fichier dedans avec cette commande :
aws s3 cp U:\test.txt s3://devopsteam03-i346/dossierTest --profile devopsteam03
```
[OUTPUT]
upload: U:\test.txt to s3://devopsteam03-i346/dossierTest
```

### Lister le contenu d'un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object --bucket devopsteam03-i346 --key dossierTest dossierTest --profile devopsteam03
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:40:53+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3api get-object --bucket devopsteam03-i346 --key s3://devopsteam03-i346/dossierTest dossierTest --profile devopsteam03

```

```
[OUTPUT]
An error occurred (AccessDenied) when calling the GetObject operation: User: arn:aws:iam::709024702237:user/devopsteam03-i346 
is not authorized to perform: s3:ListBucket on resource: "arn:aws:s3:::devopsteam03-i346" because no 
identity-based policy allows the s3:ListBucket action
```

### Synchroniser un répertoire local de sa machine avec un bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object --bucket devopsteam03-i346 --key dossierTest dossierTest --profile devopsteam03
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:40:53+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3 sync U:/dossierTest s3://devopsteam03-i346 --profile devopsteam03
```

```
[OUTPUT]
fatal error: An error occurred (AccessDenied) when calling the ListObjectsV2 operation: 
User: arn:aws:iam::709024702237:user/devopsteam03-i346 is not authorized to perform: s3:ListBucket on 
resource: "arn:aws:s3:::devopsteam03-i346" because no identity-based policy allows the s3:ListBucket action

```

### Publier un fichier présent sur un bucket en générant un lien (url) temporaire

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
aws s3api get-object --bucket devopsteam03-i346 --key dossierTest dossierTest --profile devopsteam03
```

```
[OUTPUT]
{
    "AcceptRanges": "bytes",
    "LastModified": "2025-02-05T10:40:53+00:00",
    "ContentLength": 0,
    "ETag": "\"d41d8cd98f00b204e9800998ecf8427e\"",
    "ChecksumCRC64NVME": "AAAAAAAAAAA=",
    "ChecksumType": "FULL_OBJECT",
    "ContentType": "text/plain",
    "ServerSideEncryption": "AES256",
    "Metadata": {}
}
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

### Supprimer un fichier

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
aws s3api delete-object --bucket devopsteam03-i346 --key test.txt --profile devopsteam03

```

```
[OUTPUT]
//TODO
```

### Vider un "repertoire"

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash


```

```
[OUTPUT]

```

### Extraire uniquement les metadonnées d'un objet

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

### Vider le bucket

//TODO en suivant le modèle livré sous "Créer un bucket"

* [AWS Official Doc - Create Bucket](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/s3/mb.html#examples)

* [Vérifier l'état du bucket avant votre commande]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

* [La commande à réaliser pour effecuter l'action demandée]

```bash
//TODO
```

```
[OUTPUT]
//TODO
```

---

## Questions d'analyse

Consigne : répondre en utilisant des sources officielles et en vous appuyant dessus pour répondre.

### Pourquoi est-il déconseillé de détruire un bucket S3 selon AWS ?

* [Sources AWS]

[Votre réponse]

### Quelle est la différence entre un Bucket S3 et Glacier ?

* [Sources AWS]

[Votre réponse]

### Reprenez l'IAM "Policy" et expliquer ce que vous pouvez en déduire au niveau des droits qui vous sont alloués

Consigne : Reprenez la "policy" et documenter chaque ligne