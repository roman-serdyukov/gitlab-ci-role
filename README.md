Apps-role
=========

Ansible role для установки gitlab-ce и gitlab-runner. Есть 2 варианта установки - обычный (по умолчанию) и docker контейнер (требует корректировки main.yml)
Состоит из следующих действий:
- Установка Docker [install-docker.yml](https://github.com/roman-serdyukov/gitlab-ci-role/blob/main/tasks/install-docker.yml).
- Установка и настройка gitlab-ce [gitlab.yml](https://github.com/roman-serdyukov/gitlab-ci-role/blob/main/tasks/gitlab.yml) (или [docker-gitlab.yml](https://github.com/roman-serdyukov/gitlab-ci-role/blob/main/tasks/docker-gitlab.yml)).
- Установка и настройка gitlab-runner [runner.yml](https://github.com/roman-serdyukov/gitlab-ci-role/blob/main/tasks/runner.yml) (или [docker-runner.yml](https://github.com/roman-serdyukov/gitlab-ci-role/blob/main/tasks/docker-runner.yml)).

Requirements
------------

Работоспособность протестирована на Ubuntu 20.04.


Role Variables
--------------

- runner:       имя хоста runner
- gitlab:       имя хоста gitlab
- my_domain:    доменное имя
- gitlab_pass:  пароль для gitlab. Указан только для демонстрации. Не рекомендуется хранить в открытом виде.
- token_ce:     токен для runner (генерируется в play gitlab)
- gitlab_host:  fqdn имя gitlab
- gitlab_url:   полный url адрес gitlab-ce
- gitlab_urls:  полный url (https) адрес gitlab-ce
- http_port, ssh_port: порты служб

Example Playbook
----------------
```
- name: Install gitlab ci
  hosts: servers
  roles:
    - gitlab-ci-role
```

Before start
----------------

- Если нет внутрненнего DNS сервера, то раскоментировать play hosts.yml.
- Для установки в Docker необходимо в main.yml закоментировать строку "when: ansible_nodename == {{ runner }}", а также  заменить 'include_tasks" с gitlab и runner на docker-gitlab и docker-runner.

License
-------

MIT

Author Information
------------------

Сердюков Роман
reserdukov@gmail.com