# Setup Instructions
* Diff between 30xx and 50xx

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

1. In the client directory, copy the .env.sample file to .env
```
cp .env.sample .env
```

2. Use nano or vim to modify the environment variables in the .env file to what
they should be for you on your local machine or the school server. (You can also
use FileZilla to copy the .env files to the school server.) You should not
change the .env.sample file unless you are adding a new variable to the project.
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

## 4. Run
You can run things using Forever or tmux. If you use tmux, you will be able to
see the output which may be helpful in troubleshooting errors.

### Forever
If you are in the client or server directory you use ./ for the path portion.
```
forever start -c "npm start" <path_to_client_dir>
forever start -c "npm start" <path_to_server_dir>
```

### tmux
1. Start a new tmux window
```
tmux
```
or attach to an existing session (tmux attach if only one session running)
```
tmux ls
tmux attach -t <session_name>
```
