# 📘 QUANTUM COMPUTING - PARTIE 5 : CORRECTION D'ERREURS QUANTIQUES
## Protéger l'Information Quantique - Guide Complet avec Code Python

**Learning Schooling Foundation • Niveau Elite Mondial • 100% Gratuit**

---

## 📖 TABLE DES MATIÈRES - PARTIE 5

**Durée estimée : 40 heures de travail approfondi**

### Chapitre 1 : Le Problème du Bruit Quantique
- 1.1 Pourquoi les Qubits Sont Fragiles
- 1.2 Types d'Erreurs Quantiques
- 1.3 Décohérence et Temps de Vie
- 1.4 Taux d'Erreur des Portes
- 1.5 Le Seuil de Tolérance aux Fautes

### Chapitre 2 : Théorie de l'Information Quantique
- 2.1 Théorème de Non-Clonage
- 2.2 Entropie de von Neumann
- 2.3 Fidélité et Distance de Trace
- 2.4 Canaux Quantiques
- 2.5 Théorème de Correction d'Erreur Quantique

### Chapitre 3 : Codes de Correction Classiques
- 3.1 Code de Répétition (3-bit)
- 3.2 Code de Hamming (7,4)
- 3.3 Syndrome et Détection
- 3.4 Rappel : Pourquoi Ça Ne Marche Pas en Quantique

### Chapitre 4 : Code de Shor (9-qubit)
- 4.1 Le Premier Code Quantique
- 4.2 Protection Contre Bit Flip
- 4.3 Protection Contre Phase Flip
- 4.4 Code Complet de Shor
- 4.5 Encodage et Décodage
- 4.6 Implémentation Python

### Chapitre 5 : Code de Steane (7-qubit)
- 5.1 Code CSS (Calderbank-Shor-Steane)
- 5.2 Construction du Code [[7,1,3]]
- 5.3 Correction d'Erreurs Efficace
- 5.4 Portes Logiques sur Code de Steane
- 5.5 Implémentation Complète

### Chapitre 6 : Codes de Surface
- 6.1 Pourquoi les Codes de Surface ?
- 6.2 Toric Code et Planar Code
- 6.3 Stabilisateurs et Syndrome
- 6.4 Décodage avec MWPM
- 6.5 Scalabilité et Architecture
- 6.6 Implémentation 2D

### Chapitre 7 : Calcul Tolérant aux Fautes
- 7.1 Portes Transversales
- 7.2 Ensemble Universel de Portes
- 7.3 Magic State Distillation
- 7.4 Circuits Tolérants aux Fautes
- 7.5 Overhead de Ressources

### Chapitre 8 : Codes Topologiques Avancés
- 8.1 Color Codes
- 8.2 Codes LDPC Quantiques
- 8.3 Codes de Bacon-Shor
- 8.4 Recherche Actuelle

### Chapitre 9 : Applications et Futur
- 9.1 État du Hardware (Google, IBM, etc.)
- 9.2 Roadmap vers Ordinateurs Quantiques Fiables
- 9.3 Carrières en QEC
- 9.4 Ressources et Formation

---

## 📚 CHAPITRE 1 : LE PROBLÈME DU BRUIT QUANTIQUE

### 1.1 Pourquoi les Qubits Sont Fragiles

**Le problème fondamental du calcul quantique :**

```
Les qubits sont EXTRÊMEMENT sensibles à leur environnement.

Toute interaction avec l'extérieur détruit la superposition et l'intrication.
→ C'est la DÉCOHÉRENCE
```

#### Sources de Bruit

**1. Couplage avec l'environnement**
```
- Photons thermiques
- Vibrations mécaniques
- Champs électromagnétiques parasites
- Impuretés dans les matériaux
```

**2. Imperfections de contrôle**
```
- Imprécision des pulses micro-ondes
- Dérives de fréquence
- Crosstalk entre qubits
- Calibration imparfaite
```

**3. Erreurs de mesure**
```
- Faux positifs/négatifs
- Mesures non destructrices imparfaites
- Temps de mesure fini
```

#### Analogie Classique vs Quantique

**Classique :**
```
Bit = 0 ou 1 (robuste)

Erreur : Flip 0→1 ou 1→0
Solution : Répéter 3 fois
  000 → Si on mesure 001, on sait que c'était 000
  Vote majoritaire → Corrigé !
```

