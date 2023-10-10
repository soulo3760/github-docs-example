# Terraform Beginner Bootcamp 2023

## Writing Good Documentation 

codeblocks are very easy to *copy and paste* and share code. 
A good **cloud engineer** needs to support _future_reviewers_ and users of the code.


```
---
- name: Automate Terraform
  hosts: localhost
  become: yes
  tasks:
    - name: Update apt cache (for Ubuntu)
      apt:
        update_cache: yes
      when: ansible_os_family == "Debian"

    - name: Install Terraform
      command: >
        curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
        && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
        && sudo apt-get update && sudo apt-get install terraform
      when: ansible_os_family == "Debian"

    - name: Install Terraform (for RedHat-based systems)
      command: >
        sudo yum install -y dnf-plugins-core
        && sudo dnf config-manager --add-repo https://rpm.releases.hashicorp.com/$release/hashicorp.repo
        && sudo dnf -y install terraform
      when: ansible_os_family == "RedHat"

    - name: Clone Terraform configuration from Git (if needed)
      git:
        repo: https://github.com/your/repo.git
        dest: /path/to/terraform-project
        version: main  # Replace with the branch or tag you want to use
      ignore_errors: yes
      when: not ansible_check_mode

    - name: Change directory to the Terraform project
      ansible.builtin.cd:
        path: /path/to/terraform-project

    - name: Initialize Terraform
      command: terraform init
      when: not ansible_check_mode

    - name: Apply Terraform changes
      command: terraform apply -auto-approve
      when: not ansible_check_mode

    # Additional tasks like running tests or capturing outputs can be added here

    # To destroy resources created by Terraform, use:
    # - name: Destroy Terraform resources
    #   command: terraform destroy -auto-approve
    #   when: not ansible_check_mode
````
## choose your editor using GFM task lists

-[x] visualstudio
-[x] online cli

# use emojis  and markdown tables 
## GFM  github Flavoured Markdown [<sup>[2]</sup>](#references)
| name | shortcode | Emoji|
| -----| ---- |----|
|cloud| :cloud:| 🌩️|


## References 
- [Github flavoured markdown specs](https://cran.r-project.org/web/packages/gluedown/vignettes/github-spec.html)

- [Github Flavored Markdown cheatsheet](https://www.google.com/search?q=Github+flavoured+markdown+examples&oq=Github+flavoured+markdown++examples&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIICAEQABgWGB4yCAgCEAAYFhgeMggIAxAAGBYYHjIICAQQABgWGB4yCAgFEAAYFhgeMgoIBhAAGIYDGIoFMgoIBxAAGIYDGIoFMgoICBAAGIYDGIoFMgoICRAAGIYDGIoF0gEIODc5OWowajSoAgCwAgA&sourceid=chrome&ie=UTF-8#:~:text=Github%20Flavored%20Markdown%20cheatsheet)
