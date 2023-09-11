# GIT PROJECT

 ## Prequisite :

 - Install git 
 - Create a Github account or sign into a Git account 

## Initializing Git Repository

   Steps : 

   - Open Git Bash

   - Create or make Directory ; Run `mkdir Project2` on Terminal 

   - Change or Move into the folder 'Project2' : Run `Project2`

   - Once inside the 'project2 folder' : Run `git init`

   ![Alt text](<Images/initializing Repo.png>)


## Making First Commit 

  Note : In Git to 'COMMIT' means to save changes made to a file.

  Steps : 

   - Inside the working directory create a file index.txt : Run `touch index.txt`
    
   -  write ' I am happy to be part of the Git project' and save changes ; 

   - Run `echo "I am happy to be part of the Git Project" > index.txt`

   - Add changes to git staging area : Run `git add .`

   - To commit changes to git : Run `git commit -m "practice commit"`

   ![Alt text](<Images/Making first commit.png>)


## Working with Branches

 **Making a new branch**

 Steps;

To make a "new branch" Run : `git branch (name)`

- i.e Run : `git branch project2`

![Alt text](<Images/creating a new Branch.png>)


## Listing Git Branches

To list git branches : 

- Run `git branch`

![Alt text](<Images/listing branches.png>)


## Change into Old branch

- Run `git checkout (branch name)`

- i.e present branch is "project2" , to switch back to "main" branch

- Run `git checkout main`

![Alt text](<Images/git checkout.png>)


## Merging Branch into another Branch

- Run `git merge (B)` i.e to add comment from Branch B into A

To add comments from "project2" Branch into the "main" Branch

- Run `git merge main`

![Alt text](<Images/git merge.png>)

## Deleting a Git Branch 

To delete a git branch : Run ` git branch -d (branch name)`

- i.e `git branch -d project2`

![Alt text](<Images/git delete.png>)


# Collaborating and Remote Repositories

## Creating a Github account
  
  To create a Github account: Visit github.com

  ![Alt text](<Images/Git hub.png>)


## Creating first repository

steps : 
- Click on the plus sign on the top right corner of the github account 

- Click on new repository to create a new one 

- add a unique name, description and tick Readme to add a readme file 

![Alt text](<Images/gitHub account.png>)


## Pushing local git repository to Remote git repository.

- Run `git remote add origin ( remote repository link )`

![Alt text](<Images/git remote add.png>)


**To push into remote repository**

- Run `git push origin (branch name)`

- i.e `git push origin main`

![Alt text](<Images/git push.png>)


# Branch Management and Tagging


 1. **To create a HEADING**

   - Run `# Project 1`

       `## Project 1`

       `### Project 1`

       ![Alt text](<Images/markdown Heading.png>)


2. To create a Emphasis
   
   Use asterick

   - Run `*Italic*`
     
      `**Bold**`

      ![Alt text](Images/Italic.png)


3. To create a list (ordered and unordered list)

   **Unodered list**

   - Item1

   - Item2

   - Item3


   **ordered list**

   1. Item1

   2. Item2

   3. Item3


4. To Create a Hyperlink 

   - Run `[text link]`(www.darey.io)

   - i.e [darey.io](www.darey.io)


5. To display Images

   - Run `![Alt Text](https://example.com/image.jpg)`

   - i.e ![Alt text](Images/Italic.png)


6. To display code snippet

   - Run `console.org(welcome to darey)`



      





 

 

 






  

