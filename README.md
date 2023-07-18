# Развертывание Shadowsocks Rust

Данный Ansible playbook предназначен для развертывания Shadowsocks Rust на целевых Linux-хостах.

## Требования
- Ansible
- Linux-хосты

## Использование
1. Обновите переменную `MYHOSTS` при запуске в командной строке или в файле инвентаря (inventory.ini) с целевыми хостами, на которых вы хотите развернуть Shadowsocks Rust.

2. Запустите playbook:
   ```
   ansible-playbook deploy_shadowsoks_rust.yml --extra-var "MYHOSTS="Наименование вашей группы"" --vault-password-file=password.txt
  
   ```
#### Hеобходимо поместить пароль vault в файл password.txt
3. Playbook установит необходимые зависимости, загрузит архив Shadowsocks Rust, извлечет его, загрузит плагин V2Ray, создаст директорию конфигурации, сгенерирует файл `ssserver.service` и файл `config.json`, а затем запустит сервер Shadowsocks Rust.

## Настройка
Вы можете настроить развертывание, изменив следующие переменные в playbook в каталоге `roles/defaults/main.yml`:

- `destin_folder`: Каталог, в котором будет создан файл `ssserver.service`.
- `destin_folder_shadowsocks`: Каталог, в котором будет создан файл `config.json`.
- `shadowsocks_rust`: URL архива Shadowsocks Rust.
- `V2Ray_plugin`: URL плагина V2Ray.
- `port_enable`: Переменная открывающая порт использует шаблон `config.j2` и playbook `roles/tasks/main.yml` - name: Open port.
- `port_disable`: Переменная закрывающая порт использует шаблон `config.j2` и playbook `roles/tasks/main.yml` - name: Open port.
- `proto_enable`: Переменная включает протокол использует шаблон `config.j2` и playbook `roles/tasks/main.yml` - name: Open port.
- `proto_disable`: Переменная отключает протокол использует шаблон `config.j2` и playbook `roles/tasks/main.yml` - name: Open port.
Так же неоходимо настроить переменную в playbook в каталоге `roles/vars/main.yml`:
- `shadowsoks_password использует шаблон `config.j2`, предварительно зашифрован vault.
## Ограничения
- Этот playbook предполагает, что целевые хосты работают под управлением операционной системы Linux.
- Убедитесь, что необходимые порты и сетевые настройки правильно настроены для работы Shadowsocks Rust.

Обратите внимание, что playbook может потребовать дополнительной настройки в соответствии с вашим конкретным окружением и требованиями.


