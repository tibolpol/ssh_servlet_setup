# ssh_servlet_setup Installe une servlet ssh et son client
```
ssh_servlet_setup(1)                                  ssh_servlet_setup(1)

NOM
    ssh_servlet_setup -  Installe une servlet ssh et son client.

SYNOPSIS
    ssh_servlet_setup [-h|u] | | user@host:command

DESCRIPTION
    ssh_servlet_setup user@host:command
    installe le client ./command.cmd et la servlet ssh
    user@host:.ssh/servlet_command.

    - un client est créé localement sous le nom ./command.cmd,
    - une paire de clés est générée,
    - la clé privée est incluse dans le client,
    - la clé publique est incluse dans
      user@host:.ssh/authorized_keys,
    - le script est lu sur l'entrée standard et copié dans
      user@host:.ssh/servlet_command.

    Si la servlet doit lire l'entrée standard, il faudra ensuite éditer
    le client et supprimer l'option -n dans la commande ssh.

    Exemple :

    ssh_servlet_setup tlp@localhost:mytest <<< hostname

OPTIONS
    -h
        Aide

    -u
        Update ce script avec la branche master.

STATUT FINAL
    0 SUCCESS
        Succès.

    4 ERROR
        Une erreur est signalée.

VOIR AUSSI
    ssh(1) authorized_keys(5) ssh-keygen(1)

AUTEURS
    tlp(at)laposte(dot)net

ssh_servlet_setup(1)                                  ssh_servlet_setup(1)
```
