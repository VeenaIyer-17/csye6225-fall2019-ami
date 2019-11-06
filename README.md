# fa19-team-008-ami

## Team Information

| Name | NEU ID | Email Address |
| --- | --- | --- |
| Veena Vasudevan Iyer | 001447061 | iyer.v@husky.neu.edu |
| Amogh Doijode Harish| 001449026 | doijodeharish.a@husky.neu.edu |
| Ravi Kiran | 001491808 | lnu.ra@husky.neu.edu |
| | | |

## Technology Stack

The Amazon Machine Images being built here uses Packer. Packer is a Hashicorp 
technology used to automate building of Amazon Images.

### Build Instructions
    * Install Packer using - https://www.packer.io/
    * Generate ssh key and add in key pairs of instance resource in AWS
    * Follow the deploy instructions to view an ami being generated
    
### Deploy Instructions
    * Generate VPC, subnet using cloudformation/terraform scripts
    * Use the generated subnet id in ami-vars.json
    * Add region to ami-vars.json
    * Validate the json using the below command
      `packer validate -var 'aws_access_key= ' -var 'aws_secret_key=' centos-ami.json`
    * Once validated, build the template using the below command
       `packer build -var 'aws_access_key= ' -var 'aws_secret_key=' centos-ami.json` 
    * Use the generated ami-id and login into AWS
    * Create EC2 instance using AMI ID generated by the packer
    * Select the appropriate vpc id and subnet id when creating instance
    * Open the security group of the instance created and open port 80 & 8080 if your web application uses java
    * Generate a war file of your web application using
      `mvn clean install`
    * Scp the war file into your instance
       `scp source/war destination:~`
    * SSH into the instance created using
       `ssh -i sshkey.pem centos@IPv4 address`
    * Once you are in your instance, log into your database using command
       ` sudo mysql_secure_installation` and enter password for database
        `sudo mysql -u root -p`
    * In your database create database 'recipeSystem`
    * Run the war file in your instance using
       `java -jar warFile.war`
    * Use any REST tool like Postman to hit the enpoints of the application using the instance IP address
    

