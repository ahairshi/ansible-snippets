# ansible-snippets


```yaml
---
- name: debug module demo
  hosts: all
  vars:
    fruit: "Apple"
    
  tasks:
    - name: Debug Message Prints Hello World 
      ansible.builtin.debug:

    - name: Customized Debug Message
      ansible.builtin.debug:
        msg: "Example Text Message"
    
    - name: Display fruit Variable
      ansible.builtin.debug:
        var: fruit
    
    - name: Using jinja Template to display fruit variable
      ansible.builtin.debug:
        msg: "The Fruit is {{ fruit }}" 

    - name: Task with Verbosity 2
      ansible.builtin.debug:
        verbosity: 2

```
## Verbosity Skipped
<img width="1440" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/ab35cfa5-6993-46bc-b14b-7fcdd091a0dd">

## Verbosity not skipped

<img width="1440" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/3fb38e53-9f8c-4d23-a02a-2a5725c48973">


```yaml
---
- name: pause module demo
  hosts: all
  vars:
    wait_seconds: 10
  tasks:
    - name: pause for {{ wait_seconds | int }} second(s)
      ansible.builtin.pause:
        seconds: "{{ wait_seconds | int }}"

    - name: message
      ansible.builtin.debug:
        msg: "The end"
```

<img width="844" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/2ebf92b5-4eee-4616-b008-a9638f57b977">

```yaml
---
- name: extra variable demo
  hosts: all
  gather_facts: no
  vars:
    fruit: "banana"
  tasks:
    - name: print message
      ansible.builtin.debug:
        msg: "fruit is {{ fruit }}"

```

<img width="840" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/48d51b5a-f2b8-41aa-a381-dfa17f50f15a">

## The Basics: | and > Operators
In Ansible, breaking a string over multiple lines is accomplished using two main operators:

* | (Literal Block Scalar): This operator instructs Ansible to treat the string as a literal block scalar, preserving the newlines within the string.
* \> (Folded Block Scalar): This operator tells Ansible to treat the string as a folded block scalar, collapsing all newlines into a single space.

https://ansiblepilot.medium.com/how-to-break-a-string-over-multiple-lines-with-ansible-and-yaml-73cd5909fae8#:~:text=The%20Basics%3A%20%7C%20and%20%3E%20Operators,the%20newlines%20within%20the%20string.

```yaml
- name: debug module demo
  hosts: all
  gather_facts: no
  vars:
    variable1: |
      exactly as you see
      will appear these three
      lines of poetry
    variable2: >
      this is really a
      single line of text
      despite appearances
    variable3: |-
      exactly as you see
      will appear these three
      lines of poetry
    variable4: >-
      this is really a
      single line of text
      despite appearances
  tasks:
    - name: print variable1
      ansible.builtin.debug:
        var: variable1
    - name: print variable2
      ansible.builtin.debug:
        var: variable2
    - name: print variable3 with no newline at the end- Literal Block Scalar
      ansible.builtin.debug:
        var: variable3
    - name: print variable3 with no newline between Strings- Literal Block Scalar
      ansible.builtin.debug:
        msg: "{{ variable3.split('\n') }}"
    - name: print variable4 with no new line - Folded Block Scalar
      ansible.builtin.debug:
        var: variable4
```
<img width="1440" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/35932a79-cf89-47ad-af94-ddff701f683f">


## Ansible terminology — ansible_hostname vs inventory_hostname vs ansible_fqdn

https://ansiblepilot.medium.com/ansible-terminology-ansible-hostname-vs-inventory-hostname-vs-ansible-fqdn-ae44d2acc484
https://www.middlewareinventory.com/blog/ansible-inventory_hostname-ansible_hostname-variables/


## Set remote environment per task or play - Ansible environment statement
https://www.ansiblepilot.com/articles/set-remote-environment-per-task-or-play-ansible-environment-statement/

```yaml
---
- name: remote environment demo
  hosts: all
  gather_facts: false
  environment:
    EXAMPLE: test1

  tasks:
    - name: diplay EXAMPLE Playbook level
      ansible.builtin.command: "echo $EXAMPLE"

    - name: diplay EXAMPLE Task Level
      ansible.builtin.command: "echo $EXAMPLE"
      environment:
        EXAMPLE: test2
```
<img width="1440" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/c0789872-3769-418b-b0e2-8ebfa7aac78c">

## Execute command on the Ansible host — Ansible localhost

https://ansiblepilot.medium.com/execute-command-on-the-ansible-host-ansible-localhost-71fa92459fe1

https://www.shellhacks.com/ansible-run-shell-command-on-remote-host/

https://medium.com/margarytachepiga/ansible-beggining-b64d578ed7d5

```yml
---
- name: localhost demo
  hosts: localhost
  vars:
    ansible_connection: local
    ansible_python_interpreter: "{{ ansible_playbook_python }}"
  tasks:
    - name: print hostname
      ansible.builtin.debug:
        msg: "{{ inventory_hostname }} -  {{ ansible_python_interpreter }}"
```
<img width="833" alt="image" src="https://github.com/ahairshi/ansible-snippets/assets/1314201/bc42de44-ccb1-4730-a4a0-0485db61beac">

## Three options to Safely Limit Ansible Playbooks Execution to a Single Machine

https://ansiblepilot.medium.com/three-options-to-safely-limit-ansible-playbooks-execution-to-a-single-machine-f4abc107246f

## Ansible modules - command vs shell

https://www.ansiblepilot.com/articles/ansible-modules-command-vs-shell/ **to be watched again**

## Write a Variable to File — Ansible module copy vs template
https://ansiblepilot.medium.com/write-a-variable-to-file-ansible-module-copy-vs-template-2ef51c67ebdc

## How to Run Only One Task in Ansible Playbook? — Ansible tags statement

https://ansiblepilot.medium.com/how-to-run-only-one-task-in-ansible-playbook-ansible-tags-statement-1c5d007370bb

## Filter A List By Its Attributes — Ansible selectattr filter

https://www.educative.io/answers/how-to-filter-a-list-by-its-attributes-in-ansible

https://ansiblepilot.medium.com/filter-a-list-by-its-attributes-ansible-selectattr-filter-66881fe8a825

## Using Date, Time and Timestamp in Ansible Playbook - Ansible Tip and Tricks
https://www.ansiblepilot.com/articles/using-date-time-and-timestamp-in-ansible-playbook-ansible-tip-and-tricks/

## Using Date, Time and Timestamp without Facts in Ansible Playbook - Ansible date and lookup plugin
https://www.ansiblepilot.com/articles/using-date-time-and-timestamp-without-facts-in-ansible-playbook-ansible-date-and-lookup-plugin/
