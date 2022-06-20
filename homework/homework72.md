# Задача 1
Настроил яндекс.клауд, подготовил всё к подключению к облаку.
Авторизационный токен поместил в переменные окружения.

# Задача 2
2. Зарегистрировал провайдер
3. Токен поместил в переменную окружения.
```xml
export YC_TOKEN=`yc iam create-token`
```
4. Не применимо к яндексу
5. Создал ресурс.

# Итоговая конфигурация
Файл main.tf
```terraform
provider "yandex" {
  cloud_id  = "b1g4vbedphcdqtu6gsm0"
  folder_id = "b1glhgk4h39lcj1meak9"
  zone      = "ru-central1-a"
}

resource "yandex_compute_instance" "vm-1" {
  name = "terraform1"

  resources {
    cores  = 2
    memory = 2
  }

  boot_disk {
    initialize_params {
      image_id = "fd8hguc7o9hhr5bcvhql"
    }
  }

  network_interface {
    subnet_id = yandex_vpc_subnet.subnet-1.id
    nat       = true
  }

  metadata = {
    user-data = "${file("~/yc-terra/meta.yml")}"
  }
}

resource "yandex_vpc_network" "network-1" {
  name = "network1"
}

resource "yandex_vpc_subnet" "subnet-1" {
  name           = "subnet1"
  zone           = "ru-central1-a"
  network_id     = yandex_vpc_network.network-1.id
  v4_cidr_blocks = ["192.168.10.0/24"]
}

output "internal_ip_address_vm_1" {
  value = yandex_compute_instance.vm-1.network_interface.0.ip_address
}

output "external_ip_address_vm_1" {
  value = yandex_compute_instance.vm-1.network_interface.0.nat_ip_address
}
```

versions.tf
```terraform
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
  required_version = ">= 0.13"
}
```

meta.yml
```terraform
#cloud-config
users:
  - name: panda
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh_authorized_keys:
      - ssh-rsa AAAAB3Nza...ZcCzP/9 vagrant@vagrant
```