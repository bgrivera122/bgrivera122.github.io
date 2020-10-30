---
hero_image: https://northslopechillers.com/wp-content/uploads/2019/07/Cool-Server-Room.jpg
---
# Ansible Notes
## It's Alive!

It turned out that a simple "@" symbol caused my _config.yml to not get pushed through. Github
wouldn't even tell me what was wrong! "@" is reserved, and fields within _config.yml cannot be
led with an "@" as it is reserved.

I was able to find out through https://yaml.org/spec/1.2/spec.html#id2774157 in section 5.10.

I'll be implementing a theme by the next due date.

<!--end_excerpt-->
## Docker Container

I was able to use my local machine's directory to place files within the Docker container using this
command:

`docker run  -it -v $(pwd):/home/ansible -p 8080:8080 ubuntu:18.04 /bin/bash`

With this, I was able to import the 000-default.conf, apache2.conf, and dir.conf files using Windows'
FIle Explorer and have the Copy tasks within Ansible recognize them from a relative source. This made
copying easy.

## Lack of Stdout

Because Ansible does not display stdout when performing tasks, I was unable to confirm if `noninteractive`was functioning in the manner I wanted to for the timezone check in one of the php packages. By assigning a variable `out` with `register` to echo out the result of `DEBIAN_FRONTEND=$DEBIAN_FRONTEND`, and displaying the result using `debug`, I would see if `$DEBIAN_FRONTEND` would come out as a blank or not. This was dummied out afterwards. I was going to use `echo` for the Install Composer task because I thought it had crashed when I first attempted to install Composer. However, it completed just fine, it was just quite slow.

## Syntax and Symbolic links

The Ansible syntax is really sensetive with spaces and it's structure, but when looking at an Ansible
playbook, it at least looks nice. The "Install required packages" task turned

`RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y php libapache2-mod-php php-mysql php7.2-cli php7.2-curl php7.2-gd php7.2-mbstring php7.2-mysql php7.2-xml php-xml`

Into a pleasant shopping list.

I was surprised at how Ansible was able to detect symbolic links with `state: link`. While Apache can be configured to put affinity in any directory that is desired, the "Create a symbolic link" task exemplifies using a symbolic link to have Affinity use Apache's default directory of /html/public. In this Ansible file, this symbolic link enables Affinity to "play nice" with apache as-is without setting up aforementioned configuration.

## Root vs. www-data

When I left the owner and group as "root," it allowed the .conf files to be used by whoever wants to use them, which is good for me because it was easy even though it's bad for everyone else because it's a potential security risk. But, Affinity tasks had to be handled differently.

www-data is apache's defaulted "special user" that carries out actions on behalf of the people that are using the web application. Any PHP scripts run as www-data every time a user requests a wepage or an HTTP request, etc. If these fields were set to "root" like in the file copy tasks, it would fail and get an error.

## Affinity Dependencies

Installing Affinity dependies relies on Composer being installed. Composer is a tool to download
dependencies of PHP applications, like libraries. The dependenceies land in the `/vendor` directory,
so `when: not deps_stat.stat.exists` sees if the `/vendor` directory exists. This way, dependencies are installed only when needed.

## Links I Found Useful

https://docs.ansible.com/ansible/latest/reference_appendices/playbooks_keywords.html

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debug_module.html

https://stackoverflow.com/questions/36059804/ansible-store-commands-stdout-in-new-variable

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/git_module.html

https://docs.ansible.com/ansible/2.8/modules/file_module.html

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html