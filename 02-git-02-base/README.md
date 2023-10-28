## Gitlab. Добавление и просмотр удаленных репозиториев по протоколам SSH и HTTPS

<code>

@smproskuryakov ➜ /workspaces/netology-devops (master) $ **git remote -v**
*origin  https://github.com/smproskuryakov/netology-devops (fetch)
origin  https://github.com/smproskuryakov/netology-devops (push)*

@smproskuryakov ➜ /workspaces/netology-devops (master) $ **git remote add gitlab https://gitlab.com/netology-devops-35/netology-devops.git**

@smproskuryakov ➜ /workspaces/netology-devops (master) $ **git remote -v**
*gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (fetch)
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (push)
origin  https://github.com/smproskuryakov/netology-devops (fetch)
origin  https://github.com/smproskuryakov/netology-devops (push)*
@smproskuryakov ➜ /workspaces/netology-devops (master) $ 

@smproskuryakov ➜ /workspaces/netology-devops (master) $ **git remote -v**
*github-ssh      git@github.com:smproskuryakov/netology-devops.git (fetch)
github-ssh      git@github.com:smproskuryakov/netology-devops.git (push)
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (fetch)
gitlab  https://gitlab.com/netology-devops-35/netology-devops.git (push)
gitlab-ssh      git@gitlab.com:netology-devops-35/netology-devops.git (fetch)
gitlab-ssh      git@gitlab.com:netology-devops-35/netology-devops.git (push)
origin  https://github.com/smproskuryakov/netology-devops (fetch)
origin  https://github.com/smproskuryakov/netology-devops (push)*
@smproskuryakov ➜ /workspaces/netology-devops (master) $ 

</code>


## Работа с IDE VS Code в графическом режиме ОС Windows, Linux shell и Codespaces

#### Запуск IDR, просмотр списка удаленных репозиториев
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



