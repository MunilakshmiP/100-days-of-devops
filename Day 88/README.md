# Getting Started with Ansible Galaxy and Roles

Welcome back to Day 88 of our  **100 Days of DevOps**  journey! Today, we’ll explore how to organize, manage, and reuse your automation workflows using  **Ansible Galaxy**  and  **Roles**. Let’s dive in!

----------

### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-why-use-ansible-roles "Permalink")Why Use Ansible Roles?

As your Ansible Playbooks grow in complexity, they can become lengthy and difficult to manage. For instance:

-   A single Playbook with  **50+ tasks**,  **20 variables**, handlers, and metadata can easily exceed 2000 lines of YAML.

This is where  **Ansible Roles**  come in! Roles modularize your automation into reusable components, improving:

-   **Readability**: Break down Playbooks into smaller files.
    
-   **Reusability**: Share and reuse roles across multiple projects.
    
-   **Collaboration**: Work effectively with teams using predefined structures.
    

----------

### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-what-are-ansible-roles "Permalink")What Are Ansible Roles?

**Ansible Roles**  are a standardized way to organize your Playbooks by splitting them into smaller, logical components within a predefined folder structure. This structure makes it easier to manage variables, tasks, handlers, and templates.

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-folder-structure-of-a-role "Permalink")Folder Structure of a Role

When you create a role, it generates the following structure:

Copy

Copy

```
roles/
  └── <role_name>/
      ├── tasks/
      │   └── main.yml
      ├── handlers/
      │   └── main.yml
      ├── vars/
      │   └── main.yml
      ├── defaults/
      │   └── main.yml
      ├── files/
      ├── templates/
      ├── meta/
      │   └── main.yml
      └── README.md

```

Each folder has a specific purpose:

-   **tasks/**: Contains tasks to execute.
    
-   **handlers/**: Defines handlers triggered by tasks.
    
-   **vars/**  and  **defaults/**: Store variables.
    
-   **files/**  and  **templates/**: Store static files and templates.
    
-   **meta/**: Contains metadata about the role.
    

----------

### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-what-is-ansible-galaxy "Permalink")What Is Ansible Galaxy?

**Ansible Galaxy**  is a platform for discovering, sharing, and reusing Ansible content, including roles and collections. Think of it as a package manager for Ansible automation.

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-why-use-ansible-galaxy "Permalink")Why Use Ansible Galaxy?

-   **Speed**: Download prebuilt roles instead of writing them from scratch.
    
-   **Collaboration**: Share your roles with the community.
    
-   **Consistency**: Follow standardized practices for roles and collections.
    

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-key-commands-in-ansible-galaxy "Permalink")Key Commands in Ansible Galaxy

1.  **Initialize a Role**:
 
    
    ```
     ansible-galaxy role init <role_name>
    
    ```
    
    Example:

    
    ```
     ansible-galaxy role init apache_setup
    
    ```
    
    This generates the folder structure for the  `apache_setup`  role.
    
2.  **Install a Role**: Download roles from Ansible Galaxy:
   
    
    ```
     ansible-galaxy install <role_name>
    
    ```
    
3.  **List Installed Roles**:

    
    ```
     ansible-galaxy list
    
    ```
    
4.  **Share a Role**: Upload your role to Ansible Galaxy:

    
    ```
     ansible-galaxy role publish
    
    ```
    

----------

### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-example-using-ansible-galaxy-and-roles-together "Permalink")Example: Using Ansible Galaxy and Roles Together

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-scenario "Permalink")Scenario:

You want to install Apache and deploy a web application using a role.

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-step-1-create-a-role "Permalink")Step 1: Create a Role

Initialize a new role:


```
ansible-galaxy role init apache_web

```

This creates a role with the necessary folder structure in  `roles/apache_web/`.

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-step-2-define-the-roles-tasks "Permalink")Step 2: Define the Role’s Tasks

Edit  `roles/apache_web/tasks/main.yml`:


```
---
- name: Install Apache
  apt:
    name: apache2
    state: present

- name: Deploy Web Application
  copy:
    src: /path/to/app
    dest: /var/www/html

```

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-step-3-use-the-role-in-a-playbook "Permalink")Step 3: Use the Role in a Playbook

Create a Playbook  `site.yml`  to call the role:


```
---
- hosts: web
  become: true
  roles:
    - apache_web

```

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-step-4-run-the-playbook "Permalink")Step 4: Run the Playbook

Execute the Playbook:


```
ansible-playbook -i inventory site.yml

```

#### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-step-5-share-the-role "Permalink")Step 5: Share the Role

To share the role on Ansible Galaxy:

1.  Create a Galaxy account.
    
2.  Package your role and publish it using:

    
    ```
     ansible-galaxy role publish
    
    ```
    

----------

### [](https://100daysdevops.hashnode.dev/day-88-of-100-days-getting-started-with-ansible-galaxy-and-roles#heading-benefits-of-ansible-galaxy-roles "Permalink")Benefits of Ansible Galaxy + Roles

By combining Ansible Galaxy and Roles, you can:

-   Leverage community-contributed roles for common tasks.
    
-   Standardize your automation workflows.
    
-   Save time and effort by reusing existing content.