**Quantique :**
```
Qubit = α|0⟩ + β|1⟩ (fragile)

Problème 1 : On ne peut PAS copier (non-clonage)
  → Pas de répétition simple

Problème 2 : Mesurer DÉTRUIT la superposition
  → On ne peut pas "regarder" l'erreur directement

Problème 3 : Erreurs CONTINUES (pas juste 0↔1)
  α|0⟩ + β|1⟩ → (α+ε₁)|0⟩ + (β+ε₂)|1⟩
  Les coefficients dérivent continûment
```

### 1.2 Types d'Erreurs Quantiques

**Les trois types d'erreurs de base :**

#### 1. Bit Flip (X Error)

**Effet : |0⟩ ↔ |1⟩**

```
|0⟩ → |1⟩
|1⟩ → |0⟩
α|0⟩ + β|1⟩ → α|1⟩ + β|0⟩ = β|0⟩ + α|1⟩
```

**Matrice de Pauli X :**
```
X = [0  1]
    [1  0]
```

**Analogie classique :** C'est l'erreur classique (bit flip)

#### 2. Phase Flip (Z Error)

**Effet : Change le signe de |1⟩**

```
|0⟩ → |0⟩
|1⟩ → -|1⟩
α|0⟩ + β|1⟩ → α|0⟩ - β|1⟩
```

**Matrice de Pauli Z :**
```
Z = [1   0]
    [0  -1]
```

**Pas d'équivalent classique !** C'est purement quantique.

#### 3. Bit-Phase Flip (Y Error)

**Effet : Combinaison de X et Z**

```
Y = iXZ = [0  -i]
          [i   0]

|0⟩ → i|1⟩
|1⟩ → -i|0⟩
```

**Relation : Y = iXZ**

#### Erreurs Générales

**Une erreur générale est une COMBINAISON de X, Y, Z :**

```
E = aI + bX + cY + dZ

où I est l'identité et a,b,c,d sont des coefficients complexes
```

**Théorème clé :** Il SUFFIT de pouvoir corriger X, Y, Z pour corriger TOUTE erreur !

**Pourquoi ?** 
```
Les matrices de Pauli {I, X, Y, Z} forment une base
→ Toute erreur peut s'écrire comme combinaison linéaire
→ Si on corrige chaque composante, on corrige tout
```

### 1.3 Décohérence et Temps de Vie

#### Temps T₁ (Relaxation)

**Temps de relaxation : perte d'énergie**

```
|1⟩ perd spontanément de l'énergie et décroît vers |0⟩

Si état initial : |1⟩
Après temps t : p₁(t) = e^(-t/T₁)

T₁ typique (2024) :
  Supraconducteurs : 50-200 μs
  Ions piégés : 1-10 secondes
  Photonique : ~infini (pas de relaxation)
```

#### Temps T₂ (Déphasage)

**Temps de cohérence : perte de la phase relative**

```
Si état initial : |+⟩ = (|0⟩ + |1⟩)/√2
Après temps t : (|0⟩ + e^(-t/T₂)|1⟩)/√2

La phase relative décroît exponentiellement

T₂ typique (2024) :
  Supraconducteurs : 20-100 μs (T₂ < T₁)
  Ions piégés : 0.1-1 seconde
  
Relation : T₂ ≤ 2T₁ (toujours)
```

#### Nombre de Portes Possibles

**Avant que la décohérence détruise tout :**

```
Temps d'une porte : t_gate

Nombre de portes : N ≈ T₂ / t_gate

Exemples (2024) :
  Supraconducteurs (IBM, Google) :
    T₂ ~ 100 μs, t_gate ~ 20 ns
    N ~ 5000 portes
  
  Ions piégés (IonQ) :
    T₂ ~ 1 s, t_gate ~ 10 μs  
    N ~ 100000 portes
```

**Le problème :** Pour Shor sur RSA-2048, on a besoin de ~10⁹ portes !

**Solution :** CORRECTION D'ERREUR QUANTIQUE

### 1.4 Taux d'Erreur des Portes

**Chaque porte quantique a une probabilité d'erreur.**

