# Git course

git crash course - cheatsheet style

[DRAFT]

## Basics

### Local repo

```bash
git status

# Empty
git clone git@github.com:asantos2000/git-course.git

cd git-course.git

touch file1.txt
touch file2.yxy

git status
#  master

# No commits yet

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         file1.txt
#         file2.txt

# nothing added to commit but untracked files present (use "git add" to track)

git add .

git status
# On branch master

# No commits yet

# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#         new file:   file1.txt
#         new file:   file2.txt

git ls-files -s
# 100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file1.txt
# 100644 e69de29bb2d1d6434b8b29ae775ad8c2e48c5391 0       file2.txt

git commit -m "first release"
# [master (root-commit) 5f0b758] first commit
#  2 files changed, 2 insertions(+)
#  create mode 100644 file1.txt
#  create mode 100644 file2.txt

git cat-file -p 5f0b758
# tree 86aef144801be55837cf5954aa0f7a8ca6e799a5
# author Anderson Santos <adsantos@gmail.com> 1631141370 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631141370 -0300

# first commit

git cat-file -s 5f0b758
# 185

git cat-file -t 5f0b758
# commit

touch file3.txt

git add file3.txt

git status
# On branch master
# Changes to be committed:
#   (use "git restore --staged <file>..." to unstage)
#         new file:   file3.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md


git rm --cached file3.txt
# rm 'file3.txt'

git ls-files
# file1.txt
# file2.txt

git status
# On branch master
# Your branch is based on 'origin/master', but the upstream is gone.
#   (use "git branch --unset-upstream" to fixup)

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         file3.txt

# nothing added to commit but untracked files present (use "git add" to track)

git add file3.txt

git commit -m "second commit"
# [master 5be69e8] second commit
#  1 file changed, 0 insertions(+), 0 deletions(-)
#  create mode 100644 file3.txt

git log
# commit 2f6256d9db0111e550461ca15a2f81b7066b134a (HEAD -> master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

ls -la .git/objects/                                    
# total 0
# drwxr-xr-x  11 anderson  staff  352 Sep  8 19:50 .
# drwxr-xr-x  13 anderson  staff  416 Sep  8 19:50 ..
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:49 21 <-- blob file2.txt
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:50 2f <-- commit 2
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:49 5f <-- commit 1
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:49 6c <-- blob file3.yxy
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:49 86 <-- tree 1 
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:50 96 <-- tree 2
# drwxr-xr-x   3 anderson  staff   96 Sep  8 19:49 fe <-- blob file1.txt
# drwxr-xr-x   2 anderson  staff   64 Sep  8 19:46 info
# drwxr-xr-x   2 anderson  staff   64 Sep  8 19:46 pack
```

### Stage and commit

```bash
cat .git/refs/heads/master
# 2f6256d9db0111e550461ca15a2f81b7066b134a

git cat-file -p 2f6256d9db0111e550461ca15a2f81b7066b134a
# tree 9670adcb30ebacdee9e5a4c5855165e9907b0a77
# parent 5f0b758fca230a9a7e977e041216df0b25b618c7
# author Anderson Santos <adsantos@gmail.com> 1631141410 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631141410 -0300

# second commit

rm file*.txt

git status
# On branch master
# Changes not staged for commit:
#   (use "git add/rm <file>..." to update what will be committed)
#   (use "git restore <file>..." to discard changes in working directory)
#         deleted:    file1.txt
#         deleted:    file2.txt
#         deleted:    file3.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

# no changes added to commit (use "git add" and/or "git commit -a")

# Stage delted files
git rm file1.txt
git rm file2.txt
git rm file3.txt

git status
# On branch master
# Changes to be committed:
#   (use "git restore --staged <file>..." to unstage)
#         deleted:    file1.txt
#         deleted:    file2.txt
#         deleted:    file3.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

git commit
[master 7debe1f] third commit
 3 files changed, 3 deletions(-)
 delete mode 100644 file1.txt
 delete mode 100644 file2.txt
 delete mode 100644 file3.txt

git log
# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c (HEAD -> master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

cat .git/refs/heads/master                              
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c <-- last commit

git cat-file -p 7debe1f
# tree 4b825dc642cb6eb9a060e54bf8d69288fbee4904
# parent 2f6256d9db0111e550461ca15a2f81b7066b134a
# author Anderson Santos <adsantos@gmail.com> 1631149771 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631149771 -0300

# third commit

git cat-file -p 4b825dc
# no blobs to list

git cat-file -t 4b825dc
# tree

git ls-files -s
# nothing

# Finding SHA1 for last commit
cat .git/refs/heads/master
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c <-- 3rd commit

git cat-file -p 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# tree 4b825dc642cb6eb9a060e54bf8d69288fbee4904
# parent 2f6256d9db0111e550461ca15a2f81b7066b134a <-- 2nd commit
# author Anderson Santos <adsantos@gmail.com> 1631149771 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631149771 -0300

# third commit

# move head to second commit
# detached HEAD state - HEAD is not pointing to a branch
git checkout 2f6256d9
# Previous HEAD position was 7debe1f third commit
# HEAD is now at 2f6256d second commit

cat .git/refs/heads/master # <-- keep pointing to 3rd commit
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c

git ls-files -s        
# 100644 fe4f02ad058b43f6ed467fdf65b935107529564b 0       file1.txt
# 100644 2147e418895119ab132ef3a44c8b16a4a6ce1b77 0       file2.txt
# 100644 6cbc8780e5977a9616d6fa643ecf2e4d01a3eeee 0       file3.txt

git log
# commit 2f6256d9db0111e550461ca15a2f81b7066b134a (HEAD)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

ls -l                  
# total 40
# -rw-r--r--  1 anderson  staff  7163 Sep  9 19:54 README.md
# -rw-r--r--  1 anderson  staff     5 Sep  9 19:52 file1.txt
# -rw-r--r--  1 anderson  staff     6 Sep  9 19:52 file2.txt
# -rw-r--r--  1 anderson  staff     5 Sep  9 19:55 file3.txt
# drwxr-xr-x  5 anderson  staff   160 Sep  9 19:37 media

git checkout master
# Previous HEAD position was 2f6256d second commit
# Switched to branch 'master'

git log
# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c (HEAD -> master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

cat .git/refs/heads/master
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
```

## Branches

