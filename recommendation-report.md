Collaborative Filtering and Graph-Based Random Walks (Pixie-Inspired)

1. Introduction
With countless options available across streaming platforms like Netflix, Prime Video, and Hulu, helping users discover content they’ll enjoy has become a crucial challenge. This is where recommendation systems come in—they aim to deliver the right content to the right user at the right time.

In this project, we explore and compare three approaches to personalized movie recommendations:

User-Based Collaborative Filtering: Recommends what similar users liked.

Item-Based Collaborative Filtering: Suggests movies similar to those a user rated highly.

Graph-Based Random Walks (inspired by Pixie, Pinterest’s recommendation engine): Explores a user-movie graph via random paths to find relevant items.

All three models were implemented and evaluated using the MovieLens 100K dataset.

2. Dataset Overview: MovieLens 100K
We used the MovieLens 100K dataset as the foundation for building and testing our models. It contains:

943 users

1,682 movies

100,000 ratings (on a 1–5 scale)

Each rating record includes: User ID, Movie ID, Rating, and Timestamp.

Data Preprocessing:
Removed duplicate and inconsistent entries

Constructed a user-item rating matrix for collaborative filtering

Generated efficient index maps for fast lookup

Built a bipartite graph for the Pixie-inspired model, connecting users and the movies they rated

3. Recommendation Methodologies
We implemented and compared three different algorithms:

A. User-Based Collaborative Filtering
This method recommends movies by identifying users with similar tastes.

Computed cosine similarity between users using their rating vectors

For a given user, selected the top-K similar users ("neighbors")

Aggregated the neighbors' ratings to suggest new movies

Performs well when users have enough overlapping ratings

Limitations: struggles with sparse data or new users (cold-start problem)

B. Item-Based Collaborative Filtering
Rather than comparing users, this method looks at how similar items are.

Calculated cosine similarity between movie vectors (how users rated each movie)

If a user liked Movie A, recommend Movie B if many others rated both highly

Produces stable, high-confidence results even as user base changes

Good for scalability; doesn’t depend on active users

Limitation: Recommendations can become repetitive or genre-restricted

C. Pixie-Inspired Graph-Based Random Walk
This approach leverages graph traversal for discovery, using the user-movie interaction graph:

Constructed a bipartite graph where:

Nodes = users and movies

Edges = user ratings (unweighted in this version)

Initiated random walks from a seed movie

At each step, randomly move to a connected node

Reset to seed movie occasionally (to mimic user attention reset)

Counted how often each movie is visited—higher frequency implies higher relevance

Unlike collaborative filtering, this method captures indirect relationships and uncovers content from adjacent "interest zones" on the graph.

4. Implementation Details
Collaborative Filtering
Built rating vectors from the preprocessed dataset

Used matrix operations for fast similarity computations

Aggregated weighted scores for top-K recommendations

Graph Construction
Represented as an adjacency list for memory efficiency

Each user is linked to rated movies, and each movie links back to users

Random Walk Logic
From each seed node, executed fixed-length walks (e.g., 100 steps)

Chose the next node uniformly at random

Counted movie visits to build a ranked recommendation list

5. Results and Evaluation
Sample Outputs

Method	Example Output
User-Based CF	If User 234 and 312 share similar tastes, and 312 rated "Blade Runner" and "The Matrix" highly, then 234 is recommended those titles
Item-Based CF	A user who liked "Pulp Fiction" is recommended "Kill Bill" and "Reservoir Dogs" due to similar global rating patterns
Random Walk (Pixie)	Starting from "Titanic", recommendations like "Shawshank Redemption" or "The Notebook" emerge, even if they differ in genre
Comparison Table

Method	Advantages	Limitations
User-Based CF	Personalized; captures user preferences	Suffers with sparse or new user data
Item-Based CF	Stable; efficient; good for new users	Can overfit on genre/style
Random Walk (Pixie)	Fast; serendipitous; diverse suggestions	Needs rich graph structure; lacks personalization
Limitations and Future Work
Random walks use uniform edge weights—introducing weights based on rating strength or recency could improve relevance

No use of movie metadata (genres, tags, etc.)

Personalization in random walk restarts or edge biases could boost performance

6. Key Takeaways and Real-World Relevance
This project provided valuable hands-on experience in building and comparing recommender systems:

Collaborative Filtering is reliable when user history is dense

Pixie-inspired models show great potential for dynamic and scalable environments

Graph structures let us uncover indirect yet meaningful content connections

These techniques form the backbone of recommendation engines used by Netflix, YouTube, Pinterest, Amazon, and many others—serving millions of users every day.

7. Insights from Output Behavior
💡 User-Based CF:
Captures taste clusters: For example, users who like indie or foreign films tend to get clustered together.

Example: User 234 receives "Blade Runner" and "The Matrix" based on similar users’ high ratings.

Insight: Great for personalization but may lack recommendation diversity.

💡 Item-Based CF:
Emphasizes global consensus: Movies often co-rated similarly are recommended.

Example: If "Pulp Fiction" is liked, system recommends "Reservoir Dogs" or "Kill Bill".

Insight: More consistent for users with minimal history, but suggestions may lack novelty.

💡 Pixie-Inspired Graph Walks:
Surfaces hidden relationships and encourages content exploration.

Example: Starting from "Titanic", returns "Shawshank Redemption", "Forrest Gump", etc.—not genre-based, but connected by user patterns.

Insight: Ideal for discovering diverse or lesser-known content.