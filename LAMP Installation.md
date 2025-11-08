# 1. Ubuntu Server Installation

In this guide, we **will** use **KVM** as **our** virtualization software and the **ubuntu-live-server-24.04** ISO image.

Hardware specs:

- 4GB of RAM# 1. Instalación de Ubuntu server

In this installation we gonna use **KVM** as us Virtualization Software and an iso of **ubuntu-live-server24.04**.

Hardware specs:

- 4GB of RAM
- 2 vcpus
- 30GB of storage
- VirtIO drivers for NIC and storage

![[Pasted image 20251027140511.png]]

**Hostname**: ubuserver-web
**User**: user
**Password**: qwer

Install the **OpenSSH-server** **during** the installation process **by selecting** the corresponding checkbox.

![[Pasted image 20251027141304.png]]

Reboot the virtual machine at the end of the installation.

# 2. Apache Installation

Now we have the **Operative System** installed, we will start download and configure the web **services**.

To install **Apache**, **run** the **following** command in the virtual machine's terminal:

~~~
sudo apt install apache2 -y
~~~

Run the following command to check the **apache2.service** status:

![[Pasted image 20251103131632.png]]

Connect to the web interface at `http://[Machine_IP]` to check if Apache is **working correctly**.

![[Pasted image 20251108185451.png]]

# 3. MySQL-Server Installation

To install **MySQL-server**, **run** the **following** command in the virtual machine's terminal:

~~~
sudo apt install mysql-server -y
~~~

Now, we have to enable the **mysql.service** with the **following** command:

![[Pasted image 20251103131837.png]]

# 4. PHP Installation

**Run** the **following** command to install **php** and **its** dependencies:

![[Pasted image 20251103132238.png]]

Create a test file in `/var/www/html` to check if **php** is working:

![[Pasted image 20251103132205.png]]

**After creating** the file, try to **access it** at `http://[Machine_IP]/file.php` in your browser.

![[Pasted image 20251108190222.png]]

# 5. Additional functionality

## MySQL Secure Configuration

We will **apply** a more secure configuration **to** MySQL. This can be done **quickly** by running the official `mysql_secure_installation` script.

**The following screenshots** illustrate the process:

![[Pasted image 20251108192850.png]]

![[Pasted image 20251108192915.png]]

## User creation

First, connect to the MySQL console **with root privileges** by **running** `mysql -u root -p`. You will be prompted for the root password you configured during the secure installation.

To create a new user named 'user1' (who can only connect from localhost), **run** the **following** command:

~~~
CREATE USER 'user1'@'localhost' IDENTIFIED BY 'qwerQWER1234|@#~';
~~~

To create another user named 'user2' who can **only connect** from the specific IP 192.168.122.1, **run** this command:

~~~
CREATE USER 'user2'@'192.168.122.1' IDENTIFIED BY 'qwerQWER1234|@#~';
~~~

**Here are the screenshots** of the process:

![[Pasted image 20251108193721.png]]