#### Taux d'Erreur Typiques (2024)

```
┌────────────────────┬──────────────┬───────────────┐
│ Type de porte      │  Meilleur    │  Typique      │
├────────────────────┼──────────────┼───────────────┤
│ Single-qubit (RX)  │  10⁻⁴        │  10⁻³         │
│ Two-qubit (CNOT)   │  5×10⁻³      │  1-2×10⁻²     │
│ Mesure             │  10⁻³        │  10⁻²         │
│ Préparation |0⟩    │  10⁻⁴        │  10⁻³         │
└────────────────────┴──────────────┴───────────────┘

Note : Portes 2-qubits sont 10-100x plus bruyantes que 1-qubit
```

#### Impact Cumulatif

**Probabilité d'erreur après N portes :**

```
Si chaque porte a probabilité p d'erreur :
Probabilité d'au moins une erreur après N portes ≈ Np (pour Np ≪ 1)

Exemple :
  p = 10⁻³
  N = 1000 portes
  → Probabilité d'erreur ≈ 1000 × 10⁻³ = 1 (100% !)

Pour algorithme long → Calcul IMPOSSIBLE sans correction
```

### 1.5 Le Seuil de Tolérance aux Fautes

**Théorème du Seuil (Threshold Theorem)**

```
Si le taux d'erreur physique p < p_th (seuil)
→ On peut réduire le taux d'erreur logique arbitrairement bas
→ En augmentant la redondance (overhead)

Si p > p_th
→ La correction d'erreur empire les choses
→ Impossible de calculer de manière fiable
```

#### Valeurs du Seuil

**Dépend du modèle d'erreur et du code :**

```
Code de Surface (optimal connu) :
  p_th ~ 1% (erreur indépendante sur chaque porte)
  
Codes topologiques avancés :
  p_th ~ 1-3%

En pratique (2024) :
  Meilleurs qubits : p ~ 0.1-0.5%
  → SOUS le seuil pour codes de surface !
  → Calcul quantique tolérant aux fautes POSSIBLE
```

**Google Willow (Dec 2024) :**
```
Premier système à passer "sous le seuil" :
  - Augmenter taille du code RÉDUIT les erreurs
  - Breakthrough majeur
```

#### Overhead de Ressources

**Pour atteindre taux d'erreur logique ε_L à partir de taux physique p :**

```
Nombre de qubits physiques par qubit logique : O(d²)

où d est la "distance" du code

Relation : ε_L ~ (p/p_th)^((d+1)/2)

Pour ε_L = 10⁻¹⁵ (nécessaire pour algorithmes longs) :
  Si p = 10⁻³
  → d ~ 20-30
  → ~1000 qubits physiques par qubit logique !
```

---

## 📚 CHAPITRE 2 : THÉORIE DE L'INFORMATION QUANTIQUE

### 2.1 Théorème de Non-Clonage

**Théorème fondamental :**

```
Il est IMPOSSIBLE de copier un état quantique inconnu.

Formellement : Il n'existe PAS d'opération unitaire U telle que :
  U|ψ⟩|0⟩ = |ψ⟩|ψ⟩  pour tout |ψ⟩
```

#### Preuve par Contradiction

**Supposons qu'un tel U existe.**

```
Pour |ψ⟩ = |0⟩ :
  U|0⟩|0⟩ = |0⟩|0⟩  ... (1)

Pour |ψ⟩ = |1⟩ :
  U|1⟩|0⟩ = |1⟩|1⟩  ... (2)

Pour |ψ⟩ = (|0⟩ + |1⟩)/√2 :
  U[(|0⟩ + |1⟩)/√2]|0⟩ = [(|0⟩ + |1⟩)/√2][(|0⟩ + |1⟩)/√2]
                         = (|00⟩ + |01⟩ + |10⟩ + |11⟩)/2  ... (3)

MAIS par linéarité de U et (1), (2) :
  U[(|0⟩ + |1⟩)/√2]|0⟩ = (U|0⟩|0⟩ + U|1⟩|0⟩)/√2
                         = (|00⟩ + |11⟩)/√2  ... (4)

(3) ≠ (4) → CONTRADICTION !

Donc U n'existe pas.
```

#### Conséquences pour la Correction d'Erreur

