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

terraform plan
```xml

```