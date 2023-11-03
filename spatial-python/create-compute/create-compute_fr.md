# Créer une instance de calcul à partir d'une image personnalisée

## Présentation

Une image de calcul a été créée au préalable avec Python configuré. Dans cet exercice, vous allez créer une instance de calcul à partir de cette image.

Durée estimée du laboratoire : xx minutes

### Objectifs

*   Créez une instance de calcul à partir d'une image personnalisée avec Python préconfiguré.

### Prérequis

*   Fin de l'exercice précédent (création de clés SSH dans Cloud Shell)

## Tâche 1 : créer une instance de calcul

1.  Accédez à Compute > Instances. ![Instances de calcul](images/compute-01.png)
    
2.  Cliquez sur **Créer une instance**. ![Créer des instances](images/compute-02.png)
    
3.  Entrez un nom tel que **my-compute**, ou vous pouvez laisser la valeur par défaut. Sélectionnez un compartiment si vous en avez créé un ou conservez la valeur par défaut (racine). Ensuite, dans la section de placement, cliquez sur **Modifier**. ![Créer des instances](images/compute-03.png)
    
4.  Si vous prévoyez d'utiliser des ressources Toujours gratuit, sélectionnez le domaine de disponibilité qui propose **VM.Standard.E2.1. Forme micro**. ![Créer des instances](images/compute-04.png)
    
5.  Faites défiler la page jusqu'à la section **Image et forme**, puis cliquez sur **Modifier**. ![Créer des instances](images/compute-05.png)
    
6.  Cliquez sur **Modifier l'image**. ![Créer des instances](images/compute-06.png)
    
7.  Sélectionnez **Mes images** et **OCID d'image**. ![Créer des instances](images/compute-07.png)
    
8.  Copiez l'OCID ci-dessous, collez-le dans le champ OCID d'image et cliquez sur **Sélectionner une image**.
    
        <copy>
         ocid1.image.oc1..aaaaaaaan727cclmzfl2evanaacnganaeobmv6hvakjzqdsk4gncmcklcxha
        </copy>
        
    
    ![Créer des instances](images/compute-08.png)
    
9.  Faites défiler la page jusqu'à la section Networking et cliquez sur **Edit**. ![Créer des instances](images/compute-09.png)
    
10.  Si vous avez un réseau existant, vous pouvez l'utiliser. Sinon, sélectionnez **Créer un réseau cloud virtuel**. Pour les noms, saisissez **my-vcn** et **my-subnet**, ou vous pouvez laisser les valeurs par défaut. Sélectionnez un compartiment si vous en avez créé un ou conservez la valeur par défaut (racine). Sous Adresse IPv4 publique, vérifiez que l'option **Affecter une adresse IPv4 publique** est sélectionnée. ![Créer des instances](images/compute-10.png)
    
11.  Faites défiler la page jusqu'à la **section Ajouter des clés SSH**, sélectionnez **Coller la clé publique**, puis cliquez sur **Restaurer** pour développer Cloud Shell. ![Créer des instances](images/compute-11.png)
    
12.  La dernière commande exécutée dans Cloud Shell a imprimé votre clé publique. Copiez la clé publique à partir de Cloud Shell et collez-la dans le champ Clés SSH de la boîte de dialogue Créer une instance de calcul. Réduisez ensuite Cloud Shell. ![Créer des instances](images/compute-12.png)
    
13.  Cliquez sur **Créer**. ![Créer des instances](images/compute-13.png)
    
14.  Une fois le provisionnement terminé, copiez l'adresse IP publique de l'instance de calcul et restaurez Cloud Shell. ![Créer des instances](images/compute-14.png)
    
15.  Entrez la commande suivante dans Cloud Shell pour vous connecter à votre instance de calcul, où vous pouvez coller "\[adresse IP\]" qui a été copiée à l'étape précédente.
    
        <copy>
         ssh -i ~/.ssh/my-ssh-key opc@[IP address]
        </copy>
        
    
    Lorsque vous êtes invité à ajouter des hôtes à la liste des hôtes connus, répondez **yes**. ![Créer des instances](images/compute-15.png)
    

Votre instance de calcul est créée et vous avez vérifié l'accès SSH.

## Tâche 2 : port réseau ouvert 8001

1.  Dans le panneau de navigation principal, sélectionnez **Networking**. Sélectionnez ensuite **Réseaux cloud virtuels**. ![Créer des instances](images/compute-16.png)
    
2.  Cliquez sur le VCN créé dans la tâche précédente. ![Créer des instances](images/compute-17.png)
    
3.  Faites défiler la page vers le bas et cliquez sur **Listes de sécurité** à gauche, puis cliquez sur **Liste de sécurité par défaut pour my-vcn**. ![Créer des instances](images/compute-18.png)
    
4.  Cliquez sur **Add Ingress Rules**. ![Créer des instances](images/compute-19.png)
    
5.  Pour le CIDR source, entrez **0.0.0.0/0**. Pour Destination Port Range, entrez **8001**. Cliquez ensuite sur **Ajouter une règle entrante**. ![Créer des instances](images/compute-20.png)
    
6.  Faites défiler l'affichage vers le bas et observez la nouvelle règle entrante autorisant l'accès entrant au port 8001. ![Créer des instances](images/compute-21.png)
    

Vous pouvez maintenant **passer à l'exercice suivant**.

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, Database Product Management, juin 2023