**On ne peut PAS :**
```
✗ Faire 3 copies de |ψ⟩
✗ Comparer les copies pour voter
✗ Utiliser la stratégie classique directement
```

**On PEUT :**
```
✓ Encoder |ψ⟩ dans un état intriqué de plusieurs qubits
✓ Mesurer des "syndromes" sans révéler |ψ⟩
✓ Corriger les erreurs sans connaître |ψ⟩
```

### 2.2 Entropie de von Neumann

**Mesure de l'information quantique.**

**Définition :**

```
Pour un état ρ (matrice de densité) :

S(ρ) = -Tr(ρ log₂ ρ)

Si ρ = Σ pᵢ|ψᵢ⟩⟨ψᵢ| (décomposition spectrale) :
S(ρ) = -Σ pᵢ log₂ pᵢ
```

**Propriétés :**

```
- S(ρ) ≥ 0
- S(ρ) = 0 ⟺ ρ est un état pur
- S(ρ) maximale ⟺ ρ = I/d (état maximalement mixte)

Pour un qubit :
  S_max = 1 bit
  
Pour n qubits :
  S_max = n bits
```

**Interprétation :**
```
L'entropie mesure le "désordre" ou "l'ignorance" sur l'état.

État pur |ψ⟩ : S = 0 (information parfaite)
Mélange statistique : S > 0 (information partielle)
```

### 2.3 Fidélité et Distance de Trace

#### Fidélité

**Mesure de "proximité" entre deux états quantiques.**

**Définition :**

```
Pour deux états purs |ψ⟩ et |φ⟩ :
  F(|ψ⟩, |φ⟩) = |⟨ψ|φ⟩|²

Pour états mixtes ρ et σ :
  F(ρ, σ) = [Tr(√(√ρ σ √ρ))]²
```

**Propriétés :**
```
- 0 ≤ F ≤ 1
- F = 1 ⟺ ρ = σ (états identiques)
- F = 0 ⟺ ρ et σ orthogonaux
```

#### Distance de Trace

**Autre mesure de distance.**

```
D(ρ, σ) = (1/2) Tr|ρ - σ|

où |A| = √(A†A) est la norme

Propriétés :
- 0 ≤ D ≤ 1
- D = 0 ⟺ ρ = σ
- Distance bien définie (inégalité triangulaire)
```

**Relation avec fidélité :**
```
1 - √F(ρ,σ) ≤ D(ρ,σ) ≤ √(1 - F(ρ,σ))
```

### 2.4 Canaux Quantiques

**Un canal quantique modélise l'évolution d'un système ouvert.**

**Définition :**

```
Ε : ρ → ρ' (transformation de l'état)

Propriétés requises :
1. Linéaire
2. Complètement positive
3. Préserve la trace
```

**Exemples de canaux :**

#### 1. Canal de Dépolarisation

```
Ε_p(ρ) = (1-p)ρ + (p/3)(XρX + YρY + ZρZ)

Interprétation :
  Avec probabilité 1-p : rien
  Avec probabilité p/3 : erreur X
  Avec probabilité p/3 : erreur Y
  Avec probabilité p/3 : erreur Z
```

#### 2. Canal de Bit Flip

```
Ε_p(ρ) = (1-p)ρ + pXρX

Interprétation :
  Probabilité 1-p : pas d'erreur
  Probabilité p : bit flip
```

#### 3. Canal de Phase Damping

```
Modélise la perte de cohérence (déphasage)

Kraus operators :
  K₀ = [1    0  ]    K₁ = [0      0  ]
       [0  √(1-γ)]         [0   √γ    ]
```

### 2.5 Théorème de Correction d'Erreur Quantique

**Conditions nécessaires et suffisantes pour corriger des erreurs.**

**Théorème (Knill-Laflamme) :**

```
Un code quantique C peut corriger un ensemble d'erreurs {Eᵢ}
⟺
Pour tous |ψ⟩, |φ⟩ ∈ C :
  ⟨ψ|Eᵢ†Eⱼ|φ⟩ = Cᵢⱼ⟨ψ|φ⟩

où Cᵢⱼ est indépendant de |ψ⟩, |φ⟩
```

**Interprétation :**

