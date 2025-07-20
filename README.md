# Box Office Analysis: Maximizing Movie Revenue
## Aperçu
Dans ce projet, nous analysons les données de recettes de films (bom.movie_gross.csv.gz) pour comprendre quels facteurs influencent le succès financier d'un film.

L'objectif est de formuler des recommandations commerciales claires pour un studio de cinéma en se basant uniquement sur les revenus du box office.

## Compréhension des Affaires
Le studio veut maximiser ses revenus au box office.  
Voici les questions clés :

- Quels types de films rapportent le plus ?
- Quels studios dominent le marché ?
- Y a-t-il une saisonnalité dans les sorties les plus rentables ?
- Le marché domestique (US) ou international est-il plus stratégique ?

Livrable final :  
3 recommandations basées sur les résultats.

## Compréhension des Données
Le fichier utilisé : bom.movie_gross.csv.gz

### Principales colonnes :

| Colonne | Description |
|---|---|
| title | Titre du film |
| studio | Studio producteur |
| domestic_gross | Revenus aux États-Unis |
| worldwide_gross | Revenus mondiaux |
| year | Année de sortie |

---
## Préparation de Données
- Chargement des données : pd.read_csv
- Nettoyage :
  - Supprimer les $ et , dans les colonnes domestic_gross et worldwide_gross
  - Convertir en format numérique
  - Vérifier les valeurs manquantes
- Création de nouvelles colonnes si nécessaire : 
  - International_gross = Worldwide_gross - Domestic_gross


## Analyses et Recommendations

### Analyses possibles

| Analyse | Outil Statistique | Cas d'utilisation |
|----------|-------------------|-------------------|
| Top studios par revenus | Statistiques descriptives (moyenne, médiane) | Identifier les studios les plus rentables |
| Distribution des revenus | Histogrammes + PDF (Probability Density Function) | Visualiser la répartition des revenus |
| Comparaison des revenus domestiques vs internationaux | Diagrammes circulaires + comparaison des moyennes | Vérifier l’importance des marchés étrangers |
| Évolution temporelle des revenus | Courbes temporelles (Line plot) | Identifier les années les plus lucratives |
| ANOVA (Analyse de Variance) | scipy.stats.f_oneway() | Comparer les revenus moyens entre studios ou années |
| Régression linéaire | statsmodels ou sklearn.linear_model | Prédire les revenus en fonction des années |
| Puissance statistique | statsmodels.stats.power | Vérifier si l’échantillon est assez grand pour détecter une différence |
| PMF (Probability Mass Function) | Distribution discrète (ex : nombre de films par studio) | Voir la probabilité qu’un film aléatoire appartienne à un studio donné |

---
### Visualisations recommandées

- Barplot : Revenus moyens par studio
- Histogramme avec PDF : Distribution des revenus total_gross
- Boxplot : Comparaison des revenus par studio
- Courbe temporelle : Évolution des revenus au fil des années
- Nuage de points + régression linéaire : Relation entre l’année et les revenus

---
## Visualisation : Top 10 des Studios par Revenu Moyen

Après avoir calculé les revenus moyens par studio, on utilise un diagramme en barres horizontales pour visualiser les 10 studios les plus rentables.

python
sns.barplot(x=studio_avg.values, y=studio_avg.index, color="skyblue")
plt.title("Top 10 Studios par Revenu Moyen")
plt.xlabel("Revenu Moyen ($)")
plt.ylabel("Studio")
plt.show()

<div style="text-align: center; margin-top: 20px;">
    <img src="Images/WhatsApp Image 2025-07-20 at 15.05.26_b48a2c97" width="800" alt="Capture d'écran IMDB">
    <p style="font-style: italic; color: #7f8c8d; margin-top: 10px;">
        Schéma de la base de données IMDB utilisée pour l'analyse.
    </p>
</div>


## Visualisation : Distribution des Revenus Totaux des Films

Cette partie du code permet de visualiser la *distribution des recettes totales (total_gross)* des films à l'aide d'un histogramme avec courbe de densité (PDF).

python
# Histogramme avec courbe de densité (PDF)
sns.histplot(df_clean['total_gross'], kde=True, color="skyblue", bins=30)
plt.title("Distribution des Revenus (PDF)")
plt.xlabel("Revenu Total ($)")
plt.ylabel("Nombre de films / Densité")
plt.show()

<div style="text-align: center; margin-top: 20px;">
    <img src="Images/Screenshot 2025-07-20 160423.png
" width="800" alt="Capture d'écran IMDB">
    <p style="font-style: italic; color: #7f8c8d; margin-top: 10px;">
        Schéma de la base de données IMDB utilisée pour l'analyse.
    </p>
</div>

## Visualisation : Régression Linéaire entre l'Année et les Revenus Totaux

Cette visualisation permet d’observer la *relation entre l’année de sortie d’un film (year) et ses recettes totales (total_gross)* grâce à une régression linéaire.

python
sns.lmplot(data=df_clean, x='year', y='total_gross', height=6, aspect=1.5)
plt.title("Régression Linéaire : Année vs Revenu Total")
plt.show()

<div style="text-align: center; margin-top: 20px;">
    <img src="Images/Screenshot 2025-07-20 160446.png
" width="800" alt="Capture d'écran IMDB">
    <p style="font-style: italic; color: #7f8c8d; margin-top: 10px;">
        Schéma de la base de données IMDB utilisée pour l'analyse.
    </p>
</div>


### Recommandations commerciales

1. Se concentrer sur les studios les plus rentables : Les données indiquent qu'une poignée de studios dominent le marché.
2. Adapter la stratégie internationale : Les revenus étrangers représentent une part significative du box-office pour certains films.
3. Optimiser le calendrier des sorties : Identifier les périodes les plus lucratives pour maximiser les profits.
