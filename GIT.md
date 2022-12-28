(Github CLI Docs)[https://docs.github.com/en/get-started/importing-your-projects-to-github/importing-source-code-to-github/adding-locally-hosted-code-to-github]


```shell
#Initialising
git init -b main
git add . && git commit -m "initial commit"
gh repo create
    
#Configuration
>> git config --global user.name "<UserName>"
>> git config --global user.email "<Email>"

#Initialising
>> git init                                   #Initialise repo
>> git status                                 #Get repo status

#Committing
>> git add .                                  #Stage all modified or new files
>> git commit -m "<message>"                  #Commit with a message

#Branches
>> git branches                               #List brances
>> git branch <new-branch-name>               #Create a new branch
>> git branch -d <branch-to-delete-name>      #Delete a branch
>> git checkout master                        #Revert back to the master branch
>> git checkout <commitHash>                  #Revert back to a previous commit

#Making Changes
>> git merge <branch-to-merge-name>           #Merge a branch with this one
>> git pull --all                             #Get all new changes, merges remote file changes into the local repo
>> git push origin main                       #Push committed changes (for everyone else)
```

Git Rebase 