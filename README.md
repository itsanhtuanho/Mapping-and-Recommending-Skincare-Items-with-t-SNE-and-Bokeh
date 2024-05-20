# Mapping-and-Recommending-Skincare-Items-with-t-SNE-and-Bokeh
Visualizing and recommending skincare products using scraped product data from Yesstyle.com

![isntree_real_green_tea_2048x](https://github.com/itsanhtuanho/Mapping-and-Recommending-Skincare-Items-with-t-SNE-and-Bokeh/assets/46179761/7c4a240f-db24-464e-bd2e-b6cc5a07e893) <br>


# Introduction
Choosing your optimal skincare routine can be a daunting and exhausting task. With thousands and thousands of products to choose from, how would you pick which ones would be effective in improving your overall skin health? The only real answer to that is simply try them and see their results first-hand, a process that can up to 8 weeks. This is because skincare is highly personalized -- what works for one person may not necessarily work for another person, even if they share the skin type (dry, normal, combination, oily) <br>

Now let's say you are in the intermediate stage of your skincare journey and you already have an established skincare routine that works for you. But for whatever reason, you want to try out a new toner. The company claims that this new toner offers many benefits, and you notice they mention similar benefits from the toner that you are currently using. Is there any way to preemptively investigate this?

Many people suffer from having **sensitive** skin, whereby a person experiences unpleasant sensations - pulling, prickling, burning or stinging - in response to factors such as temperature changes, wind, UV, hard water or harsh products. If you encounter a product that has similar ingredients to that of a product that has worked well for you in the past, chances are you will also respond well to the new product.

# Objective
By vectorizing the ingredient list for each skincare product and then reducing its dimension to 2, we can plot and **visualize** its chemical composition. We can then use its features to compute similarity metrics for a given product in order to provide **recommendations** based on ingredient similarity.

# Data
Skincare product data was scraped from [Yesstyle](https://www.yesstyle.com/en/home.html), a global online retailer specializing in Asian beauty products and cosmetics. This dataset contains releavant information about skincare products, including price, brand, number of reviews, and ingredients. The raw dataset contains 2292 rows, while the cleaned dataset contains 1574 rows. Data was scraped used using [Beautiful Soup](https://beautiful-soup-4.readthedocs.io/en/latest/) and [Selenium](https://selenium-python.readthedocs.io/).

# Data Preprocessing and Algorithm
After data cleaning, the ingredients list corpus was vectorized via tokenization and one-hot encoding. The resulting sparse matrix had a dimension of (1574, 4930), which means there were 4930 unique ingredients. Dimensionality reduction with **2 components** was performed via **t-SNE**, a non-linear, non-deterministic dimensionality reduction technique that maximizes variance (similar to PCA), but it does so by keeping similar data points together, both in higher and lower dimensions. This makes it ideal for data visualization and exploratory data analysis tasks. 

In order to visualize the chemical composition of each product, an interactive visualization was made using [Bokeh](https://bokeh.org/), which includes a 2-D scatter plot, hover tool, and a drop down menu to allow users to **filter** through skincare product categories (cleanser, moistirizer, toner, serum, spf). Upon hovering each data point, users can see product information such as price, brand, number of reviews, etc. <br>

![bokeh](https://github.com/itsanhtuanho/Mapping-and-Recommending-Skincare-Items-with-t-SNE-and-Bokeh/assets/46179761/520b4b6e-e75e-4015-9faa-1f9296a2feb8) <br>

# Recommendations
**Cosine similarity** was used as a similarity metric, which measures the cosine of the angle between two vectors in a multidimensional space. It's widely used in recommendation systems, especially when dealing with high-dimensional data, as it is invariant to the magnitude of the vectors. The closer the cosine similarity is to 1, the more similar the items are, and vice versa. Using the recommender tool for the **Matcha Hydrating Foam Cleanser** from B.LAB, here are the results:

| Recommendation Number | Product                                             | Brand             | Price | Dist     |
|-----------------------|-----------------------------------------------------|-------------------|-------|----------|
| 0                     | Matcha Hydrating Foam Cleanser                     | B.LAB             | 10.08 | 1.000000 |
| 1                     | No. 3 All Green pH Balancing Cleanser              | numbuzin          | 13.36 | 0.999998 |
| 2                     | ACSEN Oil Cut Cleansing 120ml                       | TROIAREUKE        | 40.60 | 0.999978 |
| 3                     | Gentle Cleansing Foam Mini                          | Sulwhasoo         | 10.80 | 0.999863 |
| 4                     | Gentle Black Facial Cleanser                        | Dear, Klairs      | 18.80 | 0.999542 |
| 5                     | Cleansing Gel Be Clean Be Moist                     | Huxley            | 20.00 | 0.999474 |
| 6                     | Apple Seed Lip & Eye Remover 100ml                  | innisfree         | 12.90 | 0.999454 |
| 7                     | Heartleaf Acne Facial Cleanser                      | Anua              | 16.70 | 0.999333 |
| 8                     | Collagen Bubble Cleanser                            | VILLAGE 11 FACTORY| 12.08 | 0.999246 |
| 9                     | Cleansing Water Be Clean Be Moist 200ml             | Huxley            | 18.88 | 0.999245 |
| 10                    | Curel Intensive Moisture Care Makeup Cleansing...   | Kao               | 19.00 | 0.999180 |

