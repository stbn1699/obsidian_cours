### Jeu de données: 

Téléchargez ou générez un jeu de données de stations météorologiques, qui incluent la date, la température, la pression atmosphérique, etc.
___
### Préparation des données: 

__a.__ Importez les données de stations météorologiques dans MongoDB en utilisant la commande mongoimport. 

__b.__ Assurez-vous que les données sont bien structurées et propres pour une utilisation ultérieure.
___
### Indexation avec MongoDB: 

__a.__ Créez un index sur le champ de la date pour améliorer les performances de la recherche. Utilisez la méthode createIndex (). 

__b.__ Vérifiez que l'index a été créé en utilisant la méthode listIndexes ().
___
### Requêtes MongoDB: 

__a.__ Recherchez les stations météorologiques qui ont enregistré une température supérieure à 25°C pendant les mois d'été (juin à août). Utilisez la méthode find () et les opérateurs de comparaison pour trouver les documents qui correspondent à vos critères. 

__b.__ Triez les stations météorologiques par pression atmosphérique, du plus élevé au plus bas. Utilisez la méthode sort () pour trier les résultats.
___
### Framework d'agrégation: 

__a.__ Calculez la température moyenne par station météorologique pour chaque mois de l'année. Utilisez le framework d'agrégation de MongoDB pour effectuer des calculs sur les données et grouper les données par mois. 

__b.__ Trouvez la station météorologique qui a enregistré la plus haute température en été. Utilisez le framework d'agrégation de MongoDB pour effectuer des calculs sur les données et trouver la valeur maximale.
___
### Export de la base de données: 

__a.__ Exportez les résultats des requêtes dans un fichier CSV pour un usage ultérieur. Utilisez la commande mongoexport pour exporter des données de MongoDB.