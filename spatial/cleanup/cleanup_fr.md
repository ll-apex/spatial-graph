# Réinitialiser ADB à l'état pré-atelier

## Présentation

Cet exercice consiste à supprimer tout ce qui a été créé dans les exercices précédents afin de pouvoir recommencer si nécessaire.

Durée estimée : 2 minutes

### À propos

Dans cet exercice, tous les artefacts créés précédemment sont supprimés.

### Objectifs

*   Réinitialisez ADB à l'état pré-atelier.

### Prérequis

*   Achèvement de l'atelier 3 ; Préparer les données spatiales

## Tâche 1 : supprimer tout ce qui a été créé dans cet atelier

1.  Pour enlever des tables et des index créés dans cet atelier, exécutez la commande suivante à l'aide du bouton Run Script dans SQL Worksheet.
    
    ![Texte de remplacement de l'image](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  Pour supprimer les métadonnées spatiales insérées dans cet atelier, exécutez la commande suivante à l'aide du bouton Run Script dans SQL Worksheet.
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  Pour supprimer la fonction créée dans cet atelier, exécutez la commande suivante.
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## Accusés de réception

*   **Auteur** - David Lapp, Database Product Management, Oracle
*   **Dernière mise à jour par/date** - David Lapp, septembre 2022