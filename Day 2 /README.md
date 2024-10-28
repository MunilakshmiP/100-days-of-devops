# Day 2: Introduction to Git and GitHub

## What is Git?

Git is a distributed version control system that helps developers manage changes in source code during software development. Here are some key features:

- **Version Control**: Tracks changes in files, allowing users to revert to previous versions if needed.
- **Branching and Merging**: Enables users to create branches for feature development and merge them back into the main codebase.
- **Collaboration**: Facilitates teamwork by allowing multiple developers to work on the same project without conflict.

## What is GitHub?

GitHub is a web-based platform that uses Git for version control and collaboration. Key features include:

- **Repository Hosting**: Allows users to host their Git repositories online for easy access and sharing.
- **Pull Requests**: Enables developers to propose changes to a project and collaborate on code reviews.
- **Issue Tracking**: Provides tools to track bugs and feature requests, enhancing project management.

## Git Commands Explained

- **`git init`**: Initializes a new Git repository in the current directory.
- **`git add`**: Stages changes in your working directory for the next commit.
- **`git commit`**: Records changes to the repository, including a message describing the changes.
- **`git remote add`**: Adds a remote repository to your local Git configuration, allowing you to push and pull changes.
- **`git push`**: Uploads local repository content to a remote repository.

---

## Exercise 1: Create a Git Repository

1. **Download Git Bash**.
2. **Create a Repository on GitHub named "MyProject"**.

Run the following commands in Git Bash:

```bash
# Configure Git with your username and email
git config --global user.name "Muni**********"
git config --global user.email "*************gmail.com"

# Create a new directory for your project
mkdir MyProject
cd MyProject

# Initialize a new Git repository
git init

# Create a README file
echo "# MyProject is about DevOps" > README.md

# Stage the README file
git add README.md

# Commit the changes
git commit -m "Initial commit with README.md"

# Link the local repository to the GitHub repository
git remote add origin https://github.com/Muni*********/MyProject.git

# Push the changes to GitHub
git push -u origin master
