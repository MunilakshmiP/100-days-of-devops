#  YAML Basics and Creating Ansible Playbooks
Welcome to Day 87 of my  **100 Days of DevOps**  journey! Today, we're diving into YAML (Yet Another Markup Language) and exploring how to use it to create Ansible playbooks for infrastructure automation. Let's break it down step-by-step.

----------

## [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-what-is-yaml "Permalink")**What is YAML?**

YAML stands for "Yet Another Markup Language" and is commonly used in configuration files due to its simplicity and readability. It follows a human-readable data format and is heavily used in DevOps tools like Ansible, Kubernetes, and Docker Compose.

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-key-features-of-yaml "Permalink")**Key Features of YAML:**

-   **Readable**: Uses indentation for structure.
    
-   **Data Types**: Supports scalars, lists, and dictionaries.
    
-   **Key-Value Pairs**: Defines configuration with ease.
    

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-basic-yaml-syntax "Permalink")**Basic YAML Syntax:**

1.  **Key-Value Pairs**:


```
key: value

```

2.  **Lists**:

```
fruits:
  - apple
  - banana
  - cherry

```

3.  **Dictionaries**:


```
person:
  name: John
  age: 30

```

4.  **Comments**:

```
# This is a comment
key: value

```

> **Pro Tip:**  Indentation in YAML uses spaces, not tabs. Consistency is crucial to avoid parsing errors.

----------

## [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-ansible-and-yaml "Permalink")**Ansible and YAML**

Ansible uses YAML to define playbooks, which are scripts that describe how Ansible should automate tasks.

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-structure-of-an-ansible-playbook "Permalink")**Structure of an Ansible Playbook:**

-   **Hosts**: The group of machines where tasks will run.
    
-   **Tasks**: The actions to perform on the hosts.
    
-   **Modules**: The tools to execute specific tasks (e.g.,  `shell`,  `copy`,  `apt`).
    

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-sample-ansible-playbook "Permalink")**Sample Ansible Playbook**

Copy

Copy

```
---
- name: Install and start Apache web server
  hosts: webservers
  become: yes
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present

    - name: Start Apache service
      service:
        name: apache2
        state: started

```

**Explanation:**

-   `---`: Indicates the start of a YAML document.
    
-   `name`: Provides a description of the play or task.
    
-   `hosts`: Specifies the target machines.
    
-   `become: yes`: Elevates privileges to perform tasks as root.
    

----------

## [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-hands-on-deploying-a-web-server-using-ansible "Permalink")**Hands-On: Deploying a Web Server Using Ansible**

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-step-1-prerequisites "Permalink")**Step 1: Prerequisites**

-   Ansible installed on your control node.
    
-   SSH access to the target servers.
    
-   An inventory file specifying your servers.
    

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-step-2-create-an-inventory-file "Permalink")**Step 2: Create an Inventory File**

Copy

Copy

```
[webservers]
192.168.1.100
192.168.1.101

```

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-step-3-write-the-playbook "Permalink")**Step 3: Write the Playbook**

Save the following YAML code as  `deploy_webserver.yml`:

Copy

Copy

```
---
- name: Deploy Apache Web Server
  hosts: webservers
  become: yes
  tasks:
    - name: Update apt repository cache
      apt:
        update_cache: yes

    - name: Install Apache
      apt:
        name: apache2
        state: present

    - name: Ensure Apache is running
      service:
        name: apache2
        state: started

    - name: Copy custom index.html
      copy:
        src: /path/to/index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'

```

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-step-4-execute-the-playbook "Permalink")**Step 4: Execute the Playbook**

Run the playbook using the  `ansible-playbook`  command:

Copy

Copy

```
ansible-playbook -i inventory deploy_webserver.yml

```

----------

## [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-practical-exercises "Permalink")**Practical Exercises**

1.  **Modify the Playbook:**
    
    -   Add tasks to install additional packages like  `curl`  or  `git`.
        
    -   Include a step to create a backup of the existing  `index.html`  file.
        
2.  **Use Variables in Playbooks:**  Create a playbook that uses variables for package names and file paths:
    
    Copy
    
    Copy
    
    ```
     ---
     - name: Deploy Web Server with Variables
       hosts: webservers
       vars:
         web_package: apache2
         html_path: /var/www/html/index.html
       tasks:
         - name: Install Web Server
           apt:
             name: "{{ web_package }}"
             state: present
    
         - name: Ensure Web Server is Running
           service:
             name: "{{ web_package }}"
             state: started
    
    ```
    
3.  **Challenge Yourself:**
    
    -   Write a playbook to install and configure MySQL.
        
    -   Automate the deployment of a static website hosted on multiple servers.
        

----------

## [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-interactive-section "Permalink")**Interactive Section**

To make learning more engaging, answer these questions:

1.  **What will happen if you miss the**  `---`  at the start of a YAML document?
    
2.  **What is the purpose of the**  `become: yes`  directive in Ansible playbooks?
    
3.  **How would you handle errors in an Ansible playbook to ensure the script continues executing?**
    

Post your answers in the comments or try them out in your own Ansible environment!

----------

### [](https://100daysdevops.hashnode.dev/day-87-of-100-days-yaml-basics-and-creating-ansible-playbooks#heading-closing-thoughts "Permalink")**Closing Thoughts**

YAML is a cornerstone of configuration in DevOps, and Ansible playbooks offer a powerful way to automate infrastructure tasks. Mastering these tools will make you a more efficient and capable DevOps engineer.

Stay tuned for Day 88 as we continue to unlock more DevOps secrets. Feel free to share your thoughts or ask questions in the comments section. Let’s keep learning together!
