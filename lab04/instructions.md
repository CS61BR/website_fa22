---
parent: "Lab 04: Git and Debugging"
title: Instructions
nav_order: 1
---

## Starting the Lab

 - Open the `lab04/` folder in your preferred text editor.
 - Open the `lab04/` folder in your preferred terminal.
 - Run `git pull skeleton main` to get the latest version of the skeleton code for this lab.

## Experiencing a Merge Conflict

{: .warning}
> This portion of the lab may mess up your local Git repository. Make sure to commit and push all your work to Github before starting this portion of the lab; run `git status` and make sure it says "On branch main; Your branch is up to date with 'origin/main'; nothing to commit, working tree clean" before continuing.
>
> If things go horribly wrong, you can just delete your local repository, re-clone it from Github (see lab01 setup), and start this section over.

You may have heard dark rumors of a terrible monster called a "merge conflict". It's a hideous beast that destroys mercilessly and strikes fear into the hearts of experienced developers. 

Today you're going to create one!

 - Open up your browser and go to your repository on Github. In the `lab04/` folder, open `poem.txt`, and click the edit button. Notice that the 3rd verse has a missplelling: it says "l337", but that should be "great". Fix the missplelling and commit your change on Github. (Note: if you come back to this step, you can pick a new word besides "great". Some candidates: "green", "leek", "beet", "leaf")
 - In your text editor (working in the local `lab04/` folder), open `poem.txt`. Strange, the missplelling is still there! However, this time, change the word "l337" to "elite".
 - In the terminal, add and commit your change.
 - Run `git push`. You should get an error: "the remote has work that you do not have locally". Oops!
 - To get the remote's work, run `git pull`. You should receive the following message:
    ```
    Auto-merging lab04/poem.txt
    CONFLICT (content): Merge conflict in lab04/poem.txt
    Automatic merge failed; fix conflicts and then commit the result.
    ```
    Oh no! It's a merge conflict!
 - In your text editor, open `poem.txt`. You should see a section that looks like:
    ```
    <<<<<<< HEAD
    I use aliases that make me feel elite,
    =======
    I use aliases that make me feel great,
    >>>>>>> 1053959eab016f9b0ba8608d83291c8b19bb330d
    ```
    This is the merge conflict! Since "elite" actually rhymes, let's keep the line with "elite". Delete the 4 extra lines (the 3 lines with the strange symbols, and the line with "great").
 - Add and commit `poem.txt`. This is the "merge commit". 
 - Push your change to Github. Congratulations, you've survived a merge conflict!

## Enterprise Software Development


Your company, Flik Enterprises, has released a fine software library (`flik.rs`) that is able to determine whether two Integers are the same or not.

You receive an email from someone named "Horrible Steve" who describes a problem they're having with your library:
> Dear Flik Enterprises,
> 
> Your library is very bad. See the attached code. It should be printing "Incorrect. Access Denied", but is printing "Correct. Access Granted."
>
> (attachment: main.rs)

If you run the program with `cargo run`, you'll see that it indeed prints "Correct. Access Granted". Figure out whether the bug is in Horrible Steve's code or in Flik Enterprise's library, and fix the bug.
