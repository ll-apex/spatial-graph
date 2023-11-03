# Connexion au calcul

## Présentation

Pour accéder à votre calcul d'hôte Python, vous avez besoin d'une paire de clés SSH. Oracle Cloud Infrastructure (OCI) Cloud Shell est un terminal basé sur un navigateur Web accessible à partir de la console Oracle Cloud permettant d'accéder à un shell Linux. Vous allez extraire une paire de clés SSH et vous connecter à l'hôte Python dans OCI Cloud Shell.

Temps de laboratoire estimé : 5 minutes

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire. [Laboratoire 1](videohub:1_0tvxm2q0)

### Objectifs

*   Récupération de l'adresse IP de calcul
*   Extraire une paire de clés SSH
*   Créer une connexion SSH au calcul

### Prérequis

*   Vous devez être connecté à la console OCI

## Tâche 1 : extraire l'adresse IP de l'instance de calcul

1.  Dans le menu principal, accédez à Compute > Instances.

![Ouvrir Cloud Shell](images/compute-01.png)

2.  Sur la page d'instructions de l'atelier, cliquez sur **Visualiser les informations de connexion** en haut à gauche et copiez le nom du compartiment.

![Ouvrir Cloud Shell](images/compartment.png)

1.  Dans la console OCI, collez le nom de votre compartiment et sélectionnez-le dans la liste déroulante.

![Ouvrir Cloud Shell](images/compute-02.png)

4.  Notez l'adresse IP publique de votre instance de calcul. Vous l'utiliserez plus tard dans cet exercice et dans d'autres exercices.

![Ouvrir Cloud Shell](images/compute-03.png)

## Tâche 2 : extraire les clés SSH

1.  Ouvrez cloud shell.
    
    ![Ouvrir Cloud Shell](images/compute-04.png)
    
2.  Si vous êtes invité à exécuter le tutoriel, tapez N et entrez.
    
    ![Ouvrir Cloud Shell](images/compute-05.png)
    
3.  Sur la ligne de commande, exécutez chacun des éléments suivants pour créer votre dossier SSH et y accéder.
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh \`\`

![Créer des clés](images/compute-06.png)

1.  Sur la ligne de commande, exécutez la commande suivante pour extraire et répertorier un fichier ZIP contenant des clés SSH.
    
        <copy>
        wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/hfpJ4-8XrB5tWBDUWvgnCmGch_1WHhihBrRpHNIzj6JSq5O5hbwp2wsqRPYbg8Gm/n/c4u04/b/livelabsfiles/o/labfiles/ocw23-keys.zip
        </copy>
        
    
        <copy>
        ls
        </copy>
        
    
    ![Créer des clés](images/compute-07.png)
    
2.  Sur la ligne de commande, exécutez la commande suivante pour décompresser et répertorier le contenu du fichier ZIP.
    
        <copy>
        unzip ocw23-keys
        </copy>
        
    
        <copy>
        ls
        </copy>
        

![Créer des clés](images/compute-08.png)

## Tâche 3 : connexion à l'instance de calcul

2.  Sur la ligne de commande, exécutez la commande suivante pour vous connecter à votre instance de calcul Python, où l'adresse IP est l'adresse IP de calcul de la tâche 1.
    
        <copy>
         ssh -i ~/.ssh/ocw23-rsa opc@[IP address]
        </copy>
        
    
    Si vous êtes invité à ajouter des hôtes à la liste des hôtes connus, répondez **yes**.
    
    ![Créer des clés](images/compute-09.png)
    
3.  Cliquez sur l'icône Réduire pour réduire Cloud Shell.
    
    ![Réduire Cloud Shell](images/compute-10.png)
    
4.  Observez le bouton Restore pour rouvrir Cloud Shell. Vous rouvrirez Cloud Shell dans un laboratoire ultérieur.
    
    ![Restaurer Cloud Shell](images/compute-11.png)
    

Vous pouvez maintenant **passer à l'exercice suivant**.

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Dernière mise à jour par/date** - David Lapp, août 2023