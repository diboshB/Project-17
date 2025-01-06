# Project-17
Captsone_Project - Clustering - E_Commerce behavior data


Introduction:
In a modern e-commerce platform, understanding customer behavior is
critical for optimizing user experience and increasing sales. The provided
dataset contains information about user interactions with various products on
the platform, including event types, product categories, brands, prices, and
user sessions. This is an unsupervised machine learning problem aimed at
uncovering hidden patterns in user behavior to group similar users or actions.
These insights could assist in personalizing user experiences, targeting
advertisements, or improving product recommendations.
In this solution, we will explore the process of data cleaning, feature
selection, clustering, model evaluation, and insights generation to
identify key customer segments based on their interaction patterns and
behaviors. The goal is to uncover actionable insights that can inform business
strategies and improve the overall user experience on the platform.
1.1 Database Connection and Data Extraction:
• We connected to an SQLite database (Database.db) and fetched data
from the Ecommerce_data table into a pandas DataFrame.
• This data contains various columns such
as user_id, product_id, category_id, brand, price, event_type, and event_time.
1.2 Handling Missing Values:
• The missing values were handled by filling them with defaults:
o Missing category_code and brand were replaced with 'Unknown'.
o Missing user_session was replaced with 'No Session'.
• We ensured that event_time is converted to the proper datetime format.
1.3 Feature Engineering:
• Extracted key time-based features from event_time:
o day_of_week: This represents the day of the week (0 for Monday, 6
for Sunday).
o hour_of_day: This represents the hour of the day (0 to 23).
o month: This represents the month of the event (1 to 12).
These new features allow we to capture temporal patterns in user behavior,
which are crucial for understanding purchase timing and engagement trends.
Step 2: Feature Selection and Scaling
2.1 Numerical Features Selection:
• The features selected for clustering include:
o Price
o Day of week
o Hour of day
o Month
o Event type columns (which represent various event types as
binary features, created using one-hot encoding).
2.2 Scaling the Features:
• The features were scaled using StandardScaler to ensure they are
normalized (mean of 0 and standard deviation of 1). Scaling is important
to avoid features like price dominating due to their larger numerical
range.
Step 3: Clustering and Identifying the Number of Clusters
3.1 Elbow Method:
• The KMeans algorithm was used for clustering. The "elbow method" was
applied to identify the optimal number of clusters. This is done by
plotting the Within-Cluster Sum of Squares (WCSS), which
decreases as the number of clusters increases.
o Interpretation: In this case, the elbow curve suggests
that k=3 clusters is an appropriate choice, as adding more clusters
does not significantly reduce WCSS.
3.2 KMeans Clustering:
• The KMeans algorithm was run with k=3 clusters. The resulting clusters
were added to the data as a new column (cluster), allowing we to
segment users into distinct groups based on their behavior.
Step 4: Evaluation of the Model
4.1 PCA for Visualization:
• Principal Component Analysis (PCA) was applied to reduce the data to
two components (2D) for visualization. This allows us to see the
distribution of the clusters in a lower-dimensional space, which is easier
to interpret.
o Interpretation: The scatter plot visualized the three clusters in
two dimensions. Clusters are spread out, suggesting that there
are distinct patterns among the users in terms of their
engagement and purchases.
4.2 Silhouette Score:
• The silhouette score for the clustering was calculated to evaluate the
quality of the clustering:
o Silhouette Score (Sample): 0.459
o Interpretation: A silhouette score close to 1 indicates well-
separated clusters, while values close to 0 indicate overlapping
clusters. A score of 0.459 suggests moderate clustering quality,
with some overlap between the clusters. This indicates that while
the clustering captures some patterns, there may still be room for
improvement.
Step 5: Profiling the Clusters
5.1 Cluster Profiling:
• We grouped the data by clusters and calculated the mean values for the
numerical features (price, day of week, hour of day, month). The profiles
of the clusters provide insights into the typical behavior of users in each
group.
o Cluster 0: Average price: 206.8, average hour of day: 4.8,
frequent category: construction.tools.light, frequent brand: samsung.
o Cluster 1: Average price: 204.2, average hour of day: 10.5,
frequent category: construction.tools.light, frequent brand: samsung.
o Cluster 2: Average price: 1145.1, average hour of day: 8.5,
frequent category: construction.tools.light, frequent brand: apple.
Interpretation:
o Cluster 0 and Cluster 1 appear to be budget-conscious users, with
lower average prices and frequent purchases in
the construction.tools.light category, primarily buying Samsung
products.
o Cluster 2, on the other hand, has a significantly higher average
price, and users in this group tend to purchase products from
the construction.tools.light category but with a preference for Apple
products.
5.2 Categorical Profiling:
• We also computed the most frequent category and brand for each
cluster:
o Most Frequent Category: All clusters predominantly purchase
items from the construction.tools.light category.
o Most Frequent Brand: Cluster 0 and Cluster 1 predominantly
buy Samsung products, while Cluster 2 favors Apple.
Step 6: Investigating Unknown Brands
6.1 Unknown Brands in Categories:
• We checked how frequently the brand "Unknown" appears in each
category, with several categories having a significant proportion of
unknown brands.
o Interpretation: This could indicate missing or unbranded
products, or it may suggest that customers frequently purchase
generic or no-name items in certain categories.
6.2 Unknown Brands per Cluster:
• The proportion of "Unknown" brands was also investigated across
clusters:
o Cluster 0: 42,064 "Unknown" brands
o Cluster 1: 57,745 "Unknown" brands
o Cluster 2: 5,143 "Unknown" brands
Interpretation: Clusters 0 and 1 have a significantly higher proportion
of purchases with unknown brands. This suggests that customers in
these clusters are more likely to buy unbranded or generic items, while
Cluster 2 has a preference for branded items (like Apple).
Step 7: Visualizing the Results
We visualized several aspects of the data, including:
• Heatmap of Hour-of-Day Patterns by Day of Week: This heatmap
displayed the average price for each hour of the day across different
days of the week. It helps to identify peak shopping times and price
fluctuations based on time.
• Bar Plot for Average Price per Cluster: This plot shows the average
price for each cluster. Cluster 2 stands out with a much higher average
price, indicating that this cluster is likely made up of high-value
customers.
• Bar Plot for Unknown Brands per Cluster: This plot visualizes the
number of unknown brands across clusters. As mentioned earlier,
Clusters 0 and 1 have a significant number of unknown brands,
indicating that they are more likely to purchase unbranded items.
Insights for Business:
1. Customer Segmentation for Targeted Marketing:
o Cluster 0 & 1: These clusters are likely budget-conscious
shoppers who purchase products from
the construction.tools.light category and prefer Samsung products.
Marketing strategies for these groups should focus on
promotions for budget-friendly, generic, or unbranded items.
o Cluster 2: This group consists of high-value customers who tend
to purchase more expensive items and prefer Apple products.
Premium product lines and exclusive offers targeted at this group
could increase engagement and sales.
2. Unknown Brand Analysis:
o A large proportion of purchases in Clusters 0 and 1 involve
unknown brands. This might indicate missing product information,
unbranded or generic products, or even customer indifference to
brand names. Investigating whether this is due to missing data or
actual purchasing behavior could help refine product offerings.
o Offering more visibility or incentives for branded products might
help increase brand awareness in these clusters.
3. Optimal Pricing and Timing:
o The heatmap of hour-of-day patterns by day of the week can be
used to identify peak shopping times. Understanding these times
allows the platform to optimize pricing and marketing efforts.
o For instance, offering flash sales or discounts during off-peak
hours could help stimulate more activity during less active
periods.
4. Product Recommendations:
o Based on the clustering of products, we can tailor product
recommendations. For example, Cluster 2 users might be
recommended high-end tools or Apple products, while users in
Clusters 0 and 1 might be shown more budget-friendly options.
Conclusion:
By clustering customer behavior and analyzing the results, we have uncovered
three distinct groups of customers with different spending behaviors, brand
preferences, and shopping patterns. These insights can be directly applied to
improve marketing strategies, personalized product recommendations, and
sales optimization, leading to enhanced customer experience and increased
revenue for the platform.
