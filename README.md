# Домашнее задание к занятию "`Название занятия`" - `Фамилия и имя студента`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. В личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
# это kafka_setup.yml
---
- name: Download and extract Apache Kafka archive
  hosts: all
  become: true
  vars:
    kafka_version: "3.8.0"
    kafka_url: "https://archive.apache.org/dist/kafka/{{ kafka_version }}/kafka_2.13-{{ kafka_version }}.tgz"
    kafka_dest_dir: "/opt/kafka"
    kafka_archive_name: "kafka_2.13-{{ kafka_version }}.tgz"

  tasks:
    - name: Create destination directory for Kafka
      file:
        path: "{{ kafka_dest_dir }}"
        state: directory
        mode: '0755'

    - name: Download Kafka binary archive
      get_url:
        url: "{{ kafka_url }}"
        dest: "/tmp/{{ kafka_archive_name }}"
        mode: '0644'

    - name: Extract Kafka archive to destination directory
      unarchive:
        src: "/tmp/{{ kafka_archive_name }}"
        dest: "{{ kafka_dest_dir }}"
        remote_src: yes
        creates: "{{ kafka_dest_dir }}/kafka_{{ kafka_version }}"

    - name: Clean up downloaded archive
      file:
        path: "/tmp/{{ kafka_archive_name }}"
        state: absent
# это tuned_setup.yml

---
- name: Install and enable tuned service
  hosts: all
  become: true

  tasks:
    - name: Install tuned package from default repository
      apt:
        name: tuned
        state: present
      when: ansible_os_family == "Debian"
   
    - name: Enable tuned to start on boot
      systemd:
        name: tuned
        enabled: yes

    - name: Start tuned service
      systemd:
        name: tuned
        state: started

# это motd_setup.yml
---
- name: Update system MOTD greeting
  hosts: all
  become: true
  vars:
    motd_message: "Добро пожаловать! Это обновлённое приветствие через Ansible."

  tasks:
    - name: Write custom MOTD message
      copy:
        content: "{{ motd_message }}\n"
        dest: /etc/motd
        mode: '0644'


....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 1](ссылка на скриншот 1)`


---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
---
- name: Install and configure MOTD with host info
  hosts: local
  become: true
  tasks:
    - name: Gather facts (ensure ansible_facts are available)
      setup:
        gather_subset: "!all"

    - name: Build MOTD content
      set_fact:
        motd_content: |
          
          #  Welcome to the Ansible test VM
          #
          #  Hostname: {{ ansible_hostname }}
          #  IP Address: {{ ansible_default_ipv4.address | default('unknown') }}
          #
          #  Have a great day, SysAdmin! 
          

    - name: Write MOTD file
      copy:
        content: "{{ motd_content }}"
        dest: /etc/motd
        owner: root
        group: root
        mode: '0644'

....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Всё отработало](<img width="755" height="587" alt="Все отработало" src="https://github.com/user-attachments/assets/f838cfd9-addd-4460-9f0e-3b60884ea89f" />
)`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>System Info — {{ ansible_hostname }}</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; }
    dt { font-weight: bold; }
    dd { margin-bottom: 10px; }
  </style>
</head>
<body>
  <h1>System Info: {{ ansible_hostname }}</h1>
  <dl>
    <dt>CPU Cores</dt>
    <dd>{{ ansible_processor_vcpus }}</dd>

    <dt>RAM (Total)</dt>
    <dd>{{ (ansible_memtotal_mb / 1024) | round(1) }} GB</dd>

    <dt>First HDD Size</dt>
    {% if ansible_devices.sda is defined %}
      <dd>{{ (ansible_devices.sda.size | float / 1073741824) | round(1) }} GB (sda)</dd>
    {% elif ansible_devices.vda is defined %}
      <dd>{{ (ansible_devices.vda.size | float / 1073741824) | round(1) }} GB (vda)</dd>
    {% else %}
      <dd>Unknown</dd>
    {% endif %}

    <dt>IP Address</dt>
    <dd>{{ ansible_default_ipv4.address | default('unknown') }}</dd>
  </dl>
  <p><small>Generated by Ansible role: apache_web</small></p>
</body>
</html>

....
---
- name: Install Apache web server
  apt:
    name: apache2
    state: present
  when: ansible_os_family == "Debian"

- name: Ensure Apache is enabled and started
  systemd:
    name: apache2
    enabled: true
    state: started
    daemon_reload: yes

- name: Create /var/www/html/index.html from template
  template:
    src: index.html.j2
    dest: /var/www/html/index.html
    owner: root
    group: root
    mode: '0644'
  notify: Restart Apache

- name: Open port 80 in UFW (if installed)
  ufw:
    rule: allow
    port: '80'
    proto: tcp
  when: ufw_enabled | default(false)

- name: Verify website returns HTTP 200
  uri:
    url: "http://{{ ansible_default_ipv4.address }}"
    method: GET
    timeout: 5
    status_code: 200
  register: site_check
  failed_when: site_check.status != 200

....
---
- name: Restart Apache
  systemd:
    name: apache2
    state: restarted
    daemon_reload: yes

....
---
- name: Deploy Apache with system info page
  hosts: local
  become: true
  roles:
    - apache_web

....
[local]
localhost ansible_connection=local


[defaults]
inventory = ./inventory
interpreter_python = /usr/bin/python3
deprecation_warnings = False

```

`При необходимости прикрепитe сюда скриншоты
![Для задачи 3](<img width="711" height="636" alt="Задача 3" src="https://github.com/user-attachments/assets/dba729d4-d2cd-41ff-9be4-06bfbe60215b" />
)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