```bash
git branch
# * master

git branch temp

git branch
# * master
#   temp

ls -l .git/refs/heads
# total 16
# -rw-r--r--  1 anderson  staff  41 Sep  8 22:09 master
# -rw-r--r--  1 anderson  staff  41 Sep  9 20:11 temp

cat .git/refs/heads/master
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c

cat .git/refs/heads/temp  
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c <-- point to the last commit on current branch

cat .git/HEAD           
# ref: refs/heads/master <-- current is master

git checkout temp  
# Switched to branch 'temp'

cat .git/HEAD 
# ref: refs/heads/temp

cat .git/refs/heads/temp  
# 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c <-- still pointing to last commit

git branch -m temp new-temp

git branch
#   master
# * new-temp

git branch -d new-temp     
# error: Cannot delete branch 'new-temp' checked out at '/Users/anderson/Downloads/tools/git-course'

git checkout master
# Switched to branch 'master'

git branch -d new-temp
# Deleted branch new-temp (was 7debe1f).

git checkout -b BR-1 # <-- create and switch. -b option
# Switched to a new branch 'BR-1'

echo  "Hello, Git" > file4.txt

git status
# On branch BR-1
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         file4.txt
#         media/

# nothing added to commit but untracked files present (use "git add" to track)

git add file4.txt

git commit -m "1st in BR-1"  
# [BR-1 2f213cb] 1st in BR-1
#  1 file changed, 1 insertion(+)
#  create mode 100644 file4.txt

git ls-files -s
# 100644 b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e 0       file4.txt

git log
# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa (HEAD -> BR-1)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c (master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

git cat-file -p 2f213cb7                 
# tree 0b7af1531d775dba317cb934aaca5826d907bb2f
# parent 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c <-- master
# author Anderson Santos <adsantos@gmail.com> 1631229987 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631229987 -0300

# 1st in BR-1

git cat-file -p 7debe1f681        
# tree 4b825dc642cb6eb9a060e54bf8d69288fbee4904
# parent 2f6256d9db0111e550461ca15a2f81b7066b134a
# author Anderson Santos <adsantos@gmail.com> 1631149771 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631149771 -0300

# third commit

cat .git/HEAD 
# ref: refs/heads/BR-1

ls -l .git/objects   
# total 0
# drwxr-xr-x  3 anderson  staff   96 Sep  9 20:26 0b <-- tree 1st in BR-1
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 21 <-- blob file2.txt
# drwxr-xr-x  4 anderson  staff  128 Sep  9 20:26 2f <-- commit 1st BR-1, 2nd commit master
# drwxr-xr-x  3 anderson  staff   96 Sep  8 22:09 4b <-- tree third commit
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 5f <-- 1st commit master
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 6c <-- blob file3.txt
# drwxr-xr-x  3 anderson  staff   96 Sep  8 22:09 7d <-- commit 3rd master
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 86 <-- tree first commit
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:50 96 <-- tree second commit
# drwxr-xr-x  3 anderson  staff   96 Sep  9 20:25 b7 <-- blob file4.txt
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 fe <-- blob file1.txt
# drwxr-xr-x  2 anderson  staff   64 Sep  8 19:46 info
# drwxr-xr-x  2 anderson  staff   64 Sep  8 19:46 pack
```

## Merge

### Fast-forward

```bash
git checkout BR-1
# Switched to branch 'BR-1'

git log
# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa (HEAD -> master, BR-1)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

git checkout master
# Switched to branch 'master'

git log
# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

git merge BR-1
# Updating 7debe1f..2f213cb
# Fast-forward
#  file4.txt | 1 +
#  1 file changed, 1 insertion(+)
#  create mode 100644 file4.txt

git log
# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa (HEAD -> master, BR-1)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

cat .git/refs/heads/master
# 2f213cb721286f76ee1e5b66c882b57bd80318fa

git branch -d BR-1    
# Deleted branch BR-1 (was 2f213cb). <-- no needed anymore

git branch
# * master
```

### three way merge

```bash
git checkout -b BR-2

mkdir new-files

echo "It's neew file in the new file folder" > new-files/file5.txt
echo "Another file with filename file6.txt" > new-files/file6.txt

echo "Hello, Git" > file7.txt

git add new-files/file5.txt
git add new-files/file6.txt
git add file7.txt

git commit -m "Three new files were created in the BR-2 branch"

git status
# On branch BR-2
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

# nothing added to commit but untracked files present (use "git add" to track)

git log
# commit 62f1866318c0d56602a7007a6b68ae86d062912c (HEAD -> BR-2)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:49:07 2021 -0300

#     Three new files were created in the BR-2 branch

# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa (master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

git status          
# On branch BR-2
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git restore <file>..." to discard changes in working directory)
#         modified:   new-files/file5.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

# no changes added to commit (use "git add" and/or "git commit -a")

# Stage all files
git commit -a -m "Changed file5.txt"

# OR
git add new-files/file5.txt

git commit -m "Changed file5.txt"
# [BR-2 009df99] Changed file5.txt
#  1 file changed, 3 insertions(+), 1 deletion(-)

git log
# commit 009df999d067ddf8b5ac48538aaebd624eeb5441 (HEAD -> BR-2)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:57:04 2021 -0300

#     Changed file5.txt

# commit 62f1866318c0d56602a7007a6b68ae86d062912c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:49:07 2021 -0300

#     Three new files were created in the BR-2 branch

# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa (master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

git checkout master              
# Switched to branch 'master'

git log
# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa (HEAD -> master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

echo "This file was added in the master branch" > file8.txt

git add file8.txt

git commit -m "Create file8.txt"
# [master fe06a52] Create file8.txt
#  1 file changed, 1 insertion(+)
#  create mode 100644 file8.txt

git log
# commit fe06a526930b5526f4e433721259860e238d7d8d (HEAD -> master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 17:04:52 2021 -0300

#     Create file8.txt

# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

git merge BR-2 -m "Merge branch 'BR-2' into master branch"
# Merge made by the 'recursive' strategy.
#  file7.txt           | 1 +
#  new-files/file5.txt | 3 +++
#  new-files/file6.txt | 1 +
#  3 files changed, 5 insertions(+)
#  create mode 100644 file7.txt
#  create mode 100644 new-files/file5.txt
#  create mode 100644 new-files/file6.txt

ls -l
# total 64
# -rw-r--r--   1 anderson  staff  19511 Sep 11 17:08 README.md
# -rw-r--r--   1 anderson  staff     11 Sep 11 16:29 file4.txt
# -rw-r--r--   1 anderson  staff     10 Sep 11 17:08 file7.txt
# -rw-r--r--   1 anderson  staff     40 Sep 11 17:02 file8.txt
# drwxr-xr-x  12 anderson  staff    384 Sep 10 09:37 media
# drwxr-xr-x   4 anderson  staff    128 Sep 11 17:08 new-files

git log
# commit a62c2c120650bc1402681d3001e6210069e57d97 (HEAD -> master)
# Merge: fe06a52 009df99
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 17:08:03 2021 -0300

#     Merge branch 'BR-2' into master branch

# commit fe06a526930b5526f4e433721259860e238d7d8d
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 17:04:52 2021 -0300

#     Create file8.txt

# commit 009df999d067ddf8b5ac48538aaebd624eeb5441 (BR-2) <-- Still point to this commit
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:57:04 2021 -0300

#     Changed file5.txt

# commit 62f1866318c0d56602a7007a6b68ae86d062912c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:49:07 2021 -0300

#     Three new files were created in the BR-2 branch

# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

cat .git/refs/heads/master
# a62c2c120650bc1402681d3001e6210069e57d97

git cat-file -p a62c2c120
# tree 437f25aa007ee0910c4b03952e213bf288c9bfa4
# parent fe06a526930b5526f4e433721259860e238d7d8d <-- parent 1 (master)
# parent 009df999d067ddf8b5ac48538aaebd624eeb5441 <-- parent 2 (BR-2)
# author Anderson Santos <adsantos@gmail.com> 1631390883 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631390883 -0300

# Merge branch 'BR-2' into master branch

git cat-file -p fe06a526
# tree 30fe888853ae60b07786b2eccf80ada0f3fd3a42
# parent 2f213cb721286f76ee1e5b66c882b57bd80318fa
# author Anderson Santos <adsantos@gmail.com> 1631390692 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631390692 -0300

# Create file8.txt <-- Last commit in master branch before branch

git cat-file -p 009df999
# tree 39a9f9243b6da6f071e02c4fa7fd1317d8d86e1b
# parent 62f1866318c0d56602a7007a6b68ae86d062912c
# author Anderson Santos <adsantos@gmail.com> 1631390224 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631390224 -0300

# Changed file5.txt <-- Last commit in BR-2 branch

git branch
#   BR-2
# * master

git branch -d BR-2
# Deleted branch BR-2 (was 009df99).

git log
# commit a62c2c120650bc1402681d3001e6210069e57d97 (HEAD -> master)
# Merge: fe06a52 009df99
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 17:08:03 2021 -0300

#     Merge branch 'BR-2' into master branch

# commit fe06a526930b5526f4e433721259860e238d7d8d
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 17:04:52 2021 -0300

#     Create file8.txt

# commit 009df999d067ddf8b5ac48538aaebd624eeb5441 <-- No pointer to BR-2
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:57:04 2021 -0300

#     Changed file5.txt

# commit 62f1866318c0d56602a7007a6b68ae86d062912c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 16:49:07 2021 -0300

#     Three new files were created in the BR-2 branch

# commit 2f213cb721286f76ee1e5b66c882b57bd80318fa
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Thu Sep 9 20:26:27 2021 -0300

#     1st in BR-1

# commit 7debe1f6814735cfa4c583bd60c7d2dcfc2ed64c
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 22:09:31 2021 -0300

#     third commit

# commit 2f6256d9db0111e550461ca15a2f81b7066b134a
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:50:10 2021 -0300

#     second commit

# commit 5f0b758fca230a9a7e977e041216df0b25b618c7
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Wed Sep 8 19:49:30 2021 -0300

#     first commit

git cat-file -p a62c2c120
# tree 437f25aa007ee0910c4b03952e213bf288c9bfa4
# parent fe06a526930b5526f4e433721259860e238d7d8d
# parent 009df999d067ddf8b5ac48538aaebd624eeb5441 <-- kept it after branch BR-2 deletion
# author Anderson Santos <adsantos@gmail.com> 1631390883 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631390883 -0300

# Merge branch 'BR-2' into master branch
```

