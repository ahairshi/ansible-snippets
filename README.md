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