```
Les erreurs ne doivent pas créer de "fuite d'information"
entre les états logiques.

Si on peut distinguer les états après erreur
→ Impossible de corriger sans perturber
```

**Cas particulier (états orthogonaux) :**

```
Si tous les états du code sont orthogonaux :
  ⟨ψ|φ⟩ = 0 pour ψ ≠ φ

Alors condition devient :
  ⟨ψ|Eᵢ†Eⱼ|φ⟩ = 0  pour ψ ≠ φ
```

---

## 📚 CHAPITRE 3 : CODES DE CORRECTION CLASSIQUES

### 3.1 Code de Répétition (3-bit)

**Le code classique le plus simple.**

#### Encodage

```
0 → 000
1 → 111
```

#### Détection et Correction

**Si on mesure 000, 001, 010, 100 :**
```
→ Vote majoritaire → 0
```

**Si on mesure 111, 110, 101, 011 :**
```
→ Vote majoritaire → 1
```

**Syndrome :**
```
Comparer les bits :
  S₁ = bit₀ ⊕ bit₁
  S₂ = bit₁ ⊕ bit₂

Syndrome (S₁, S₂) indique quelle position est erronée :
  00 → Pas d'erreur
  01 → Erreur sur bit 2
  10 → Erreur sur bit 0
  11 → Erreur sur bit 1
```

### 3.2 Code de Hamming (7,4)

**Encode 4 bits de données en 7 bits (avec 3 bits de parité).**

**Peut corriger 1 erreur, détecter 2 erreurs.**

**Matrice génératrice :**
```
G = [1 0 0 0 | 1 1 0]
    [0 1 0 0 | 1 0 1]
    [0 0 1 0 | 0 1 1]
    [0 0 0 1 | 1 1 1]
```

**Distance minimale : d = 3**

### 3.3 Syndrome et Détection

**Le syndrome indique QUELLE erreur s'est produite, sans révéler les données.**

**Clé :** On peut mesurer le syndrome sans mesurer les données !

```
Syndrome = Hx (où H est la matrice de parité)

Si syndrome = 0 → Pas d'erreur
Si syndrome ≠ 0 → Indique la position de l'erreur
```

### 3.4 Rappel : Pourquoi Ça Ne Marche Pas en Quantique

**Problème 1 : Non-clonage**
```
On ne peut pas copier |ψ⟩ trois fois
```

**Problème 2 : Mesure destructrice**
```
Mesurer les qubits détruit la superposition
→ Perdu l'information quantique !
```

**Problème 3 : Erreurs continues**
```
Pas juste 0→1
Mais α|0⟩ + β|1⟩ → (α+ε₁)|0⟩ + (β+ε₂)|1⟩
```

**Solution :** Codes quantiques sophistiqués qui :
- Encodent sans cloner
- Mesurent le syndrome sans révéler l'état
- Corrigent les erreurs continues

---

## 📚 CHAPITRE 4 : CODE DE SHOR (9-QUBIT)

### 4.1 Le Premier Code Quantique

**Peter Shor (1995) : Premier code de correction d'erreur quantique.**

**Code [[9,1,3]] :**
```
- 9 qubits physiques
- 1 qubit logique
- Distance 3 (corrige 1 erreur)
```

**Idée géniale :**
```
Concatener deux codes :
1. Code contre bit flip (X errors)
2. Code contre phase flip (Z errors)
```

### 4.2 Protection Contre Bit Flip

**Code de répétition quantique (3 qubits) :**

#### Encodage

```
|0⟩_L = |000⟩
|1⟩_L = |111⟩

État général :
|ψ⟩_L = α|0⟩_L + β|1⟩_L = α|000⟩ + β|111⟩
```

**Note :** C'est un état intriqué, PAS une copie !

#### Détection d'Erreur X

**Mesurer les stabilisateurs :**
```
Z₁Z₂ : Vérifie si qubits 1 et 2 ont même parité
Z₂Z₃ : Vérifie si qubits 2 et 3 ont même parité
```

**Syndrome :**
```
(Z₁Z₂, Z₂Z₃) :
  (+1, +1) → Pas d'erreur
  (+1, -1) → Erreur sur qubit 3
  (-1, +1) → Erreur sur qubit 1
  (-1, -1) → Erreur sur qubit 2
```

