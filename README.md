In this project we are doing tasks in server 2 from server 1 using ansible scripts... all works will do by a single command "ansible-playbook task_name.yml"
benefits of this project:
    -server2 will be always safe
    -no need to share the server2'spem file with anyone
    -you can do some complex tasks using simple commands
    - you can use this project for a high number of users.
    - we assume that server1 is the super server of the company that will manage all cloud accounts.
    - and if any new project comes then it will provide a new instance for this specific task.
    - in pub files, you can save the public keys of all of your employees.
    
 first, it will do the task and then break the connection, so if you want to do the tasks again you have to build a connection again between these 2 servers.
  
  
  
first of all you need to add public key of server1 to server2's authorized_keys(/home/ubuntu/.ssh/)
and then go to ansible hosts file(/etc/ansible/hosts) and these lines(in server1):
[webservers]
<server2 ip>   ansible_user=ubuntu

  
  
  and your setup is ready now let's talk about each file...
about create-user.yml
  - in this file, you can create users in server2 from server1
  - first, it will ask for the name of the users you want to create(you can create multiple users: user.name1,user.name2,user.name3,,,, and many more)
  - it will install some packages in server2 like acl(useful for third-party apps access like ansible and GitHub), ansible(to build connection again you should have this on server2)
  - it will break the connection after this
  
about delete-user.yml
    - in this file you can delete users in server2 from server 1(you can delete multiple users: user.name1,user.name2,user.name3,,,, and many more)
  
about userSwitch.yml
    - after breaking the connection, if you want to do the tasks again you have to build the connection again.
    - this script will run on server2 by admin.... and it will be directly copied to the desired user's folder while running create_user.yml
  
  
about pub files
    - here public keys are stored(public keys of users you wanna create in server2)
    - nomenclature is fixed, you have to save the public keys in this format(user.name.pub)