### Branch conflict

```bash
git checkout -b BR-3
# Switched to a new branch 'BR-3'

ls -l
# total 72
# -rw-r--r--   1 anderson  staff  24410 Sep 11 19:41 README.md
# -rw-r--r--   1 anderson  staff     11 Sep 11 16:29 file4.txt
# -rw-r--r--   1 anderson  staff     10 Sep 11 17:08 file7.txt
# -rw-r--r--   1 anderson  staff     59 Sep 11 19:37 file8.txt
# drwxr-xr-x  12 anderson  staff    384 Sep 10 09:37 media
# drwxr-xr-x   4 anderson  staff    128 Sep 11 19:37 new-files

# Change file file5.txt, file7.txt on VS Code

git commit -a -m "Changes made in BR-3"
# [BR-3 b99ccd6] Changes made in BR-3
#  2 files changed, 2 insertions(+), 2 deletions(-)

git cat-file -p b99ccd6
# tree 0d53cd264b3456a2c6f3d5d0e113e7d99e300377
# parent 405a77da8499b53aeabae857b6c6e4eb6a465ea5
# author Anderson Santos <adsantos@gmail.com> 1631400299 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631400299 -0300

# Changes made in BR-3

git ls-files --with-tree 0d53cd26
# file4.txt
# file7.txt
# file8.txt
# new-files/file5.txt
# new-files/file6.txt

git log
# commit b99ccd6dbe0ad6d0c6d93352c615e0aad6a7353f (HEAD -> BR-3)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 19:44:59 2021 -0300

#     Changes made in BR-3

# commit 405a77da8499b53aeabae857b6c6e4eb6a465ea5
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 19:35:59 2021 -0300

#     Modified file8.txt
# ...

git checkout master
# Switched to branch 'master'

# Change file file5.txt, file7.txt on VS Code

git commit -a -m "file5 and file7 modified in master"
# [master 6d1f32e] file5 and file7 modified in master
#  2 files changed, 2 insertions(+), 2 deletions(-)

git log
# commit 6d1f32e6a9a8bb8fa76aae40ab4b31bf30b0f9a8 (HEAD -> master)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 19:51:17 2021 -0300

#     file5 and file7 modified in master

# commit 405a77da8499b53aeabae857b6c6e4eb6a465ea5
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 19:35:59 2021 -0300

#     Modified file8.txt
# ...

# Start merge
# Chceckout receive branch
git checkout master

git merge BR-3
# Auto-merging new-files/file5.txt
# CONFLICT (content): Merge conflict in new-files/file5.txt
# Auto-merging file7.txt
# CONFLICT (content): Merge conflict in file7.txt
# Automatic merge failed; fix conflicts and then commit the result.

git status
# On branch master
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#   (use "git merge --abort" to abort the merge)

# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#         both modified:   file7.txt
#         both modified:   new-files/file5.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

# no changes added to commit (use "git add" and/or "git commit -a")

git ls-files -s # Stage area               
# 100644 b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e 0       file4.txt
# 100644 6fe402b35d6e80a187adc393f36ce10e4fdd259f 1       file7.txt
# 100644 5749b350c8358f5e9b384e52b804d883280f4d53 2       file7.txt
# 100644 30ba061a5dec2330f773c1a8c51b1274c305c92d 3       file7.txt
# 100644 a529592a90242ad5002712bd5ba3b7ae97496666 0       file8.txt
# 100644 ec7426c4bfc4262aa09945cab137dec04acd6459 1       new-files/file5.txt
# 100644 993ef05c62618767c67fd9d1bdd04b7114a4ceed 2       new-files/file5.txt
# 100644 99c21cd4d1eaea216fb0b74f73edbdc6327fe2d8 3       new-files/file5.txt
# 100644 cf9ca3f4f20ab449121b916d6387328a789df46f 0       new-files/file6.txt

git cat-file -p 6fe402b3 # <--- file7.txt 1 - Initial version. Ancestor version.
# Hello, Git

git cat-file -p 5749b350 # <--- file7.txt 2
# Line replaced in master branch

git cat-file -p 30ba061a # <--- file7.txt 3
# Hello, Git. it was modified in the BR-3 branch.

cat file7.txt          
# <<<<<<< HEAD
# Line replaced in master branch
# =======
# Hello, Git. it was modified in the BR-3 branch.
# >>>>>>> BR-3

cat file5.txt
# It's neew file in the new file folder

# <<<<<<< HEAD
# file5txt was just changed. This line was modified in master branch.
# =======
# file5txt was just changed. This line was changed in BR-3 branch
# >>>>>>> BR-3

# Rememove on editor the conflict lines in file7.txt
cat file7.txt
# Line replaced in master branch

git status
# On branch master
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#   (use "git merge --abort" to abort the merge)

# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#         both modified:   file7.txt
#         both modified:   new-files/file5.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

# no changes added to commit (use "git add" and/or "git commit -a")

git add file7.txt

git status
# On branch master
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#   (use "git merge --abort" to abort the merge)

# Changes to be committed:
#         modified:   file7.txt

# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
#         both modified:   new-files/file5.txt

# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         README.md
#         media/

git ls-files -s
# 100644 b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e 0       file4.txt
# 100644 1e4937a843f913aa04c9a4943c5802cf90f406bc 0       file7.txt <-- conflict resolved
# 100644 a529592a90242ad5002712bd5ba3b7ae97496666 0       file8.txt
# 100644 ec7426c4bfc4262aa09945cab137dec04acd6459 1       new-files/file5.txt
# 100644 993ef05c62618767c67fd9d1bdd04b7114a4ceed 2       new-files/file5.txt
# 100644 99c21cd4d1eaea216fb0b74f73edbdc6327fe2d8 3       new-files/file5.txt
# 100644 cf9ca3f4f20ab449121b916d6387328a789df46f 0       new-files/file6.txt

# Resolve conflict in file new-files/file5.txt
cat new-files/file5.txt
# It's neew file in the new file folder

# file5txt was just changed. This line was changed in BR-3 branch

git add new-files/file5.txt
# 100644 b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e 0       file4.txt
# 100644 1e4937a843f913aa04c9a4943c5802cf90f406bc 0       file7.txt
# 100644 a529592a90242ad5002712bd5ba3b7ae97496666 0       file8.txt
# 100644 dc2c7a1bfd7fec2cf48430e17f68f54d78ae1751 0       new-files/file5.txt
# 100644 cf9ca3f4f20ab449121b916d6387328a789df46f 0       new-files/file6.txt

# Finish merge
cat .git/MERGE_HEAD
# 96d9e73bfac533919475a53df08c8ae090c4f38d

git cat-file -p 96d9e73bfac533919475a53df08c8ae090c4f38d
# tree 16a2b912a1bb7aeb0d56efa31b175a44b717b76f
# parent 6d1f32e6a9a8bb8fa76aae40ab4b31bf30b0f9a8
# parent b99ccd6dbe0ad6d0c6d93352c615e0aad6a7353f
# author Anderson Santos <adsantos@gmail.com> 1631412080 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631412080 -0300

# Merge branch 'BR-3'

git commit
# Merge branch 'BR-3'

# Conflicts:
#       file7.txt
#       new-files/file5.txt
#
# It looks like you may be committing a merge.
# If this is not correct, please run
#       git update-ref -d MERGE_HEAD
# and try again.


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# All conflicts fixed but you are still merging.

# [master 96d9e73] Merge branch 'BR-3'

git status
# commit 96d9e73bfac533919475a53df08c8ae090c4f38d (HEAD -> master)
# Merge: 6d1f32e b99ccd6
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 23:01:20 2021 -0300

#     Merge branch 'BR-3'

# commit 6d1f32e6a9a8bb8fa76aae40ab4b31bf30b0f9a8
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 19:51:17 2021 -0300

#     file5 and file7 modified in master
# ...

git branch
#   BR-3
# * master

git branch -d BR-3
# Deleted branch BR-3 (was b99ccd6).
```

