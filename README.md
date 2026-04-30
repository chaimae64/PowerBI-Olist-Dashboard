# E-commerce Sales & Customer Analytics
### Power BI Dashboard — Olist Dataset

## Objectif
Analyser plus de 100 000 commandes réelles d'un e-commerce 
brésilien afin d'identifier des opportunités d'optimisation 
des ventes, de la logistique et de la satisfaction client.

## Dataset
Source : Kaggle — Brazilian E-Commerce Public Dataset by Olist
- 100 000+ commandes réelles
- 7 tables relationnelles (clients, commandes, produits, 
  paiements, avis, vendeurs, catégories)

## Architecture des données
Schéma simplifié des relations principales :

olist_customers
      |
      | customer_id
      |
olist_orders ──── olist_order_items ──── olist_products
      |                                        |
      | order_id                               | product_category_name
      |                                        |
olist_order_reviews              product_category_name_translation
olist_order_payments

(voir screenshots/modele.png pour le schéma complet Power BI)

## Approche technique
- Modélisation relationnelle (schéma en étoile, 6 relations)
- Nettoyage et transformation avec Power Query
- Mesures DAX personnalisées pour les KPIs business
- Dashboard interactif structuré en 5 pages orienté 
  prise de décision

## Mesures DAX principales
-- Chiffre d'affaires total
CA Total = SUM(olist_order_items_dataset[price])

-- Nombre de commandes
Nb Commandes = DISTINCTCOUNT(olist_orders_dataset[order_id])

-- Panier moyen
Panier Moyen = DIVIDE([CA Total], [Nb Commandes])

-- Délai moyen de livraison (en jours)
Délai Moyen = AVERAGEX(olist_orders_dataset,
    DATEDIFF(olist_orders_dataset[order_purchase_timestamp],
             olist_orders_dataset[order_delivered_customer_date],
             DAY))

-- % commandes en retard
% Retard = DIVIDE(
    COUNTROWS(FILTER(olist_orders_dataset,
        olist_orders_dataset[order_delivered_customer_date] >
        olist_orders_dataset[order_estimated_delivery_date])),
    [Nb Commandes])

-- Note moyenne client
Note Moyenne = AVERAGE(olist_order_reviews_dataset[review_score])

## Dashboard — 5 pages
- Overview    : KPIs globaux et évolution des ventes
- Clients     : segmentation et analyse géographique
- Produits    : performance et contribution au CA
- Livraison   : analyse des délais et retards
- Insights    : synthèse et recommandations

## KPIs analysés
- Chiffre d'affaires total : 1,36 Md BRL
- Nombre de commandes     : 96 000+
- Délai moyen livraison   : ~12 jours
- % commandes en retard   : 8%
- Note moyenne client     : 4,09 / 5

## Insights clés
- health_beauty génère 11% du CA, catégorie la plus dominante
  devant watches_gifts (9%) et bed_bath_table (8%)
- 8% des commandes arrivent en retard → impact direct 
  sur la fidélisation client
- États RR, AP, AM : délais moyens ~30 jours 
  → problème logistique concentré dans le nord du Brésil
- Note moyenne 4,09/5 malgré les inefficacités 
  → satisfaction globale solide mais fragile
- Croissance du CA x10 entre 2016 et 2018 
  → forte phase d'expansion de la plateforme

## Recommandations
- Optimiser la logistique dans les régions à forte latence
  (RR, AP, AM en priorité)
- Prioriser health_beauty et watches_gifts 
  dans les campagnes marketing
- Mettre en place des alertes automatiques sur les retards
- Concentrer les efforts commerciaux sur le sud-est 
  (São Paulo, Rio de Janeiro)

## Impact
Ce dashboard permet d'identifier rapidement :
- Les zones logistiques à améliorer en priorité
- Les catégories produits à fort potentiel de croissance
- Les facteurs influençant la satisfaction client
- Les tendances de ventes pour anticiper la demande

## Compétences démontrées
- Data Visualization (Power BI)
- DAX & modélisation de données relationnelles
- Data Cleaning (Power Query)
- Data Analysis & Business Insights
- Data Storytelling

## Screenshots
![Modele](screenshots/modele.png)
![Overview](screenshots/overview.png)
![Clients](screenshots/clients.png)
![Produits](screenshots/produits.png)
![Livraison](screenshots/livraison.png)
![Insights](screenshots/insights.png)