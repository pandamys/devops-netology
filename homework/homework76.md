# Задача 1
1. Все resources перечисленны тут
```doctest
https://github.com/hashicorp/terraform-provider-aws/blob/6a89c8517ca5a5e65efcbe4d3ca03aea3c65cb53/internal/provider/provider.go#L906
```
Все data_source
```doctest
https://github.com/hashicorp/terraform-provider-aws/blob/6a89c8517ca5a5e65efcbe4d3ca03aea3c65cb53/internal/provider/provider.go#L423
```
2. По пунктам
- ConflictsWith: []string{"name_prefix"},
```doctest
https://github.com/hashicorp/terraform-provider-aws/blob/6a89c8517ca5a5e65efcbe4d3ca03aea3c65cb53/internal/service/sqs/queue.go#L87
```
- Максимальная длинна имени и регулярное выражение.
```doctest
https://github.com/hashicorp/terraform-provider-aws/blob/6a89c8517ca5a5e65efcbe4d3ca03aea3c65cb53/internal/service/sqs/queue.go#L424
```
Получается, что имя должно соответствовать одному из двух правил:
- Если fifo, то от 1 до 75 символов и оканчиваться на .fifo;
- Если не fifo, то быть от 1 до 80 символов

А также состоять из латинских букв разного регистра, может содержать - или _