# Домашнее задание к занятию «Инструменты Git» - Студент группы FOPS-42 Власов Владимир

### Цель задания

В результате выполнения задания вы:

* научитесь работать с утилитами Git;
* потренируетесь решать типовые задачи, возникающие при работе в команде. 

### Инструкция к заданию

1. Склонируйте [репозиторий](https://github.com/hashicorp/terraform) с исходным кодом Terraform.
2. Создайте файл для ответов на задания в своём репозитории, после выполнения прикрепите ссылку на .md-файл с ответами в личном кабинете.
3. Любые вопросы по решению задач задавайте в чате учебной группы.

------

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?
* Сколько родителей у коммита `b8d720`? Напишите их хеши.
* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.
* Кто автор функции `synchronizedWriters`? 

*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.

### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.

---

## Ответ вопрос 1 в задании:

1. Хеш aefead2207ef7e2aa5dc81a34aedf0cad4c32545 у комментария 'Update CHANGELOG.md'.
Нашел путем ввода команд:
```bash
git show aefea
git log aefea -1

```
![z1](https://github.com/wlasoff/netology-devops-home-git-tools/blob/main/img/z1.png)

## Ответ вопрос 2 в задании:

2.1 У коммита `85024d3` есть соответствие только тэгу 'v0.12.23'
Нашли путем ввода команд:
```bash
git show 85024d3
git log 85024d3 -1
```
![z21](https://github.com/wlasoff/netology-devops-home-git-tools/blob/main/img/z21.png)

2.2 У коммита `b8d720` всего 2 родителя: 56cd7859e05c36c06b56d013b55a252d0bb7e158 9ea88f22fc6269854151c571162c5bcf958bee2b
```bash
git show b8d720 --parents
```
![z22](https://github.com/wlasoff/netology-devops-home-git-tools/blob/main/img/z22.png)

2.3 Так выглядят хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24:
```bash
lastir@pmx-netology:~/github/terraform$ git log v0.12.23^..v0.12.24 --oneline
33ff1c03bb (tag: v0.12.24) v0.12.24
b14b74c493 [Website] vmc provider links
3f235065b9 Update CHANGELOG.md
6ae64e247b registry: Fix panic when server is unreachable
5c619ca1ba website: Remove links to the getting started guide's old location
06275647e2 Update CHANGELOG.md
d5f9411f51 command: Fix bug when using terraform login on Windows
4b6d06cc5d Update CHANGELOG.md
dd01a35078 Update CHANGELOG.md
225466bc3e Cleanup after v0.12.23 release
85024d3100 (tag: v0.12.23) v0.12.23
lastir@pmx-netology:~/github/terraform$
```
* коммит, в котором была создана функция `func providerSource` - commit 8c928e83589d90a031f811fae52a81be7153e82f
нашел с помощью команд:
```bash
lastir@pmx-netology:~/github/terraform$ git grep -p -n 'func providerSource('
provider_source.go=6=import (
provider_source.go:26:func providerSource(configs []*cliconfig.ProviderInstallation, services *disco.Disco) (getproviders.Source, tfdiags.Diagnostics) {
lastir@pmx-netology:~/github/terraform$
lastir@pmx-netology:~/github/terraform$ git log -L :providerSource:provider_source.go
```
первой командой определил в каком файле эта функция, а следующей список коммитов ее изменяющие, выбрал самый первый коммит
* все коммиты, в которых была изменена функция `globalPluginDirs`
```bash
lastir@pmx-netology:~/github/terraform$ git log -S "globalPluginDirs" --oneline
7c4aeac5f3 stacks: load credentials from config file on startup (#35952)
65c4ba7363 Remove terraform binary
125eb51dc4 Remove accidentally-committed binary
22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
7c7e5d8f0a Don't show data while input if sensitive
35a058fb3d main: configure credentials from the CLI config file
c0b1761096 prevent log output during init
8364383c35 Push plugin discovery down into command package
lastir@pmx-netology:~/github/terraform$
```
* автор функции `synchronizedWriters` - Martin Atkins <mart@degeneration.co.uk>
выполнил git grep 'synchronizedWriters' и ничего не нашел, поэтому как и в предыдущем варианте искал через git log -S
```bash
lastir@pmx-netology:~/github/terraform$ git grep 'synchronizedWriters'
lastir@pmx-netology:~/github/terraform$
lastir@pmx-netology:~/github/terraform$ git log -S synchronizedWriters
commit bdfea50cc85161dea41be0fe3381fd98731ff786
Author: James Bardin <j.bardin@gmail.com>
Date:   Mon Nov 30 18:02:04 2020 -0500

    remove unused

commit fd4f7eb0b935e5a838810564fd549afe710ae19a
Author: James Bardin <j.bardin@gmail.com>
Date:   Wed Oct 21 13:06:23 2020 -0400

    remove prefixed io

    The main process is now handling what output to print, so it doesn't do
    any good to try and run it through prefixedio, which is only adding
    extra coordination to echo the same data.

commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Wed May 3 16:25:41 2017 -0700

    main: synchronize writes to VT100-faker on Windows

    We use a third-party library "colorable" to translate VT100 color
    sequences into Windows console attribute-setting calls when Terraform is
    running on Windows.

    colorable is not concurrency-safe for multiple writes to the same console,
    because it writes to the console one character at a time and so two
    concurrent writers get their characters interleaved, creating unreadable
    garble.

    Here we wrap around it a synchronization mechanism to ensure that there
    can be only one Write call outstanding across both stderr and stdout,
    mimicking the usual behavior we expect (when stderr/stdout are a normal
    file handle) of each Write being completed atomically.
lastir@pmx-netology:~/github/terraform$ git show 5ac311e2a91e381e2f52234668b49ba670aa0fe5
commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Wed May 3 16:25:41 2017 -0700
...
+++ b/synchronized_writers.go
@@ -0,0 +1,31 @@
+package main
+
+import (
+       "io"
+       "sync"
+)
+
+type synchronizedWriter struct {
+       io.Writer
+       mutex *sync.Mutex
+}
+
+// synchronizedWriters takes a set of writers and returns wrappers that ensure
+// that only one write can be outstanding at a time across the whole set.
+func synchronizedWriters(targets ...io.Writer) []io.Writer {
+       mutex := &sync.Mutex{}
+       ret := make([]io.Writer, len(targets))
+       for i, target := range targets {
+               ret[i] = &synchronizedWriter{
+                       Writer: target,
+                       mutex:  mutex,
+               }
+       }
+       return ret
+}
+
+func (w *synchronizedWriter) Write(p []byte) (int, error) {
+       w.mutex.Lock()
+       defer w.mutex.Unlock()
+       return w.Writer.Write(p)
+}

```
