# "Основы Git"

## Gitlab. Добавление и просмотр удаленных репозиториев по протоколам SSH и HTTPS

<pre>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git remote -v</b>
<i>origin  https://github.com/smproskuryakov/netology-devops (fetch)
origin  https://github.com/smproskuryakov/netology-devops (push)</i>

<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git remote add gitlab https://gitlab.com/netology-devops-35/netology-devops.git</b>

<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git remote -v</b>
<i>gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (fetch)
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (push)
origin  https://github.com/smproskuryakov/netology-devops (fetch)
origin  https://github.com/smproskuryakov/netology-devops (push)</i>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $

<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git remote -v</b>
<i>github-ssh      git@github.com:smproskuryakov/netology-devops.git (fetch)
github-ssh      git@github.com:smproskuryakov/netology-devops.git (push)
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (fetch)
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (push)
gitlab-ssh      git@gitlab.com:netology-devops-35/netology-devops.git (fetch)
gitlab-ssh      git@gitlab.com:netology-devops-35/netology-devops.git (push)
origin  https://github.com/smproskuryakov/netology-devops (fetch)
origin  https://github.com/smproskuryakov/netology-devops (push)</i>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $
</pre>


## Работа с IDE VS Code в графическом режиме ОС Windows, Linux shell и Codespaces

#### Запуск IDE, просмотр списка удаленных репозиториев

![](img/vscode-start.png)

#### Создание репозитория в Gitlab

![](img/gitlab-new-repo.png)

#### Тестовое выполнение команд git remote -v, git clone, git init, git remote add

![](img/git-remote-add-gitlab.png)

#### Переход в Codespaces

![](img/open-netologydevops-graphis.png)

#### Редактирование файла README.md, попытка сохранения через графические средства IDE

![](img/index-changes.png)

#### Commit & Push посредством IDE

![](img/commit-push.png)

#### Просмотр активностей проекта в Gitlab

![](img/git-lab-project-overview.png)

#### Просмотр списка удаленных репозиториев, выполнение git push посредством SSH

![](img/git-push-ssh.png)

#### Клонирование репозитория origin в проект Gitlab

![](img/git-remote-add-github-ssh.png)

#### Просмотр коммитов и тегов в графическом режиме

![](img/vs-code-gitlens-commitgraph-tags.png)

#### Работа через WEB-интерфейс Codespaces

![](img/codespaces-web-ide.png)



#### Работа с тегами


<b>git tag v0.0 HEAD</b> // Легековесный тег на HEAD-коммите

<pre>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git show v0.0</b>

<i>commit 45861c2efa74d3fdb302cb64efe78652d91e50e5 (HEAD -> master, tag: v0.0, gitlab-ssh/master, github-ssh/master)
Author: smproskuryakov <139803641+smproskuryakov@users.noreply.github.com>
Date:   Sat Oct 28 17:20:29 2023 +0000

    edit readme

diff --git a/02-git-02-base/README.md b/02-git-02-base/README.md
index b0c010a..c912a81 100644
--- a/02-git-02-base/README.md
+++ b/02-git-02-base/README.md
@@ -31,17 +31,37 @@ origin  https://github.com/smproskuryakov/netology-devops (push)

 ## Работа с IDE VS Code в графическом режиме ОС Windows, Linux shell и Codespaces</i>

</pre>

<pre>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ **git log --grep "First commit"**
<i>commit 9bb3575b4748ff3579ffd8153ba999dc74b85dad
Author: smproskuryakov <smproskuryakov@yandex.ru>
Date:   Tue Oct 17 15:18:44 2023 +0300

    First commit

**git tag -a v0.2 -m "First commit" 9bb3575b4748ff3579ffd8153ba999dc74b85dad**

<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ **git show v0.2**
tag v0.2
Tagger: smproskuryakov <139803641+smproskuryakov@users.noreply.github.com>
Date:   Sat Oct 28 17:46:34 2023 +0000

First commit

commit 9bb3575b4748ff3579ffd8153ba999dc74b85dad (tag: v0.2)
Author: smproskuryakov <smproskuryakov@yandex.ru>
Date:   Tue Oct 17 15:18:44 2023 +0300

    First commit

diff --git a/02-git-vcs/README.md b/02-git-vcs/README.md
new file mode 100644
index 0000000..e69de29
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $</i>
</pre>


<b>git push origin <tag></b>
<b>git push <remote> --tags</b>

<pre>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git push gitlab-ssh v0.0</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To gitlab.com:netology-devops-35/netology-devops.git
 * [new tag]         v0.0 -> v0.0</i>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git push github-ssh v0.0</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:smproskuryakov/netology-devops.git
 * [new tag]         v0.0 -> v0.0</i>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git push github-ssh --tags</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 180 bytes | 180.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:smproskuryakov/netology-devops.git
 * [new tag]         v0.2 -> v0.2</i>
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $ <b>git push gitlab-ssh --tags</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 180 bytes | 180.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To gitlab.com:netology-devops-35/netology-devops.git
 * [new tag]         v0.2 -> v0.2
<span style="color:green;">@smproskuryakov ➜ /workspaces/netology-devops (master)</span>> $</i>
</pre>

#### Просмотр тегов в графическом режиме, удаление случайного тега "show"

![Просмотр тегов в графическом режиме, удаление случайного тега "show"](img/tags-graph.png)


## Работа с историей коммитов и ветвлениями