### push, fetch and pull - interact with remote repos

```bash
git remote
# origin

git remote -v
# origin  git@github.com:asantos2000/git-course.git (fetch)
# origin  git@github.com:asantos2000/git-course.git (push)

# First push to remote
git push --set-upstream origin master
# Enumerating objects: 45, done.
# Counting objects: 100% (45/45), done.
# Delta compression using up to 4 threads
# Compressing objects: 100% (32/32), done.
# Writing objects: 100% (45/45), 3.44 KiB | 1.15 MiB/s, done.
# Total 45 (delta 12), reused 0 (delta 0), pack-reused 0
# remote: Resolving deltas: 100% (12/12), done.
# To github.com:asantos2000/git-course.git
#  * [new branch]      master -> master
# Branch 'master' set up to track remote branch 'master' from 'origin'.

# All branches local and remote
git branch -a
# * master
#   remotes/origin/master

# All remote branches
git branch -r
#   origin/master

# Tracking branch
git branch -vv
# * master 96d9e73 [origin/master] Merge branch 'BR-3'

# Create new branch on remote
git fetch    
# From github.com:asantos2000/git-course
#  * [new branch]      feature-1  -> origin/feature-1

git branch -a
# * master
#   remotes/origin/feature-1
#   remotes/origin/master

# Track remote branch feature-1
git checkout feature-1
# Branch 'feature-1' set up to track remote branch 'feature-1' from 'origin'.
# Switched to a new branch 'feature-1'

git branch -vv
# * feature-1 96d9e73 [origin/feature-1] Merge branch 'BR-3'
#   master    96d9e73 [origin/master] Merge branch 'BR-3'

# try delete remote branch
git branch -d feature-1
# error: Cannot delete branch 'feature-1' checked out at '/Users/anderson/Downloads/tools/git-course'

git checkout master
# Switched to branch 'master'
# Your branch is up to date with 'origin/master'.

git branch -d feature-1
# Deleted branch feature-1 (was 96d9e73).

# Tracking feature-1 again
git checkout feature-1
# Branch 'feature-1' set up to track remote branch 'feature-1' from 'origin'.
# Switched to a new branch 'feature-1'

git remote -v
# origin  git@github.com:asantos2000/git-course.git (fetch)
# origin  git@github.com:asantos2000/git-course.git (push)

git remote show origin
# * remote origin
#   Fetch URL: git@github.com:asantos2000/git-course.git
#   Push  URL: git@github.com:asantos2000/git-course.git
#   HEAD branch: master
#   Remote branches:
#     feature-1 tracked
#     master    tracked
#   Local branches configured for 'git pull':
#     feature-1 merges with remote feature-1
#     master    merges with remote master
#   Local refs configured for 'git push':
#     feature-1 pushes to feature-1 (up to date)
#     master    pushes to master    (up to date)

# After create new branch on remote
git remote show origin
# * remote origin
#   Fetch URL: git@github.com:asantos2000/git-course.git
#   Push  URL: git@github.com:asantos2000/git-course.git
#   HEAD branch: master
#   Remote branches:
#     feature-1 tracked
#     master    tracked
#     temp      new (next fetch will store in remotes/origin)
#   Local branches configured for 'git pull':
#     feature-1 merges with remote feature-1
#     master    merges with remote master
#   Local refs configured for 'git push':
#     feature-1 pushes to feature-1 (up to date)
#     master    pushes to master    (up to date)

git fetch             
# From github.com:asantos2000/git-course
#  * [new branch]      temp       -> origin/temp

git branch -r
#   origin/feature-1
#   origin/master
#   origin/temp

git checkout temp
# Branch 'temp' set up to track remote branch 'temp' from 'origin'.
# Switched to a new branch 'temp'

git remote show origin
# * remote origin
#   Fetch URL: git@github.com:asantos2000/git-course.git
#   Push  URL: git@github.com:asantos2000/git-course.git
#   HEAD branch: master
#   Remote branches:
#     feature-1 tracked
#     master    tracked
#     temp      tracked
#   Local branches configured for 'git pull':
#     feature-1 merges with remote feature-1
#     master    merges with remote master
#     temp      merges with remote temp
#   Local refs configured for 'git push':
#     feature-1 pushes to feature-1 (up to date)
#     master    pushes to master    (up to date)
#     temp      pushes to temp      (up to date)

# Delete temp branch on remote

git remote show origin
# * remote origin
#   Fetch URL: git@github.com:asantos2000/git-course.git
#   Push  URL: git@github.com:asantos2000/git-course.git
#   HEAD branch: master
#   Remote branches:
#     feature-1                tracked
#     master                   tracked
#     refs/remotes/origin/temp stale (use 'git remote prune' to remove)
#   Local branches configured for 'git pull':
#     feature-1 merges with remote feature-1
#     master    merges with remote master
#     temp      merges with remote temp
#   Local refs configured for 'git push':
#     feature-1 pushes to feature-1 (up to date)
#     master    pushes to master    (up to date)

git remote prune origin
# Pruning origin
# URL: git@github.com:asantos2000/git-course.git
#  * [pruned] origin/temp

git remote show origin
# * remote origin
#   Fetch URL: git@github.com:asantos2000/git-course.git
#   Push  URL: git@github.com:asantos2000/git-course.git
#   HEAD branch: master
#   Remote branches:
#     feature-1 tracked
#     master    tracked
#   Local branches configured for 'git pull':
#     feature-1 merges with remote feature-1
#     master    merges with remote master
#     temp      merges with remote temp
#   Local refs configured for 'git push':
#     feature-1 pushes to feature-1 (up to date)
#     master    pushes to master    (up to date)

git branch -vv
#   feature-1 96d9e73 [origin/feature-1] Merge branch 'BR-3'
#   master    96d9e73 [origin/master] Merge branch 'BR-3'
# * temp      96d9e73 [origin/temp: gone] Merge branch 'BR-3'

git checkout master
# Switched to branch 'master'
# Your branch is up to date with 'origin/master'.

git branch -d temp     
# Deleted branch temp (was 96d9e73).

git branch -vv
#   feature-1 96d9e73 [origin/feature-1] Merge branch 'BR-3'
# * master    96d9e73 [origin/master] Merge branch 'BR-3'

git branch -a 
#   feature-1
# * master
#   remotes/origin/feature-1
#   remotes/origin/master

git fetch -v
# From github.com:asantos2000/git-course
#  = [up to date]      master     -> origin/master
#  = [up to date]      feature-1  -> origin/feature-1

git pull -v
# From github.com:asantos2000/git-course
#  = [up to date]      master     -> origin/master
#  = [up to date]      feature-1  -> origin/feature-1
# Already up to date.

ls -l .git/          
# total 64
# -rw-r--r--   1 anderson  staff   540 Sep 11 23:01 COMMIT_EDITMSG
# -rw-r--r--   1 anderson  staff   206 Sep 12 16:35 FETCH_HEAD <-- 
# -rw-r--r--   1 anderson  staff    23 Sep 12 16:09 HEAD
# -rw-r--r--   1 anderson  staff    41 Sep 12 16:35 ORIG_HEAD
# -rw-r--r--   1 anderson  staff   379 Sep 12 16:10 config
# -rw-r--r--   1 anderson  staff    73 Sep  8 19:46 description
# drwxr-xr-x  15 anderson  staff   480 Sep  8 19:46 hooks
# -rw-r--r--   1 anderson  staff   491 Sep 12 16:09 index
# drwxr-xr-x   3 anderson  staff    96 Sep  8 19:46 info
# drwxr-xr-x   4 anderson  staff   128 Sep  8 19:49 logs
# drwxr-xr-x  44 anderson  staff  1408 Sep 12 16:35 objects
# -rw-r--r--   1 anderson  staff    46 Sep 12 16:10 packed-refs
# drwxr-xr-x   5 anderson  staff   160 Sep 12 15:36 refs

cat .git/FETCH_HEAD
# 96d9e73bfac533919475a53df08c8ae090c4f38d                branch 'master' of github.com:asantos2000/git-course
# 96d9e73bfac533919475a53df08c8ae090c4f38d        not-for-merge   branch 'feature-1' of github.com:asantos2000/git-course

# git cat-file -p 96d9e73btree 16a2b912a1bb7aeb0d56efa31b175a44b717b76f
# parent 6d1f32e6a9a8bb8fa76aae40ab4b31bf30b0f9a8
# parent b99ccd6dbe0ad6d0c6d93352c615e0aad6a7353f
# author Anderson Santos <adsantos@gmail.com> 1631412080 -0300
# committer Anderson Santos <adsantos@gmail.com> 1631412080 -0300

# Merge branch 'BR-3'

git log
# commit 96d9e73bfac533919475a53df08c8ae090c4f38d (HEAD -> master, origin/master, origin/feature-1, feature-1)
# Merge: 6d1f32e b99ccd6
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 23:01:20 2021 -0300

#     Merge branch 'BR-3'

# commit 6d1f32e6a9a8bb8fa76aae40ab4b31bf30b0f9a8
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 19:51:17 2021 -0300

#     file5 and file7 modified in master
# ...

# Create file in feaature-1 remote branch and pull those changes
git checkout feature-1
# Switched to branch 'feature-1'
# Your branch is behind 'origin/feature-1' by 1 commit, and can be fast-forwarded.
#   (use "git pull" to update your local branch)

git pull -v
# Updating 96d9e73..e5934fb
# Fast-forward
#  feature/another-file.txt | 1 +
#  1 file changed, 1 insertion(+)
#  create mode 100644 feature/another-file.txt

# listing stage area
git ls-files -s
# 100644 7aa991eb0a469479537b396d374520486f42aadd 0       feature/another-file.txt
# 100644 b7aec520dec0a7516c18eb4c68b64ae1eb9b5a5e 0       file4.txt
# 100644 1e4937a843f913aa04c9a4943c5802cf90f406bc 0       file7.txt
# 100644 a529592a90242ad5002712bd5ba3b7ae97496666 0       file8.txt
# 100644 dc2c7a1bfd7fec2cf48430e17f68f54d78ae1751 0       new-files/file5.txt
# 100644 cf9ca3f4f20ab449121b916d6387328a789df46f 0       new-files/file6.txt

# Listing working directory
ls -l
# total 112
# -rw-r--r--   1 anderson  staff  41434 Sep 12 16:51 README.md
# drwxr-xr-x   3 anderson  staff     96 Sep 12 16:46 feature
# -rw-r--r--   1 anderson  staff     11 Sep 11 16:29 file4.txt
# -rw-r--r--   1 anderson  staff     31 Sep 11 22:52 file7.txt
# -rw-r--r--   1 anderson  staff     59 Sep 11 19:37 file8.txt
# drwxr-xr-x  12 anderson  staff    384 Sep 10 09:37 media
# drwxr-xr-x   4 anderson  staff    128 Sep 11 19:54 new-files

git log
# commit e5934fbe68f958d97a0f87d0ce3f64087ea5f925 (HEAD -> feature-1, origin/feature-1)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 16:45:01 2021 -0300

#     Create another-file.txt

# commit 96d9e73bfac533919475a53df08c8ae090c4f38d (origin/master, master)
# Merge: 6d1f32e b99ccd6
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 23:01:20 2021 -0300

#     Merge branch 'BR-3'
# ...

# Make local changes and commit
git checkout feature-1

git commit -a -m "Modifiead another-file.txt locally"
# [feature-1 e6b8dec] Modifiead another-file.txt locally
#  1 file changed, 2 insertions(+)

# Create another file in remote feature branch

git log
# commit e6b8dec85447978d66c8570228f65a91ea9d9aae (HEAD -> feature-1)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 17:00:12 2021 -0300

#     Modifiead another-file.txt locally

# commit e5934fbe68f958d97a0f87d0ce3f64087ea5f925
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 16:45:01 2021 -0300

#     Create another-file.txt

# commit 96d9e73bfac533919475a53df08c8ae090c4f38d (origin/master, master)
# Merge: 6d1f32e b99ccd6
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sat Sep 11 23:01:20 2021 -0300

#     Merge branch 'BR-3'

git pull -vv          
# From github.com:asantos2000/git-course
#  = [up to date]      feature-1  -> origin/feature-1
#  = [up to date]      master     -> origin/master
# hint: Pulling without specifying how to reconcile divergent branches is
# hint: discouraged. You can squelch this message by running one of the following
# hint: commands sometime before your next pull:
# hint: 
# hint:   git config pull.rebase false  # merge (the default strategy)
# hint:   git config pull.rebase true   # rebase
# hint:   git config pull.ff only       # fast-forward only
# hint: 
# hint: You can replace "git config" with "git config --global" to set a default
# hint: preference for all repositories. You can also pass --rebase, --no-rebase,
# hint: or --ff-only on the command line to override the configured default per
# hint: invocation.
# Merge made by the 'recursive' strategy.
#  feature/one-more-file.txt | 1 +
#  1 file changed, 1 insertion(+)
#  create mode 100644 feature/one-more-file.txt

git log
# commit 105ef930e3beccd56e09694b33dc6c859d3f076e (HEAD -> feature-1)
# Merge: e6b8dec cb9fdc0
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 17:08:22 2021 -0300

#     Merge branch 'feature-1' of github.com:asantos2000/git-course into feature-1

# commit cb9fdc088d43978f79dfb38ec26018ee079961d3 (origin/feature-1)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 17:01:40 2021 -0300

#     Create one-more-file.txt

# commit e6b8dec85447978d66c8570228f65a91ea9d9aae
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 17:00:12 2021 -0300

#     Modifiead another-file.txt locally
# ...

# Git local repository
ls -lt .git/objects       
# total 0
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:08 10
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:08 44
# drwxr-xr-x  4 anderson  staff  128 Sep 12 17:08 62
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:01 d5
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:01 32
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:01 90
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:01 cb
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:00 e6
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:00 fa
# drwxr-xr-x  3 anderson  staff   96 Sep 12 17:00 29
# drwxr-xr-x  3 anderson  staff   96 Sep 12 16:58 8c
# drwxr-xr-x  3 anderson  staff   96 Sep 12 16:45 7a
# drwxr-xr-x  3 anderson  staff   96 Sep 12 16:45 ad
# drwxr-xr-x  4 anderson  staff  128 Sep 12 16:45 57
# drwxr-xr-x  3 anderson  staff   96 Sep 12 16:45 e5
# drwxr-xr-x  4 anderson  staff  128 Sep 11 23:03 96
# drwxr-xr-x  4 anderson  staff  128 Sep 11 23:01 16
# drwxr-xr-x  3 anderson  staff   96 Sep 11 23:01 9a
# drwxr-xr-x  3 anderson  staff   96 Sep 11 23:00 dc
# drwxr-xr-x  3 anderson  staff   96 Sep 11 22:55 1e
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:54 c5
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:54 7f
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:51 6d
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:51 19
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:51 d9
# drwxr-xr-x  4 anderson  staff  128 Sep 11 19:51 99
# drwxr-xr-x  4 anderson  staff  128 Sep 11 19:44 b9
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:44 0d
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:44 bf
# drwxr-xr-x  4 anderson  staff  128 Sep 11 19:44 30
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:35 40
# drwxr-xr-x  3 anderson  staff   96 Sep 11 19:35 a5
# drwxr-xr-x  3 anderson  staff   96 Sep 11 17:08 a6
# drwxr-xr-x  3 anderson  staff   96 Sep 11 17:08 43
# drwxr-xr-x  4 anderson  staff  128 Sep 11 17:04 fe
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:57 00
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:57 39
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:57 f7
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:56 ec
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:49 af
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:49 13
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:48 6f
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:48 cf
# drwxr-xr-x  3 anderson  staff   96 Sep 11 16:48 45
# drwxr-xr-x  4 anderson  staff  128 Sep  9 20:26 2f
# drwxr-xr-x  3 anderson  staff   96 Sep  9 20:26 0b
# drwxr-xr-x  3 anderson  staff   96 Sep  9 20:25 b7
# drwxr-xr-x  3 anderson  staff   96 Sep  8 22:09 7d
# drwxr-xr-x  3 anderson  staff   96 Sep  8 22:09 4b
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 6c
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 5f
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 86
# drwxr-xr-x  3 anderson  staff   96 Sep  8 19:49 21
# drwxr-xr-x  2 anderson  staff   64 Sep  8 19:46 info
# drwxr-xr-x  2 anderson  staff   64 Sep  8 19:46 pack

# Merge conflict in pull operation
# Change remote README.md file
# change locally README.md file

git add README.md

git commit -m "Change README pull oper"
# [master 99cb159] Change README pull oper
#  1 file changed, 6 insertions(+)

# Bring remote changes
git pull -v
# From github.com:asantos2000/git-course
#  = [up to date]      master     -> origin/master
#  = [up to date]      feature-1  -> origin/feature-1
# Auto-merging README.md
# Merge made by the 'recursive' strategy.
#  README.md | 4 ++++
#  1 file changed, 4 insertions(+)

git push       
# Enumerating objects: 13, done.
# Counting objects: 100% (13/13), done.
# Delta compression using up to 4 threads
# Compressing objects: 100% (9/9), done.
# Writing objects: 100% (9/9), 1.08 KiB | 1.08 MiB/s, done.
# Total 9 (delta 6), reused 0 (delta 0), pack-reused 0
# remote: Resolving deltas: 100% (6/6), completed with 2 local objects.
# To github.com:asantos2000/git-course.git
#    dcb0b69..edf267f  master -> master

git log
# commit edf267f45c7008916c94ad2e514436e0796d2878 (HEAD -> master, origin/master) <-- Both point to the same commit (SHA1)
# Merge: 44e5189 dcb0b69
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 17:39:04 2021 -0300

#     Merge branch 'master' of github.com:asantos2000/git-course
# ...
```

