# Kubernetes-Ansible-wordpress

I've created a role named ec2 which will launch three instances for the K8s Multinode Cluster (1 master node, 2 slave node).

## Dynamic inventory 
After the instances are launched then the work of the dynamic inventory comes in play i.e. ec2.ini and ec2.py files
these two files need to be placed in a single folder and then the path of these file need to be given in the ansible.cfg file

For the dynamic inventory to work perfectly we need to provide the AWS ACCESS KEY and AWS SECRET KEY in the ec2.ini file and also export the env varaibles so that the boto can use it
ENV variables:
export AWS_ACCESS_KEY_ID = "ADMNDYJXDJGCGHJSRET"
export AWS_SECRET_ACCESS_KEY= "isehbzdlifughaoldjno;hPHGOGSTGGHBsdfghdn"

## Ansible Playbook
Now when the Ansible playbook runs the instances are launched and the refresh_inventory task refreshes the dynamic inventory.

Now as the ansible playbook gets the IP from the tag_Name of the instances and then Kubernetes Multi-Node Cluster set up starts

## Wordpres and Database
After the complete Kubernetes Multi-Node Cluster is ready and the slave nodes join with the Master Node, the pods for wordpress and mysql database are launched from their repective images.
The MySQL pod needs to be launched along with the decired ENV variables as described in the main playbook,
### Eg: kubectl run mydb1 --image=mysql:5.7 --env=MYSQL_ROOT_PASSWORD=redhat  --env=MYSQL_DATABASE=imran_db  --env=MYSQL_USER=imran --env=MYSQL_PASSWORD=redhat"

After the pod launches, the port 80 of the wordpress pod is exposed via service kind of the Kubernetes and of type NodePort.

Then using the public IP of any of the Slave Node we can now connect to the wordpress application in the desired port number.
In the Wordpress Web UI we now need to fill the fields with the details of the database
And when the Run installation dialog appears implies the connectin to the database was successful
Hence Task completed...!!!
