# git_workflow_basics

# Git & Github Basics Introduction

## Contents

### Part I: Starting with Git
1. Git vs Github, & Linus Torvold
2. cli git
3. github: WEB, CLI
4. Setup: SSH & GPG
5. Do projects & Mini-Projects as Git(hub) repos

## Part II: Git & Work & School
6. Merge Conflicts & Managing Git Repos
7. Cross-Functional Team Git workflow




# 1. Git vs Github, & Linus Torvold
- software versioning & group collaboration
- Linus Torvold made git (2005) for teams doing linux kernel development (which he released in 1991 (see the AT&T vs. U.C.Berkey history)). 
- Github (2008) is a freemium platform for public (and private) git projects. GitHub was purchased by Microsoft in 2018.
- People sometimes used the terms interchangeably, but git exists beyond github.
- a main difference between Github and Git is the convention of the "Pull Request" when submitting code for review and acceptance. (See workflow appendix for part 2.)

### Daily-Use cli git commands (when nothing is wrong)
- git status
- git clone
- git fetch
- git pull
- git restore .
- git branch -a
- git checkout BRANCH_NAME
- git checkout -b NEW_BRANCH_NAME
- git add .
- git commit -m "Hello World"
- git push origin BRANCH_NAME

### Check where you are and if you are up to date.
- shows many things but not everything
```bash
git status
```

### Get code from a link, standard GitHub process
(shows many things but not everything)
- by https
```bash
git clone https://github.com/lineality/definition_behavior_studies.git
```
- by ssh
```bash
git clone git@github.com:lineality/definition_behavior_studies.git 
```


### Fetch and Pull are used when getting new code updates from a repo (when your local code is behind)
- check for updates with fetch
```bash
git fetch
```
- pull updates for your branch into your local files version of the branch
```bash
git pull
```

### Restore one or more files to what they are in the remote code.
(E.g. use when you make a change by mistake.)
- restore all
```bash
git restore .
```
- restore one file
```bash
git restore FILE_NAME
```

### Inspect what all the remote and local branches are.
```bash
git branch -a
```

### Move to a branch
```bash
git checkout BRANCH_NAME
```

### Make your new branch
```bash
git checkout -b NEW_BRANCH_NAME
```

### Add your changes to get reach to commit them
```bash
git add .
```

### Make a commit of code with a helpful description
```bash
git commit -m "Hello World"
```
### Push your code commit to the online 'remote' branch
```bash
git push origin BRANCH_NAME
```

# 3. github: WEB, CLI

### Add files directly with the web interface:
- upload
- create manually



### Edit files directly with web interface
- select a file


### New directories
- prefix file name with new directory name

### Make pull requests directly with the web interface
- https://github.com/lineality/definition_behavior_studies/pulls

# 4. Example git branch workflow for sprint teams
(see appendix)


## # GPG, SSH: Githb Keys https://github.com/settings/keys 
Setting up:
- ssh https://docs.github.com/en/authentication/connecting-to-github-with-ssh 
- gpg https://docs.github.com/en/authentication/managing-commit-signature-verification 

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent   

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account 


## Resources
- https://ohmygit.org/ (Game to learn about git workflow)
- Uma


### References:
- https://en.wikipedia.org/wiki/Git
- https://en.wikipedia.org/wiki/GitHub 
- https://en.wikipedia.org/wiki/Linus_Torvalds 
- https://klarasystems.com/articles/history-of-freebsd-unix-and-bsd/ 



# Appendices

### To move head: e.g. reverting back from a problem

### run git log on both:
1. BRANCH_YOU_ARE_MOVING_THE_HEAD_OF and 
2. the branch you want to move the head to.
```bash
git checkout THAT_BRANCH_NAME
git log
```
And save the top few commit id numbers.


### 1. Go to the branch you want to change. (locally)
```bash
git checkout BRANCH_YOU_ARE_MOVING_THE_HEAD_OF
```

### 2. 'reset' to the commit where you want the head to be. (locally)
```bash
git reset --hard COMMIT_ID__WHERE_YOU_WANT_THE_HEAD_TO_GO
```

### 3. Make those changes to the remote server. (remote master)
```bash
git push --force origin BRANCH_YOU_ARE_MOVING_THE_HEAD_OF
```

#### Tips:
1. test before, test during, test after
2. make a fresh repo clone after head moving.






## Appendix 2: Example Github branch workflow for sprint teams

# When a New Sprint Starts:

Work in a development (dev) branch:
Work (making features) during the sprint will be done in the dev branch in github. 


1. Team Branch Made from dev Branch:
At the start of each sprint, the team lead will create a new branch named for that sprint, as a branch from the dev branch. The team-lead will make a fresh, synced, pull of the dev branch, and from that make the team-branch for that sprint.

e.g. datateam_dev_sprint_5

E.g. cli steps: 
(Note: double checking you are on the right branch with 'branch')
```bash
$ git checkout dev
$ git branch
$ git checkout -b datateam_dev_sprint_5
```


2. Make Team-Member's Individual Branches (implied sub-branches)
Each team member makes their own branch from the team-branch (e.g.
datateam_dev_sprint_5) just with their ~name 
e.g. 
USERNAME

E.g. cli steps: 
(Note: double checking you are on the right branch with 'branch')
```bash
$ git checkout datateam_dev_sprint_5
$ git branch
$ git checkout -b USERNAME
```

This is not a literal sub-branch that will appear in: $ git branch -a
(showing all branches) but rather this is an implied sub-branch for the team's own organization. It is up to the team to compare and merge each branch.

The implied-branching for the team's merge-workflow may look like this when the individual team-member sub-branches are added:
```
datateam_dev_sprint_5/NAME
```


3. Make Feature (sub-sub)Branches:
- For each user feature, story, task, each developer should create feature-branches branched off the sprint branch e.g (em/fix-delete-api).

- Developers work on their respective features in isolation.


The implied-branching for the team's merge-workflow may look like this when the individual feature-branches are added:
```
datateam_dev_sprint_5/USERNAME/new_delete_doc_endpoint
datateam_dev_sprint_5/USERNAME/fix_delete_voice_endpoint
datateam_dev_sprint_5/USERNAME/new_delete_all_docs_endpoint
datateam_dev_sprint_5/USERNAME/new_get_doc_endpoint 
      ```
Note: $ git branch -a will simply list all branches literally, not reflecting how people want to organize these branches as a hierarchy of branches and sub-branches, etc. 


4. Submitting ~finished Features to the team-branch:
When a team-member is done making and testing their feature-code (in their sub-sub-sub branch), they will do a pull-request to merge that code into the team-sprint branch.
```bash
	$ gh pr create {from branch to branch}...
	```
Throughout the week there will be pr (pull requests) from individuals to the team-sprint-branch. Then at the end of the sprint the whole team branch will be submitted by pr (pull request) to the dev branch.

As in/when you have branch-conflict issues.

4. During Sprint (within the team):
Throughout the sprint, the team will conduct testing and code reviews to determine when individual features can/should be merged into the team-branch.

Then at the end of the spring the team branch (with all the new features merged) will be submitted in a pull request to the overall project manager to be merged into the Dev-Branch.


5. After the sprint-team-pull-request is accepted, the team moves on to new features in the next sprint repeating the above workflow. Other staff will handle migrating code up through stages and into production.


## Best Practice

6. Regular Merging:
Periodically merge changes from feature branches into the team-sprint-branch to keep it up to date.

7. Code Reviews:
Team lead should conduct code reviews for feature branches before merging into the sprint branch.

8. Testing:
Team and lead should do testing of various kinds on the feature-branches before merging into the sprint branch, and on the final combination of features. There is no guarantee that code working before merging on one local system will work in docker or AKS after merging in other environments. 
- unit testing
- error message testing
- stress testing
- input-fuzzing testing
- package version testing
- os version testing
- dockerfile testing

## Pull Request
Create a pull request: You can use the GitHub CLI to create a pull request with 
```
$ gh pr create
```
You'll be prompted for details like the pull request title and body, and which branch you want to merge your changes into.

- Pull from the personal-sub-sprint-team-sub-feature branch to the: team-sprint branch
(which is right to left in github gui...not left the right in written language)
```
Team-Spring(branch) <- specific feature-branch
```



