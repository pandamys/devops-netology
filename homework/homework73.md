# Задача 2
1. Выполнил команду.\
```terraform init```
2. Создал два воркспейса
```xml
terraform workspace new stage
terraform workspace new prod
```
3. Добавил
```xml
locals {
    instance_type_map = {
        stage = "t3.micro"
        prod = "t3.large"
    }
}
```
4. Добавил
```xml
 instance_count_map = {
        stage = 1
        prod = 2
    }
```

6. Добавил
```xml
lifecycle {
    create_before_destroy = true
}
```

# Выводы команд
terraform workspace list
```xml
vagrant@vagrant:~/tf$ vagrant@vagrant:~/tf$ terraform workspace list
  default
* prod
  stage
```

terraform plan выполнить для aws не получается, итоговый tf файл такой:
```xml
terraform {
        required_providers {
            aws = {
                source = "hasicorp/aws"
                version = "~> 3.0"
            }
        }

        provider "aws" {
            access_key = ""
            secret_key = ""
            region = "us-east-1"
        }

        locals {
            instance_type_map = {
                stage = "t3.micro"
                prod = "t3.large"
            }
    
            instance_count_map = {
                stage = 1
                prod = 2
            }
        }

        data "aws_ami" "amazon-linux-2" {
            owners = ["amazon"]
        }

        resource "aws_instance" "web" {
            ami = data.aws_ami.amazon-linux-2.id
            instance_type = local.instance_type_map[terraform.workspace]
            count = local.instance_count_map[terraform.workspace]

            lifecycle {
                create_before_destroy = true
            }
        }
}
```