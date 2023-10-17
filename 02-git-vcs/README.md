# Added next file templates that will be ignored by git:
 *.[oa]
 *~

# Installing and initializing Git
sudo apt install git
git clone https://github.com/smproskuryakov/netology-devops.git
cd ./netology-devops/
git init
git config --global --add safe.directory /mnt/git-repo/netology-devops
git status

# Setup and add README.md in first commit
git status
git config --global user.email "smproskuryakov@yandex.ru" && git config --global user.name "smproskuryakov"
touch README.md
git status
git diff
git diff --staged
git status
git add README.md
git commit -m 'First commit'
git status

# Add .gitignore
touch .gitignore
echo -e '*.[oa]\n *~\n' > .gitignore
echo -e '# Added next file templates that will be ignored by git:\n *.[oa]\n *~\n' > README.md
mkdir ./Terraform && touch ./Terraform/.gitignore
git status
git diff
git diff --staged
git add README.md
git add .gitignore
git add /Terraform
git add ./Terraform/.gitignore
git status
git commit -m "Added gitignore"

# Deleting and moving files in third and fourth commit

echo "will_be_deleted" > will_be_deleted.txt
echo "will_be_moved" > will_be_moved.txt 
git add will_be_deleted.txt 
git add will_be_moved.txt 
git commit -m "Prepare to delete and move"
git log

git rm will_be_deleted.txt
git mv will_be_moved.txt has_been_moved.txt
git commit -m "Moved and deleted"

git log

git push