### Local and Remote sync

```bash
git pull -v 
# From github.com:asantos2000/git-course
#  = [up to date]      master     -> origin/master
#  = [up to date]      feature-1  -> origin/feature-1
# Already up to date.

git push -v
# Pushing to github.com:asantos2000/git-course.git
# To github.com:asantos2000/git-course.git
#  = [up to date]      master -> master
# updating local tracking ref 'refs/remotes/origin/master'
# Everything up-to-date
```

### Creating a Remote Branch Based on a Local Branch

```bash
git checkout -b feature-2
# Switched to a new branch 'feature-2'

git branch -a
#   feature-1
# * feature-2
#   master
#   remotes/origin/feature-1
#   remotes/origin/master

git branch -r
#   origin/feature-1
#   origin/master

git branch -vv
#   feature-1 d13edc5 [origin/feature-1] Add README.md
# * feature-2 edf267f Merge branch 'master' of github.com:asantos2000/git-course
#   master    edf267f [origin/master] Merge branch 'master' of github.com:asantos2000/git-course

# Change some files

git add feature/another-file.txt

git commit -m "another-file.txt was modified in feature-2 branch"
# feature-2 branch"
# [feature-2 fcd5011] another-file.txt was modified in feature-2 branch
#  1 file changed, 4 insertions(+), 2 deletions(-)

git log
# commit fcd50113670932014c522ce69ec0c3fdd4fa732a (HEAD -> feature-2)
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 18:07:27 2021 -0300

#     another-file.txt was modified in feature-2 branch

# commit edf267f45c7008916c94ad2e514436e0796d2878 (origin/master, master)
# Merge: 44e5189 dcb0b69
# Author: Anderson Santos <adsantos@gmail.com>
# Date:   Sun Sep 12 17:39:04 2021 -0300

#     Merge branch 'master' of github.com:asantos2000/git-course
# ...

# Try to push new branch
git push -v
# fatal: The current branch feature-2 has no upstream branch.
# To push the current branch and set the remote as upstream, use

#     git push --set-upstream origin feature-2

# git push -u origin feature-2 # The same of
git push --set-upstream origin feature-2
# Pushing to github.com:asantos2000/git-course.git
# Enumerating objects: 7, done.
# Counting objects: 100% (7/7), done.
# Delta compression using up to 4 threads
# Compressing objects: 100% (4/4), done.
# Writing objects: 100% (4/4), 451 bytes | 225.00 KiB/s, done.
# Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
# remote: Resolving deltas: 100% (1/1), completed with 1 local object.
# remote: 
# remote: Create a pull request for 'feature-2' on GitHub by visiting:
# remote:      https://github.com/asantos2000/git-course/pull/new/feature-2
# remote: 
# To github.com:asantos2000/git-course.git
#  * [new branch]      feature-2 -> feature-2
# Branch 'feature-2' set up to track remote branch 'feature-2' from 'origin'.
# updating local tracking ref 'refs/remotes/origin/feature-2'

git branch -vv
#   feature-1 d13edc5 [origin/feature-1] Add README.md
# * feature-2 fcd5011 [origin/feature-2] another-file.txt was modified in feature-2 branch
#   master    edf267f [origin/master] Merge branch 'master' of github.com:asantos2000/git-course

# Make another change
git add feature/one-more-file.txt
# [feature-2 5caa7ce] one-more-file.txt was modified in feature-2 branch
#  1 file changed, 2 insertions(+)

git push -v # no ask about renote branch because now feature-2 is tracked
# Pushing to github.com:asantos2000/git-course.git
# Enumerating objects: 7, done.
# Counting objects: 100% (7/7), done.
# Delta compression using up to 4 threads
# Compressing objects: 100% (4/4), done.
# Writing objects: 100% (4/4), 430 bytes | 430.00 KiB/s, done.
# Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
# remote: Resolving deltas: 100% (1/1), completed with 1 local object.
# To github.com:asantos2000/git-course.git
#    fcd5011..5caa7ce  feature-2 -> feature-2
# updating local tracking ref 'refs/remotes/origin/feature-2'

git remote show origin
# * remote origin
#   Fetch URL: git@github.com:asantos2000/git-course.git
#   Push  URL: git@github.com:asantos2000/git-course.git
#   HEAD branch: master
#   Remote branches:
#     feature-1 tracked
#     feature-2 tracked
#     master    tracked
#   Local branches configured for 'git pull':
#     feature-1 merges with remote feature-1
#     feature-2 merges with remote feature-2
#     master    merges with remote master
#   Local refs configured for 'git push':
#     feature-1 pushes to feature-1 (up to date)
#     feature-2 pushes to feature-2 (up to date)
#     master    pushes to master    (up to date)
```

