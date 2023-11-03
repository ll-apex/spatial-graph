# Nettoyage

## Présentation

Dans cet exercice, vous allez annuler le déploiement de l'instance Spatial Studio créée à l'aide de Cloud Marketplace. La purge permanente de toutes les ressources créées dans le cadre du déploiement de Spatial Studio à partir de Cloud Marketplace.

Temps de laboratoire estimé : 5 minutes

Regardez la vidéo ci-dessous pour une présentation rapide du laboratoire.

[Option de nettoyage 2 : Terminer Spatial Studio et ADB](videohub:1_1jnminp7)

### Objectifs

Dans cet exercice, vous allez :

*   Annulez le déploiement de Spatial Studio et des ressources associées créées à partir d'Oracle Cloud Marketplace.

### Prérequis

*   Spatial Studio déployé à partir de Cloud Marketplace

## Tâche 1 : Purger les ressources déployées

Accédez à la pile utilisée pour créer votre instance Spatial Studio.

1.  Accédez à **Services de développeur > Piles**.
    
    ![Accéder aux piles dans la console OCI](images/teardown-01.png)
    
2.  Dans le menu d'actions de la pile, sélectionnez **Visualiser les détails de la pile**.
    
    ![Afficher les détails de pile](images/teardown-02.png)
    
3.  Cliquez sur **Détruire**. Cela purgera les ressources créées par le déploiement de Spatial Studio Marketplace.
    
    ![Détruire la pile](images/teardown-03.png)
    
4.  Confirmez l'opération en cliquant à nouveau sur **Destroy**.
    
    ![Confirmer la destruction de la pile](images/teardown-04.png)
    
5.  Attendez environ 3 à 4 minutes que le processus se termine. Observez le statut dans la section Jobs. Lorsque le statut est **Succès**, le chômage est terminé et toutes les ressources provisionnées par le déploiement de Spatial Studio Marketplace sont purgées.
    
    ![Vérifier le travail de destruction](images/teardown-05.png)
    

## Tâche 2 : supprimer la pile (facultatif)

La pile est l'ensemble d'instructions pour le déploiement. Il capture les paramètres que vous avez sélectionnés lors de l'exécution de l'assistant Cloud Marketplace. Maintenant que vous avez purgé les ressources créées lorsque vous avez exécuté la pile pour créer votre instance Spatial Studio, vous pouvez maintenant supprimer la pile elle-même. Après avoir supprimé la pile, afin de déployer à nouveau Spatial Studio, vous devrez recommencer avec Cloud Marketplace. Vous pouvez également conserver la pile et la réexécuter telle quelle, ou la modifier pour modifier des paramètres tels que l'ajout d'une clé SSH afin de créer une instance à plus long terme.

1.  Dans le menu **Actions supplémentaires** de la pile, sélectionnez **Supprimer la pile**.
    
    ![Sélectionner la pile de suppression](images/teardown-06.png)
    
2.  Lorsque vous êtes invité à confirmer, cliquez sur **Supprimer**.
    
    ![Confirmer la suppression de la pile](images/teardown-07.png)
    
3.  Tous les artefacts créés par l'assistant Cloud Marketplace, à la fois les ressources et la pile, ont disparu.
    

## En savoir plus

*   [Page produit Oracle Spatial](https://www.oracle.com/database/spatial)
*   [Lancez-vous avec Spatial Studio](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)
*   [Documentation de Spatial Studio](https://docs.oracle.com/en/database/oracle/spatial-studio)

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Contributeurs** - Jesus Vizcarra
*   **Dernière mise à jour par/date** - David Lapp, août 2023