## Présentation
Une servlet SSH est l'association d'une clé et d'un script déployé sur un compte utilisateur d'un serveur SSH.
Le mapping est accompli par le paramètre `authorized_keys command` sur le compte utilisateur du serveur associé à la clé publique.
Le client est déployé sous forme de script, exécutable par `bash` ou par `DOS cmd`.
Il contient la clé privée non chiffrée, et utilise l'implémentation `OpenSSH` ou `plink`.

```
[private_key] >> ssh|plink >> user@host:authorized_keys[public_key] >> command $args
```

## Scénario
Le scénario caractéristique est la distribution d'applications shell simples sur des serveurs SSH sans augmenter la surface d'attaque.
Ce script `ssh_servlet_setup` permet de créer facilement et de déployer en une seule commande la paire de clés unique, le client et la servlet.

## Sécurité
Le cas d'usage privilégié est la distribution de processus automatisés ne nécessitant pas de passphrase fournie par un opérateur, c'est pourquoi la clé privée peut être non chiffrée.
Le client vérifie a minima que ses permissions sont restreintes à l'utilisateur propriétaire, ce qui est acceptable dans un environnement Unix.
La surface d'attaque du serveur est réduite à la clé ne désignant que la commande sctricement nécessaire.

### TODO
Ajouter un parsing des arguments pour intercepter l'injection de shell.

## ssh_servlet_setup Installe une servlet ssh et son client
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
    le script client et supprimer l'option -n dans la commande ssh.

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
