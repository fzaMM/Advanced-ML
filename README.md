# Advanced-ML
H&amp;M recommendations

Objectif & Contexte: 
- Plateforme : Kaggle Competition.
- Domaine : Retail / Fast Fashion (H&M).
- But : Predict the next 12 articles each customer is likely to purchase based on historical shopping behavior.

Dataset & Scale
- Transactions : (~2 years, > 30M lines).
- Customer Metadata : Age, Newsletter engagement, Postal code...etc
- Product Metadata : Type (Robe/Pantalon), color, Description, Image (ID)Évaluation..etc

Why is the challenge useful ? 
- Recommendation Systems: Moving beyond traditional classification to personalized ranking problems
- Sequential Modeling: Understanding how customer preferences evolve over time
- Real-world Constraints: Balancing model sophistication with computational limitations
- Cold-start Problems: Handling new customers and seasonal products with limited interaction history
  
Problems and challenges encountered: 
- Data Volume & Computational Constraints
    - RAM limitations: Unable to load the full 30M+ transaction dataset into memory
    - GPU constraints: Limited access on Collab
    - Image metadata: Could load the images data, it was unused during the challenge.


The best technical solution :

We achieved best results by combining ALS and lightgbm, which offered:

- Efficiency: ALS handles the heavy lifting of candidate retrieval; LightGBM works on small, focused sets
- Complementarity:
  ALS captures collaborative patterns (implicit similarities)
  LightGBM adds explicit personalization (customer/product attributes)
- Metadata integration: Overcomes ALS's inability to use product/customer features
- Scalability: Can't run LightGBM on all 100K articles per customer, but can on top 100-500 candidates

Why SASRec Underperformed?
We initially tried SASRec (Self-Attentive Sequential Recommendation), but encountered limitations:

- Metadata blindness: SASRec focuses purely on item sequences, ignoring rich product attributes (color, type, price)
- Temporal granularity: Treats purchases as ordered sequences but doesn't capture real calendar time (seasonal trends, promotions)
- Cold-start weakness: Struggles with new products that lack sequential interaction history


.


