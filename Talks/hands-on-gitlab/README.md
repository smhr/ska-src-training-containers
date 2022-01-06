## Objectives and scope

In this section we will show how to use GitLab to share results with the community or your colleagues. You will be able to share code, text documents, figures or notebooks, which can be rendered automatically.

Overall steps: 

- Start an account
- Start a repository (Description, README, LICENSE)
- Upload / Add / Create files and folders
- Make changes to file and commit them
- View differences and history
- Share your work!

We will use GitLab, but there are other platforms that offer very similar services and work in almost the same way. We recommend you take a look at GitHub, and BitBucket as perfectly viable alternatives. 

## What is GitLab and how does it work

GitLab is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere. Developing your project or analysis collaboratively on GitLab or GitHub provides a prompter to document your work in detail and it provides a great opportunity to get additional contributors to your idea. Contributions can be everything from new ideas, to bug reports and actual code contributions.

The platform uses version control via git command, so you will have a complete history of all the changes for all the files, and when and who commited those changes. So no more files ending with `_v2_final_reviewed_Feb_finalfinal.pdf`. Additionally, you have an issue tracker to focus discussions on specific topics easy, a build-in wiki, and even space to host web pages.


## Starting

To start working with GitLab you need to have a GitLab user account, using any of the authentication methods provided. To proceed, visit 

- `https://gitlab.com/users/sign_in`

Once registered, you can create projects, repositories, open tickets, fork other repositories and share your work, among many other features.

## Welcome to GitLab

### Create a project

In GitLab, repositories are grouped by projects, so the first thing we need to create is a project that will host different related repositories.

To do this, from the Projects menu, select "New Project" or "Create new project":

![Create New Project - 1](./media/create_new_project_1.png)

![Create New Project - 2](./media/create_new_project_2.png)

After this, select to create a new blank project:

![Create New Project - 3](./media/create_new_project_screen.png)

Now it is time to indicate the project details and the name of the repository. In the image below we include the project name, the short name, the project description and the visibility of the repository:

![Create New Project - 4](./media/create_new_project_details.png)

### Working with our repository

Once the repository has been created, the initial screen of the repository will display the following:

![New Repository - Main Screen](./media/show_repository_mainscreen.png)

### Adding content: Updating

By default the repository is created with a `README.md` file as an example. Whenever there is a `README.md` file in a directory in the repository, it will be taken as documentation or repository information. 

Now we are going to modify the `README.md` file so that it has other information related to our work. To do this, it is possible to edit the content of the stored files by selecting the file and clicking on *"Edit in Web IDE"*:

![Adding Content - Update exisisting](./media/modify_readme_content.png)

Here we include some textual information about the project and repository using a format called MarkDown to compose it (you can check the syntax [here](https://www.markdownguide.org/basic-syntax/) ).

![Adding Content - Screen Update exisisting](./media/commit_modify_readme_content.png)

After including some content, what we want to do is to save the work done so far, this is what we call a "Commit", so those changes are ready to be saved. By committing the "Commit", 

![Adding Content - Commit Update exisisting](./media/confirm_commit_mudy_readme_content.png)

To identify the "Commit" it is essential to include a message giving a brief summary of the changes and to decide whether the changes will go to a new development branch or feature.

![Adding Content - Commit Update exisisting](./media/confirm_commit_modify_readme_content.png)

We go back to the repository home screen and you can see the changes made.

![Main Screen After update](./media/goto_main_screen.png)

### Adding content: New file

