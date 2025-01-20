### How to resolve foxtrot merge in bitbucket

#### HOw to prevent foxtrot merge in bitbucket
``` console
git switch develop
git pull
git switch feature/abc
git merge develop --no-ff
git push origin feature/abc
```


The target branch, also known as the base branch, is the branch that you want to merge your changes into.

If you are already on the target branch, skip this step.
``` console
git switch <target-branch>
git pull
``` 

Reset the local branch to match the remote branch:
This step is only necessary if you have made local changes that you want to discard.
``` console
git reset --hard origin/<target-branch>
```


Create a new branch for merging the changes:
Choose a meaningful name for the merge branch.
``` console
git checkout -b <merge-branch>
```


Merge the branch with the foxtrot changes into the merge branch:

``` console
git merge <foxtrot-branch>
```
Resolve any conflicts that arise during the merge.

Commit the changes and push them to the remote repository:
``` console
git add --all 
git commit -m "merged conflicts"
git push origin <merge-branch>
```
Create a pull request for the merge branch and merge the changes:
Go to the Bitbucket repository and select the merge branch.
Click the "Create pull request" button.
Choose the target branch as the base and the merge branch as the compare branch.
Review the changes and click the "Merge" button to merge the changes into the target branch.
By following these steps, you should be able to successfully resolve a foxtrot merge in Bitbucket.

```mermaid
gitGraph
    branch develop
    commit id: "1"
    branch feature1
    checkout develop
    branch merge-conflict-branch
    commit id: "2"
    checkout feature1
    commit id: "3"
    merge develop
    checkout merge-conflict-branch
    commit id: "commit with merge conflict"
    checkout develop
    branch branch-to-resolve-conflict
    merge merge-conflict-branch
    checkout develop
    merge branch-to-resolve-conflict
```
@startmermaid
pie title Pets adopted by volunteers
"Dogs" : 386
"Cats" : 85
"Rats" : 35
@endmermaid

```mermaid!
piedfdf title Pets adopted by volunteers
  "Dogs" : 386
  "Cats" : 85
  "Rats" : 35
```