### Updating the Tracking Status of the Branches

```bash
# Create remote branch

git fetch -v
# From github.com:asantos2000/git-course
#  = [up to date]      feature-2  -> origin/feature-2
#  = [up to date]      feature-1  -> origin/feature-1
#  = [up to date]      master     -> origin/master
#  * [new branch]      temp       -> origin/temp

git branch -a
#   feature-1
# * feature-2
#   master
#   remotes/origin/feature-1
#   remotes/origin/feature-2
#   remotes/origin/master
#   remotes/origin/temp

git checkout temp 
# Branch 'temp' set up to track remote branch 'temp' from 'origin'.
# Switched to a new branch 'temp

git branch -vv
#   feature-1 d13edc5 [origin/feature-1] Add README.md
#   feature-2 5caa7ce [origin/feature-2] one-more-file.txt was modified in feature-2 branch
#   master    edf267f [origin/master] Merge branch 'master' of github.com:asantos2000/git-course
# * temp      edf267f [origin/temp] Merge branch 'master' of github.com:asantos2000/git-course

# Delete remote branch

git fetch -v
# From github.com:asantos2000/git-course
#  = [up to date]      feature-1  -> origin/feature-1
#  = [up to date]      feature-2  -> origin/feature-2
#  = [up to date]      master     -> origin/master

git branch -vv
#   feature-1 d13edc5 [origin/feature-1] Add README.md
#   feature-2 5caa7ce [origin/feature-2] one-more-file.txt was modified in feature-2 branch
#   master    edf267f [origin/master] Merge branch 'master' of github.com:asantos2000/git-course
# * temp      edf267f [origin/temp] Merge branch 'master' of github.com:asantos2000/git-course

git remote update origin --prune
# Fetching origin
# From github.com:asantos2000/git-course
#  - [deleted]         (none)     -> origin/temp

git branch -vv
#   feature-1 d13edc5 [origin/feature-1] Add README.md
#   feature-2 5caa7ce [origin/feature-2] one-more-file.txt was modified in feature-2 branch
#   master    edf267f [origin/master] Merge branch 'master' of github.com:asantos2000/git-course
# * temp      edf267f [origin/temp: gone] Merge branch 'master' of github.com:asantos2000/git-course

git branch -d temp # -D to force
# Deleted branch temp (was edf267f).
```

