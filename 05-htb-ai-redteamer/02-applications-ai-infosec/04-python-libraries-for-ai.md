# Python Libraries for AI — Cheat Sheet

---

## Scikit-learn — ML classique

Bibliothèque ML complète et cohérente. Une seule API pour tous les algos : `fit()` → `predict()`.

**Algorithmes disponibles :**

- Supervised : Linear/Logistic Regression, SVM, Decision Trees, Naive Bayes, Random Forests
- Unsupervised : K-Means, DBSCAN, PCA, t-SNE

---

### Preprocessing

```python
from sklearn.preprocessing import StandardScaler, MinMaxScaler
from sklearn.preprocessing import OneHotEncoder, LabelEncoder
from sklearn.impute import SimpleImputer

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)          # normalise les features

encoder = OneHotEncoder()
X_encoded = encoder.fit_transform(X)        # encode les catégories en binaire

imputer = SimpleImputer(strategy='mean')
X_imputed = imputer.fit_transform(X)        # remplace les valeurs manquantes
```

### Train / Eval

```python
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
scores = cross_val_score(model, X, y, cv=5)     # k-fold cross validation
```

### Entraîner un modèle

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(C=1.0)
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
```

---

## PyTorch — Deep Learning

Framework pour réseaux de neurones complexes. Utilise des **graphes computationnels dynamiques** — construits à la volée, plus flexibles que TensorFlow.

**Points forts :** GPU, autograd (gradients automatiques), grande communauté.

---

### Tensors

```python
import torch

x = torch.tensor([1.0, 2.0, 3.0])
if torch.cuda.is_available():
    x = x.to('cuda')           # déplacer sur GPU si dispo
```

### Construire un modèle

**Sequential** (simple, couche par couche) :

```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 128),
    nn.ReLU(),
    nn.Linear(128, 10),
    nn.Softmax(dim=1)
)
```

**Module class** (flexible, architectures complexes) :

```python
class CustomModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.layer1 = nn.Linear(784, 128)
        self.relu = nn.ReLU()
        self.layer2 = nn.Linear(128, 10)

    def forward(self, x):
        return self.layer2(self.relu(self.layer1(x)))
```

### Training loop

```python
optimizer = torch.optim.Adam(model.parameters(), lr=0.001)
loss_fn = nn.CrossEntropyLoss()

for epoch in range(epochs):
    y_pred = model(x_batch)           # forward pass
    loss = loss_fn(y_pred, y_batch)   # calculer la loss
    optimizer.zero_grad()             # reset les gradients
    loss.backward()                   # backpropagation
    optimizer.step()                  # mettre à jour les poids
```

### Data loading

```python
from torch.utils.data import Dataset, DataLoader

class CustomDataset(Dataset):
    def __init__(self, data, labels):
        self.data, self.labels = data, labels
    def __len__(self):
        return len(self.data)
    def __getitem__(self, idx):
        return self.data[idx], self.labels[idx]

dataloader = DataLoader(CustomDataset(data, labels), batch_size=32, shuffle=True)
```

### Sauvegarder / charger

```python
torch.save(model.state_dict(), 'model.pth')       # sauvegarder

model.load_state_dict(torch.load('model.pth'))    # charger
model.eval()                                       # mode inférence
```

---

## Scikit-learn vs PyTorch — quand utiliser quoi ?

|Scikit-learn|PyTorch|
|---|---|---|
|**Usage**|ML classique, petits datasets|Deep learning, réseaux de neurones|
|**API**|Simple — `fit/predict`|Plus verbose, plus flexible|
|**GPU**|Non|Oui|
|**Modèles**|Arbres, SVM, régression...|CNN, RNN, Transformers...|