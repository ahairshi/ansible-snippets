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

