# Setup Instructions
On the school server, the client will be running on port 50xx and the server
will be running on port 30xx. The following instructions are written primarily
as if you were using command line.

## 1. Clone Repo
Clone the Powder/Pierre/Alpine repository
```
git clone <repo_url.git>
```
You can also clone a specific branch of the repository if it already exits
```
git clone --single-branch --branch <branch_name> <repo_url.git>
```


## 2. Modify .sample Files
The .env files and Footer.jsx are not tracked by git, so you should not commit
them. As a result, **you will need to do this every time you clone a new repo.**


### .env
An .env file is a hidden file that stores environment variables specific to
one system. It should not be committed. It is useful in maintaining different
values across systems as well as security (ex keeping an API key you paid for
publicly off GitHub.) The .env.sample file shows the variable names you will
need. The .env file on your local machine and the .env files on the server do
not need to be the same. For example you could set PORT=5000 on your local
machine but have it set to your port 50xx on the server.

0. To view the .env files on Linux use the -a flag to see hidden files
```
ls -a
```

1. In the client directory, copy the .env.sample file to .env or in any way copy
the .env.sample file to .env.
```
cp .env.sample .env
```

2. Use nano or vim to modify the environment variables in the .env file to what
they should be for you on your local machine or the school server. (You can also
use FileZilla to copy the .env files to the school server.) You should not
change the .env.sample file unless you are adding a new variable to the project.
    * clinet REACT\_APP\_HOST is the url to connect to the node database server.
    You will need to modify the 3000 port to what you used for the server and
    switch between localhost on your local machine and csci331.cs.montana.edu
    on the school server. There are comments next to which is which in the
    .env.sample file.
    * server DBPORT is the port the mysql is using. You will not need to change
    this on the server but may need to change it on your local machine.
3. Repeat 1 and 2 in the server directory


### Footer.jsx
In client/src/components/ there is a Footer.jsx.sample file. This file is a
template to make your own footer. You will need to create Footer.jsx for your
app to work.

1. In the client/src/components/ directory, copy the Footer.jsx.sample to
Footer.jsx
```
cp Footer.jsx.sample Footer.jsx
```
2. If you are working on the server, you need to update the Footer.jsx file. If
you are on your local machine, the file just needs to exist.

## 3. Install Packages
**You will need to do this every time you clone a new repo.**
In BOTH the client and server directories run the command
```
npm install
```


## 4. Use the Database
On your local machine, you will need an sql server running. You can do this
using Ammps. On the school server, you don't need to start anything.


### Initialize
You will need to initialize the tables in the database for things to run
properly. This will only need to be done once, per database. (Both on your local
machine and dbxx on the school server.) To do this, you can either create the
needed tables in the mysql shell or use the template given in the DB repo. Those
instructions follow. For more options/details see
[this reference](https://dev.mysql.com/doc/refman/8.0/en/mysql-batch-commands.html).

1. Clone the DB repo outside of your project repo.
```
git clone https://github.com/331F22/DB.git
```
2. Start a mysql shell and source the .sql files. On your local machine, you
will need to navigate Ammps to do so. If you are on the school server run
```
mysql -u userxx -p
use dbxx;
source DB/bridger.sql
show tables;
exit;
```

## 5. Run
You can run things using Forever or tmux on the school server to keep them
running. If you use tmux, you will be able to see the output which may be
helpful in troubleshooting errors.

### npm start
You can start both the client and server by using "npm start" in the command
line. However, if you are not using tmux, it will not stay running one you
close your connection to the server. Using npm start is a good way to see the
output and get feedback when first testing. This way you know if you got an
error and can fix it before using something like forever to start.


### Forever
If you are in the client or server directory you use ./ for the path portion.
```
forever start -c "npm start" <path_to_client_dir>
forever start -c "npm start" <path_to_server_dir>
```

### tmux
Here is a [tmux cheatsheet](https://gist.github.com/MohamedAlaa/2961058) with
some helpful commands and tricks. The bindkey on the school server is ctrl-A
not ctrl-B.

1. Start a new tmux window
```
tmux
```
**or** attach to an existing session (tmux attach if only one session running)
```
tmux ls
tmux attach -t <session_name>
```

2. cd into the client directory and run
```
npm start
```

3. Create a second way to run the server: detach from the current tmux session
(ctrl-A then d) and open a second tmux window **or** ctrl-A then " (shift-") to
split the tmux session. ctrl-A then o to switch between panes.

4. cd into the server directory and run
```
npm start
```
5. To exit the tmux window, you can close your terminal or detach from the
session (ctrl-A then d).
