# Домашнее задание к занятию «Хранение в K8s. Часть 2» - Подус Сергей

### Задание 1

**Что нужно сделать**

Создать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории. 
4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.
5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV.  Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

------

### Задание 2

**Что нужно сделать**

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
3. Продемонстрировать возможность чтения и записи файла изнутри пода. 
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.


## Ответ:

### Задание 1

1. Написанные манифесты находятся в папке src:

2. Написанные манифесты находятся в папке src:

3. Демонстрация того, что multitool читает файл:

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/manifest.png)

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/date%20mult.png)

4. Удалил deployment и PVC:

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/pv.png)

PV останется в состоянии Released, так как для него задана политика Retain (сохранить)

5. 

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/date-pv.png)

Файлы сохранятся, потому что PV имеет политику Retain

Если удалить PV файлы останутся на диске, так как PV не управляет удалением данных на локальной файловой системе. Политика Retain означает, что данные сохранятся на диске, даже после удаления PV.

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/delete2.png)


## Задание 2

1. Установил NFS сервер:

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/nfs%20server.png)

2. Написанные манифесты находятся в папке src:

3. 

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/nfs.png)

Создаем файл test.txt внутри контейнера

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube7/nfs-work.png)

С помощью ```kubectl describe -n hm7``` выясняем путь: идем по этому пути и видим, что файл существует, значит NFS работает.

```bash
Source:
    Type:          HostPath (bare host directory volume)
    Path:          /var/snap/microk8s/common/nfs-storage
    HostPathType:
```





