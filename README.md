# Movie Recommender: GCN vs R-GCN

This project compares two graph neural network approaches to movie recommendation:

- a **Graph Convolutional Network (GCN)** as a baseline;
- a **Relational Graph Convolutional Network (R-GCN)** that additionally incorporates rating relations and movie genre information.

The task is formulated as **binary link prediction**. Observed user-movie interactions are treated as positive edges, while unobserved user-movie pairs are sampled as negative edges. The models predict whether an interaction between a user and a movie is likely to exist.

## Dataset

The comparison is performed using **MovieLens 100K** dataset available through PyTorch Geometric

https://pytorch-geometric.readthedocs.io/en/latest/generated/torch_geometric.datasets.MovieLens100K.html

## Models

### GCN

The baseline represents MovieLens as a homogeneous user-movie graph. User and movie features are projected into a shared feature space. Two GCN layers are used to obtain node embeddings. User and movie embeddings are then concatenated and passed to an MLP link predictor.

### R-GCN

The R-GCN model preserves relational information in the graph:

- ratings 1–5 are represented as five different user-movie relation types;
- movie genres are represented as additional genre nodes;
- movies and genres are connected through `has_genre` relations.

This allows the model to use both collaborative user-movie interactions and explicit genre information during message passing.

## Results

After limited hyperparameter tuning, the best configurations achieved:

| Model | Test BCE | Test Accuracy |
|------|---------:|--------------:|
| GCN | 0.431 | 0.810 |
| R-GCN | 0.388 | 0.830 |

The R-GCN improves test accuracy by approximately **2.0 percentage points**. This suggests that explicitly modeling relational information provides useful additional signal for recommendation.

## Repository Structure

- `rgcn.ipynb` – data preparation, model implementation, training, and evaluation
- `hyperparameters.md` – hyperparameter experiments
- `data/` – project data
- `README.md` – project overview

## Technologies

Python, PyTorch, PyTorch Geometric, NumPy, scikit-learn