### Removing a Remote Branch Using a Local Terminal

```bash
# Local
git checkout -b temp
# Switched to a new branch 'temp'

# Remote
git push -u origin temp
# Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
# remote: 
# remote: Create a pull request for 'temp' on GitHub by visiting:
# remote:      https://github.com/asantos2000/git-course/pull/new/temp
# remote: 
# To github.com:asantos2000/git-course.git
#  * [new branch]      temp -> temp
# Branch 'temp' set up to track remote branch 'temp' from 'origin'.

git branch -vv
#   feature-1 d13edc5 [origin/feature-1] Add README.md
#   feature-2 5caa7ce [origin/feature-2] one-more-file.txt was modified in feature-2 branch
#   master    edf267f [origin/master] Merge branch 'master' of github.com:asantos2000/git-course
# * temp      edf267f [origin/temp] Merge branch 'master' of github.com:asantos2000/git-course

# Delete remote branch
git push origin -d temp
# To github.com:asantos2000/git-course.git
#  - [deleted]         temp

git checkout master
# M       README.md
# Switched to branch 'master'
# Your branch is up to date with 'origin/master'.

git branch -d temp 
# Deleted branch temp (was edf267f).
```

### Git Show-ref

```bash
git show-ref
# d13edc50e7ef8886435acfbc7e2304f9ea304796 refs/heads/feature-1
# 5caa7ce813be37cac13ffde9682b74878357ab8d refs/heads/feature-2
# edf267f45c7008916c94ad2e514436e0796d2878 refs/heads/master
# d13edc50e7ef8886435acfbc7e2304f9ea304796 refs/remotes/origin/feature-1
# 5caa7ce813be37cac13ffde9682b74878357ab8d refs/remotes/origin/feature-2
# edf267f45c7008916c94ad2e514436e0796d2878 refs/remotes/origin/master

ls .git/refs/heads
# feature-1 feature-2 master

ls .git/refs/remotes/origin 
# feature-1 feature-2 master

git show-ref master # They are sync
# edf267f45c7008916c94ad2e514436e0796d2878 refs/heads/master
# edf267f45c7008916c94ad2e514436e0796d2878 refs/remotes/origin/master

git checkout feature-2
# Switched to branch 'feature-2'
# Your branch is up to date with 'origin/feature-2'.

git show-ref feature-2
# 5caa7ce813be37cac13ffde9682b74878357ab8d refs/heads/feature-2
# 5caa7ce813be37cac13ffde9682b74878357ab8d refs/remotes/origin/feature-2

# Make some changes and commit then

git add file8.txt

git commit -m "Changes in file8.txt - branch feature-2"
# [feature-2 638ed6e] Changes in file8.txt - branch feature-2
#  1 file changed, 3 insertions(+), 1 deletion(-)

git show-ref feature-2 # out of sync
# 638ed6ef6f71e6ff111d67dd0a96b89a81825229 refs/heads/feature-2
# 5caa7ce813be37cac13ffde9682b74878357ab8d refs/remotes/origin/feature-2

git push
# Enumerating objects: 5, done.
# Counting objects: 100% (5/5), done.
# Delta compression using up to 4 threads
# Compressing objects: 100% (3/3), done.
# Writing objects: 100% (3/3), 346 bytes | 346.00 KiB/s, done.
# Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
# remote: Resolving deltas: 100% (1/1), completed with 1 local object.
# To github.com:asantos2000/git-course.git
#    5caa7ce..638ed6e  feature-2 -> feature-2

git show-ref feature-2 # in sync again
# 638ed6ef6f71e6ff111d67dd0a96b89a81825229 refs/heads/feature-2
# 638ed6ef6f71e6ff111d67dd0a96b89a81825229 refs/remotes/origin/feature-2
```

> Change the author of the last commit with `git commit --amend -- author="UserName <user@email>"`

### Pull Requests

### Tags

```bash
git tag

git tag v0.0.1

git tag
# v0.0.1

git show v0.0.1
# commit 36f9202b3718334a9ae8b90ac90fc8c0b516a2d6 (HEAD -> master, tag: v0.0.1, origin/master)
# Merge: 4a64616 7158175
# Author: adsantos2000 <90580368+adsantos2000@users.noreply.github.com>
# Date:   Sun Sep 12 20:13:38 2021 -0300

#     Merge pull request #3 from asantos2000/adsantos2000-patch-1
    
#     Update README.md

# Create new file
echo "Hello git with tags" > new-file1.txt

git add new-file1.txt

git commit -a -m "New file"
```

```bash

```

## References

* [Complete Git Guide: Understand and Master Git and GitHub](https://learning.oreilly.com/videos/complete-git-guide/9781800209855/)
