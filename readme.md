apt install ansible
apt install python-pip
pip install boto
pip install boto3

apt install awscli
aws configure

add to etc/ansible/hosts ->  
    [lhost]
    localhost

add ./ansible.cfg
    [defaults]
    host_key_checking = False


Для более долгоживущих экземпляров EC2 имеет смысл принять ключ хоста с задачей, выполняемой только один раз при первоначальном создании экземпляра:
    - name: Write the new ec2 instance host key to known hosts
    connection: local
    shell: "ssh-keyscan -H {{ inventory_hostname }} >> ~/.ssh/known_hosts"

также будет работать с версиями Ansible старше 2.5):
- hosts: localhost
  connection: local
  gather_facts: false
  tasks:
    - add_host:
        name: my_host
        ansible_host: myhost.example.com
        host_key_checking: false

- hosts: my_host
  tasks:
    - ping: