<details>
<summary>Exercise 0: Clone Git Repository</summary>
<br />

**Tasks:**
- clone the git repository `git@gitlab.com:devops-bootcamp3/node-project.git`
- create your own project/git repo from it

**Steps to solve the tasks:**

```sh
git clone git@gitlab.com:devops-bootcamp3/node-project.git
cd node-project

# remove remote repo reference
rm -rf .git
# create your own local repository and commit its content
git init 
git add .
git commit -m "Initial commit"

# create git repository on GitHub push your newly created local repository to it
git remote add origin git@github.com:fsiegrist/devops-bootcamp-05-cloud-iaas-basics.git
# rename master branch of original Gitlab repository to main (default on GitHub)
git branch -M main
# push your newly created local repository to it
git push -u origin main
```

</details>

******