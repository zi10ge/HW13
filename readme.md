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