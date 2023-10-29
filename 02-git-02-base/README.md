# "Основы Git"

## 1. Gitlab. Добавление и просмотр удаленных репозиториев по протоколам SSH и HTTPS

$${\color{red}Welcome \space \color{lightblue}To \space \color{orange}Stackoverflow}$$
$\textsf{\color{red}Red text}$

${\color{green}@smproskuryakov ➜ /workspaces/netology-devops (master)}$ <b>git remote -v</b><br>
<pre>
<i>origin  https://github.com/smproskuryakov/netology-devops (fetch)<br>
origin  https://github.com/smproskuryakov/netology-devops (push)</i><br>

@smproskuryakov ➜ /workspaces/netology-devops (master) <b>git remote add gitlab https://gitlab.com/netology-devops-35/netology-devops.git</b><br>

@smproskuryakov ➜ /workspaces/netology-devops (master) <b>git remote -v</b><br>
<i>gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (fetch)<br>
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (push)<br>
origin  https://github.com/smproskuryakov/netology-devops (fetch)<br>
origin  https://github.com/smproskuryakov/netology-devops (push)</i><br>
@smproskuryakov ➜ /workspaces/netology-devops (master)<br>

@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git remote -v</b><br>
<i>github-ssh      git@github.com:smproskuryakov/netology-devops.git (fetch)<br>
github-ssh      git@github.com:smproskuryakov/netology-devops.git (push)<br>
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (fetch)<br>
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (push)<br>
gitlab-ssh      git@gitlab.com:netology-devops-35/netology-devops.git (fetch)<br>
gitlab-ssh      git@gitlab.com:netology-devops-35/netology-devops.git (push)<br>
origin  https://github.com/smproskuryakov/netology-devops (fetch)<br>
origin  https://github.com/smproskuryakov/netology-devops (push)</i><br>
@smproskuryakov ➜ /workspaces/netology-devops (master)<br>
</pre>


## 2. Работа с IDE VS Code в графическом режиме ОС Windows, Linux shell и Codespaces

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



## 3. Работа с тегами

<pre>
@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git tag v0.0 HEAD</b> // Легековесный тег на HEAD-коммите


@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git show v0.0</b>

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
@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git log --grep "First commit"</b>
<i>commit 9bb3575b4748ff3579ffd8153ba999dc74b85dad
Author: smproskuryakov <smproskuryakov@yandex.ru>
Date:   Tue Oct 17 15:18:44 2023 +0300

    First commit
</i>

@smproskuryakov ➜ /workspaces/netology-devops (master)> $<b>git tag -a v0.2 -m "First commit" 9bb3575b4748ff3579ffd8153ba999dc74b85dad</b>

@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git show v0.2</b>
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
@smproskuryakov ➜ /workspaces/netology-devops (master)> $</i>
</pre>



<pre>
@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git push gitlab-ssh v0.0</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To gitlab.com:netology-devops-35/netology-devops.git
 * [new tag]         v0.0 -> v0.0</i>
@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git push github-ssh v0.0</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:smproskuryakov/netology-devops.git
 * [new tag]         v0.0 -> v0.0</i>
@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git push github-ssh --tags</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 180 bytes | 180.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:smproskuryakov/netology-devops.git
 * [new tag]         v0.2 -> v0.2</i>
@smproskuryakov ➜ /workspaces/netology-devops (master)> $ <b>git push gitlab-ssh --tags</b>
<i>Enter passphrase for key '/home/codespace/.ssh/id_rsa':
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 180 bytes | 180.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
To gitlab.com:netology-devops-35/netology-devops.git
 * [new tag]         v0.2 -> v0.2</i>
@smproskuryakov ➜ /workspaces/netology-devops (master)> $
</pre>

#### Просмотр тегов в графическом режиме, удаление случайного тега "show"

![Просмотр тегов в графическом режиме, удаление случайного тега "show"](img/tags-graph.png)


## 4. Работа с историей коммитов и ветвлениями

