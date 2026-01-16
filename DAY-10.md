---SSH key geration Instead of PAT Real time scenario---NETWORK THINGS---

check credential manager github repo credentials using pat clear or erase those details

code push through ssh keys configuration
--------------------------------------------------------------------
SERVER ALIVE CONNECT CONFIGURATION

cd ~/.ssh/
vi config

# MDPrassadh account
Host github-mdprassadh
  HostName github.com
  User git
  IdentityFile C:/Users/Admin/.ssh/id_ed25519_mdprassadh
  IdentitiesOnly yes

# DurgaPrassadh account
Host github-durgaprassadh
  HostName github.com
  User git
  IdentityFile C:/Users/Admin/.ssh/id_ed25519_durgaprassadh
  IdentitiesOnly yes

Host *
ServerAliveInterval 30 # minutes
ServerAliveCountMax 2 # Terminal

---------------------------------------------------

1 cd ~/.ssh/ or ls -lrtha ~/.ssh/

2 if you have any keys delete it rm -rf id*

3 according to my knowledge 3 type keys are generated

      a] ssh-keygen and then enter enter   key created this is default also pubilc and private key are created...
      b] ssh-keygen -t rsa
      c] ssh-keygen -t rsa -f ~/.ssh/mdp_rsa_key
After generating key both pvt and public keys copy of public key completely to bring that file into configure in GITHUB UI

serrings-SSHand GPh keys -add new ssh key 

give name for that key 

key type -authentication key

key copy here what you copy in pubic key earlier

add shh key enough...

Before that remove PAT in credential manager in windows then 

gitbash ----

git remote -v 

copy of ssh link in remote repo ssh address instead of https

then 

git remote add AN [alias Name] shh-url-address

is it working or not check in known_hosts folder in cd ~/.ssh/

ssh -T git@github.com hit htis command it says everything 


