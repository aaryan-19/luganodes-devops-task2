# luganodes-devops-task2

## Node Exporter via Ansible with Monitoring


### Steps For Running the project

Steps for Running the project
1.	Clone the repository.
2.	Modify the **IP address** in **inventory file** accordingly for use case
3.	Run the command - `ansible-playbook -i inventory playbook.yml`

The command ansible-playbook -i inventory playbook.yml will execute an Ansible playbook using the specified inventory file (inventory) and playbook file (playbook.yml). 

Note – If you want multiple hosts then below is the example of inventory file for multiple hosts – 

    `
    [monitorserver]
    db_server   ansible_host=<YOUR-DB-SERVER-IP>   ansible_user=ec2-user  ansible_ssh_private_key_file=~/<YOUR-PEM-FILE>
    [nodeservers]
    server1  ansible_host=<YOUR-WEB-SERVER-IP>  ansible_user=ec2-user  ansible_ssh_private_key_file=~/<YOUR-PEM-FILE>
    server2  ansible_host=<YOUR-WEB-SERVER-IP>  ansible_user=ec2-user  ansible_ssh_private_key_file=~/<YOUR-PEM-FILE>
    `


Here you can add path to your public key in <YOUR-PEM-FILE> and ansible will use specified SSH key for authentication

Steps for Grafana – 
1.	Go to url – **localhost:3000**
2.	Add new Connection prometheus and enter url as – localhost:9090
3.	Enter default username and password = “admin” for both.
4.	Go to dashboard and click on new -> import and enter the dashboard id mentioned in **https://grafana.com/grafana/dashboards/1860-node-exporter-full/**
5.	This will create a Grafana dashboard which consists of visualizations , panels , widgets that display metrics and data collected by Prometheus from target hosts
Troubleshooting steps 
1.	Check for IP in inventory file
2.	Go to prometheus.conf.j2 in roles/prometheus/templates and add a list in target for job_name: ‘node_exporter’ containing your host ip and port number 9090 for prometheus

`Note – if you have multiple target host then add the ip and port to the target list only.`