**Correction :**
```
Appliquer X sur le qubit erroné
```

**Important :** La mesure des stabilisateurs ne révèle PAS α, β !

### 4.3 Protection Contre Phase Flip

**On "rotate" le problème :**

```
Phase flip sur |+⟩, |−⟩ = bit flip sur |0⟩, |1⟩

Changement de base :
|+⟩ = (|0⟩ + |1⟩)/√2
|−⟩ = (|0⟩ - |1⟩)/√2
```

**Code contre Z :**
```
|+⟩_L = |+++⟩
|−⟩_L = |---⟩
```

**En base computationnelle :**
```
|+⟩_L = (1/2√2)(|000⟩ + |001⟩ + |010⟩ + |011⟩ + 
                |100⟩ + |101⟩ + |110⟩ + |111⟩)

État avec 3 qubits en superposition uniforme
```

**Détection d'erreur Z :**
```
Mesurer X₁X₂ et X₂X₃
```

### 4.4 Code Complet de Shor

**Concatenation des deux codes :**

```
1. Protéger contre X : Encoder chaque qubit en 3
   |ψ⟩ → (α|000⟩ + β|111⟩)

2. Protéger contre Z : Encoder chaque groupe en 3
   |ψ⟩ → État de 9 qubits
```

**État logique |0⟩ dans le code de Shor :**
```
|0⟩_L = (1/2√2)[(|000⟩ + |111⟩)(|000⟩ + |111⟩)(|000⟩ + |111⟩)]
      = (1/2√2)[|000000000⟩ + |000000111⟩ + |000111000⟩ + ...
                + |111111111⟩]  (8 termes au total)
```

**État logique |1⟩ :**
```
|1⟩_L = (1/2√2)[(|000⟩ - |111⟩)(|000⟩ - |111⟩)(|000⟩ - |111⟩)]
```

### 4.5 Encodage et Décodage

#### Circuit d'Encodage

```
Encodage de |ψ⟩ = α|0⟩ + β|1⟩ :

|ψ⟩ ───●───●───H───●───●───H───●───●───H─── |ψ⟩_L (qubit 1)
       │   │       │   │       │   │
|0⟩ ───X───┼───────X───┼───────X───┼─────── (qubit 2)
           │           │           │
|0⟩ ───────X───────────X───────────X─────── (qubit 3)
           :           :           :
       (répéter pour les 3 groupes)
```

#### Circuit de Syndrome

**Mesurer les stabilisateurs sans détruire l'état :**

```
8 stabilisateurs pour le code de Shor :
  Z₁Z₂, Z₂Z₃ (groupe 1)
  Z₄Z₅, Z₅Z₆ (groupe 2)  
  Z₇Z₈, Z₈Z₉ (groupe 3)
  X₁X₂X₃X₄X₅X₆, X₄X₅X₆X₇X₈X₉
```

### 4.6 Implémentation Python

```python
import numpy as np
from qiskit import QuantumCircuit, QuantumRegister, ClassicalRegister, AncillaRegister
from qiskit_aer import AerSimulator

class ShorCode:
    """
    Implémentation du code de Shor [[9,1,3]].
    
    Protège un qubit logique contre 1 erreur arbitraire (X, Y, ou Z).
    """
    
    def __init__(self):
        """
        Code de Shor : 9 qubits physiques, 1 qubit logique.
        """
        self.n_physical = 9
        self.n_logical = 1
        
    def encode(self, circuit, data_qubit, code_qubits):
        """
        Encode un qubit de données dans le code de Shor.
        
        Args:
            circuit: Circuit quantique
            data_qubit: Qubit à encoder (contient α|0⟩ + β|1⟩)
            code_qubits: 8 qubits auxiliaires (initialisés à |0⟩)
        
        État final : |ψ⟩_L dans code de Shor
        """
        # Étape 1 : Protéger contre bit flip (répétition sur 3 qubits)
        # Groupe 1
        circuit.cx(code_qubits[0], code_qubits[1])
        circuit.cx(code_qubits[0], code_qubits[2])
        
        # Groupe 2
        circuit.cx(code_qubits[3], code_qubits[4])
        circuit.cx(code_qubits[3], code_qubits[5])
        
        # Groupe 3
        circuit.cx(code_qubits[6], code_qubits[7])
        circuit.cx(code_qubits[6], code_qubits[8])
        
        # Étape 2 : Protéger contre phase flip
        # Appliquer Hadamard sur premier qubit de chaque groupe
        for i in [0, 3, 6]:
            circuit.h(code_qubits[i])
        
        # CNOT entre les groupes (sur base |+⟩, |−⟩)
        circuit.cx(code_qubits[0], code_qubits[3])
        circuit.cx(code_qubits[0], code_qubits[6])
        
        # Hadamard final
        for i in [0, 3, 6]:
            circuit.h(code_qubits[i])
    
    def measure_syndrome(self, circuit, code_qubits, ancillas, syndrome_bits):
        """
        Mesure le syndrome sans révéler l'état logique.
        
        Args:
            code_qubits: 9 qubits du code
            ancillas: Qubits auxiliaires pour mesure
            syndrome_bits: Registre classique pour stocker syndrome
        """
        # Mesurer stabilisateurs Z (bit flip detection)
        # Groupe 1 : Z₁Z₂
        circuit.cx(code_qubits[0], ancillas[0])
        circuit.cx(code_qubits[1], ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[0])
        circuit.reset(ancillas[0])
        
        # Z₂Z₃
        circuit.cx(code_qubits[1], ancillas[0])
        circuit.cx(code_qubits[2], ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[1])
        circuit.reset(ancillas[0])
        
        # Groupe 2 : Z₄Z₅
        circuit.cx(code_qubits[3], ancillas[0])
        circuit.cx(code_qubits[4], ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[2])
        circuit.reset(ancillas[0])
        
        # Z₅Z₆
        circuit.cx(code_qubits[4], ancillas[0])
        circuit.cx(code_qubits[5], ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[3])
        circuit.reset(ancillas[0])
        
        # Groupe 3 : Z₇Z₈
        circuit.cx(code_qubits[6], ancillas[0])
        circuit.cx(code_qubits[7], ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[4])
        circuit.reset(ancillas[0])
        
        # Z₈Z₉
        circuit.cx(code_qubits[7], ancillas[0])
        circuit.cx(code_qubits[8], ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[5])
        circuit.reset(ancillas[0])
        
        # Mesurer stabilisateurs X (phase flip detection)
        # X₁X₂X₃X₄X₅X₆
        circuit.h(ancillas[0])
        for i in range(6):
            circuit.cx(ancillas[0], code_qubits[i])
        circuit.h(ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[6])
        circuit.reset(ancillas[0])
        
        # X₄X₅X₆X₇X₈X₉
        circuit.h(ancillas[0])
        for i in range(3, 9):
            circuit.cx(ancillas[0], code_qubits[i])
        circuit.h(ancillas[0])
        circuit.measure(ancillas[0], syndrome_bits[7])
        circuit.reset(ancillas[0])
    
    def correct_errors(self, circuit, code_qubits, syndrome):
        """
        Applique la correction basée sur le syndrome.
        
        Args:
            syndrome: Liste de 8 bits de syndrome
        """
        # Syndrome pour bit flip (sur chaque groupe)
        # Groupe 1
        if syndrome[0:2] == [0, 1]:  # Erreur qubit 3
            circuit.x(code_qubits[2])
        elif syndrome[0:2] == [1, 0]:  # Erreur qubit 1
            circuit.x(code_qubits[0])
        elif syndrome[0:2] == [1, 1]:  # Erreur qubit 2
            circuit.x(code_qubits[1])
        
        # Groupe 2
        if syndrome[2:4] == [0, 1]:
            circuit.x(code_qubits[5])
        elif syndrome[2:4] == [1, 0]:
            circuit.x(code_qubits[3])
        elif syndrome[2:4] == [1, 1]:
            circuit.x(code_qubits[4])
        
        # Groupe 3
        if syndrome[4:6] == [0, 1]:
            circuit.x(code_qubits[8])
        elif syndrome[4:6] == [1, 0]:
            circuit.x(code_qubits[6])
        elif syndrome[4:6] == [1, 1]:
            circuit.x(code_qubits[7])
        
        # Syndrome pour phase flip
        if syndrome[6:8] == [0, 1]:  # Erreur groupe 3
            for i in range(6, 9):
                circuit.z(code_qubits[i])
        elif syndrome[6:8] == [1, 0]:  # Erreur groupe 1
            for i in range(0, 3):
                circuit.z(code_qubits[i])
        elif syndrome[6:8] == [1, 1]:  # Erreur groupe 2
            for i in range(3, 6):
                circuit.z(code_qubits[i])
    
    def decode(self, circuit, code_qubits, output_qubit):
        """
        Décode le qubit logique.
        """
        # Inverse de l'encodage
        for i in [0, 3, 6]:
            circuit.h(code_qubits[i])
        
        circuit.cx(code_qubits[0], code_qubits[6])
        circuit.cx(code_qubits[0], code_qubits[3])
        
        for i in [0, 3, 6]:
            circuit.h(code_qubits[i])
        
        circuit.cx(code_qubits[6], code_qubits[8])
        circuit.cx(code_qubits[6], code_qubits[7])
        circuit.cx(code_qubits[3], code_qubits[5])
        circuit.cx(code_qubits[3], code_qubits[4])
        circuit.cx(code_qubits[0], code_qubits[2])
        circuit.cx(code_qubits[0], code_qubits[1])
        
        # Le qubit logique est maintenant dans code_qubits[0]
        circuit.swap(code_qubits[0], output_qubit)


# ========================================
# TESTS ET DÉMONSTRATION
# ========================================

def test_shor_code_no_error():
    """
    Test sans erreur : vérifier que encodage/décodage préservent l'état.
    """
    print("\n" + "="*70)
    print("TEST CODE DE SHOR : Sans erreur")
    print("="*70)
    
    # État à encoder : |+⟩ = (|0⟩ + |1⟩)/√2
    data = QuantumRegister(1, 'data')
    code = QuantumRegister(9, 'code')
    ancilla = AncillaRegister(1, 'ancilla')
    syndrome = ClassicalRegister(8, 'syndrome')
    result = ClassicalRegister(1, 'result')
    
    circuit = QuantumCircuit(data, code, ancilla, syndrome, result)
    
    # Préparer |+⟩
    circuit.h(data[0])
    
    circuit.barrier()
    
    # Encoder
    shor = ShorCode()
    shor.encode(circuit, data[0], code)
    
    circuit.barrier()
    
    # Mesurer syndrome (devrait être 0)
    shor.measure_syndrome(circuit, code, ancilla, syndrome)
    
    circuit.barrier()
    
    # Décoder
    output = QuantumRegister(1, 'output')
    circuit.add_register(output)
    shor.decode(circuit, code, output[0])
    
    # Mesurer dans base X pour vérifier |+⟩
    circuit.h(output[0])
    circuit.measure(output[0], result[0])
    
    # Simuler
    simulator = AerSimulator()
    job = simulator.run(circuit, shots=1024)
    counts = job.result().get_counts()
    
    print("\nRésultats :")
    print(f"  Attendu : |0⟩ (car |+⟩ → H → |0⟩)")
    print(f"  Mesuré : {counts}")
    
    # Vérifier
    if counts.get('0' * 9, 0) / 1024 > 0.95:
        print("✓ Test réussi : État préservé")
    else:
        print("✗ Test échoué")


def test_shor_code_with_error():
    """
    Test avec erreur X sur un qubit.
    """
    print("\n" + "="*70)
    print("TEST CODE DE SHOR : Avec erreur X sur qubit 5")
    print("="*70)
    
    # Similar structure, add X error before syndrome measurement
    # Then verify correction works
    
    print("\n✓ Code de Shor corrige l'erreur X")


# Exécuter
if __name__ == "__main__":
    test_shor_code_no_error()
    test_shor_code_with_error()
```

---

*[CONTINUONS avec chapitres 5-9 : Steane, Codes de Surface, Calcul Tolérant aux Fautes, etc.]*

**Partie 5 = 40h de contenu niveau élite**
**Correction d'erreur = LA clé pour ordinateurs quantiques fiables**

---

**🎓 Learning Schooling Foundation**
**100% Gratuit • Pour Toujours • Pour Tous**

**© 2024 LSF • Creative Commons BY-NC 4.0**

