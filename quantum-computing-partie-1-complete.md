# 📘 QUANTUM COMPUTING - PARTIE 1 : FONDEMENTS
## Du Bit au Qubit - Guide Complet avec Code Python

**Learning Schooling Foundation • Niveau Elite Mondial • 100% Gratuit**

---

## 🎯 INTRODUCTION

Bienvenue dans le monde fascinant du calcul quantique ! Ce guide te prend par la main depuis les concepts de base jusqu'à une compréhension profonde des qubits et de leur manipulation.

**Ce que tu vas apprendre :**
- Ce qu'est réellement un qubit et comment il diffère d'un bit classique
- La notation de Dirac (bra-ket) utilisée en mécanique quantique
- Comment visualiser les qubits sur la sphère de Bloch
- Les mathématiques derrière la superposition quantique
- Comment mesurer un état quantique et interpréter les résultats
- Implémenter tout ça en Python pour vraiment comprendre

**Prérequis :**
- Algèbre linéaire de base (vecteurs, matrices)
- Nombres complexes (niveau lycée suffit)
- Python 3.x avec numpy et matplotlib

**Durée estimée :** 30 heures de travail approfondi

**Tout le code est fourni, testé et prêt à l'emploi !** 🚀

---

## 📚 CHAPITRE 1.1 : LE QUBIT

### 1.1.1 Du Bit Classique au Qubit

#### Le bit classique

Un bit classique est l'unité fondamentale d'information en informatique traditionnelle.

**Caractéristiques :**
```
État : 0 OU 1 (jamais les deux simultanément)
Nature : Déterministe
Exemple physique : 
  - Tension électrique (5V = 1, 0V = 0)
  - Magnétisation (Nord = 1, Sud = 0)
  - État d'un transistor (conducteur/bloqué)
```

**Opérations possibles :**
- AND, OR, NOT, XOR
- Certaines réversibles (NOT), d'autres non (AND, OR)

#### Le qubit : la révolution quantique

Un **qubit** (quantum bit) est l'unité fondamentale du calcul quantique.

**Différences fondamentales :**

| Caractéristique | Bit Classique | Qubit |
|----------------|---------------|-------|
| États possibles | 0 OU 1 | 0 ET 1 (superposition) |
| Nature | Déterministe | Probabiliste |
| Information | 1 bit | Infinité de valeurs |
| Mesure | Lecture sans destruction | Collapse irréversible |
| Copie | Facile | Impossible (théorème de non-clonage) |

**Support physique d'un qubit :**
- **Photon** : polarisation horizontale/verticale
- **Électron** : spin up/down
- **Ion piégé** : niveaux d'énergie électronique
- **Circuit supraconducteur** : courant circulant dans deux directions

---

### 1.1.2 L'État Quantique - Notation Mathématique

#### La notation de Dirac (Bra-Ket)

En mécanique quantique, on utilise une notation spéciale inventée par Paul Dirac (Prix Nobel 1933).

**Le Ket |ψ⟩ (vecteur colonne) :**
```
|0⟩ = [1]    représente l'état "0"
      [0]

|1⟩ = [0]    représente l'état "1"
      [1]
```

**Le Bra ⟨ψ| (vecteur ligne, conjugué hermitien) :**
```
⟨0| = [1  0]    conjugué de |0⟩

⟨1| = [0  1]    conjugué de |1⟩
```

**Pourquoi cette notation ?**
- Compacte et élégante
- Facilite les calculs quantiques
- Standard universel en physique quantique
- Le "bra-c-ket" donne "bracket" (crochet) quand on fait le produit scalaire

#### Produit scalaire (Bracket)

Le produit scalaire de deux états se note ⟨φ|ψ⟩.

**Exemples de calculs :**

```
⟨0|0⟩ = [1  0] · [1] = 1×1 + 0×0 = 1
                 [0]

⟨0|1⟩ = [1  0] · [0] = 1×0 + 0×1 = 0
                 [1]

⟨1|1⟩ = [0  1] · [0] = 0×0 + 1×1 = 1
                 [1]
```

**Interprétation :**
- ⟨ψ|ψ⟩ = 1 : l'état est normalisé (norme = 1)
- ⟨φ|ψ⟩ = 0 : les états sont orthogonaux (perpendiculaires)
- |⟨φ|ψ⟩|² : probabilité de mesurer |ψ⟩ quand on est dans |φ⟩

#### Code Python : Vecteurs et Produits Scalaires

```python
import numpy as np

# États de base (kets)
ket_0 = np.array([1, 0], dtype=complex)
ket_1 = np.array([0, 1], dtype=complex)

print("="*60)
print("VECTEURS DE BASE")
print("="*60)
print(f"|0⟩ = {ket_0}")
print(f"|1⟩ = {ket_1}")

# Bras (conjugués hermitiens)
bra_0 = np.conj(ket_0)
bra_1 = np.conj(ket_1)

print(f"\n⟨0| = {bra_0}")
print(f"⟨1| = {bra_1}")

# Produits scalaires
print("\n" + "="*60)
print("PRODUITS SCALAIRES")
print("="*60)
print(f"⟨0|0⟩ = {np.vdot(ket_0, ket_0)}")  # vdot fait automatiquement le conjugué
print(f"⟨0|1⟩ = {np.vdot(ket_0, ket_1)}")
print(f"⟨1|0⟩ = {np.vdot(ket_1, ket_0)}")
print(f"⟨1|1⟩ = {np.vdot(ket_1, ket_1)}")

# Vérification d'orthonormalité
print("\n" + "="*60)
print("PROPRIÉTÉS")
print("="*60)
print(f"Les états |0⟩ et |1⟩ sont orthogonaux : ⟨0|1⟩ = {np.vdot(ket_0, ket_1)}")
print(f"Les états sont normalisés : ||0⟩| = {np.linalg.norm(ket_0)}, ||1⟩| = {np.linalg.norm(ket_1)}")
```

**Output attendu :**
```
============================================================
VECTEURS DE BASE
============================================================
|0⟩ = [1.+0.j 0.+0.j]
|1⟩ = [0.+0.j 1.+0.j]

⟨0| = [1.-0.j 0.-0.j]
⟨1| = [0.-0.j 1.-0.j]

============================================================
PRODUITS SCALAIRES
============================================================
⟨0|0⟩ = (1+0j)
⟨0|1⟩ = 0j
⟨1|0⟩ = 0j
⟨1|1⟩ = (1+0j)

============================================================
PROPRIÉTÉS
============================================================
Les états |0⟩ et |1⟩ sont orthogonaux : ⟨0|1⟩ = 0j
Les états sont normalisés : ||0⟩| = 1.0, ||1⟩| = 1.0
```

---

## 🌀 CHAPITRE 1.2 : SUPERPOSITION QUANTIQUE

### 1.2.1 L'État Général d'un Qubit

Un qubit peut exister dans une **superposition** des états |0⟩ et |1⟩ :

```
|ψ⟩ = α|0⟩ + β|1⟩
```

**Où :**
- `α` (alpha) = amplitude de probabilité pour l'état |0⟩
- `β` (beta) = amplitude de probabilité pour l'état |1⟩
- `α, β ∈ ℂ` (nombres complexes)

**Contrainte de normalisation :**
```
|α|² + |β|² = 1
```

Cette contrainte assure que les probabilités totales somment à 100%.

### 1.2.2 Représentation Matricielle

En notation matricielle :
```
|ψ⟩ = α|0⟩ + β|1⟩ = α[1] + β[0] = [α]
                       [0]    [1]   [β]
```

**Exemple concret :**
```
|ψ⟩ = (1/√2)|0⟩ + (1/√2)|1⟩ = [1/√2]   ← État |+⟩
                               [1/√2]
```

Vérification de normalisation :
```
|1/√2|² + |1/√2|² = 1/2 + 1/2 = 1 ✓
```

### 1.2.3 Interprétation Physique - ATTENTION !

**❌ IDÉES FAUSSES COURANTES :**

❌ **FAUX :** "Le qubit est 0 ET 1 en même temps"
✓ **VRAI :** "Le qubit existe dans une superposition d'états avec des amplitudes α et β"

❌ **FAUX :** "On peut lire α et β directement"
✓ **VRAI :** "On ne peut mesurer que |0⟩ ou |1⟩, avec des probabilités |α|² et |β|²"

❌ **FAUX :** "La superposition est juste une ignorance de l'état réel"
✓ **VRAI :** "La superposition est un état physique réel qui produit des interférences mesurables"

**Ce qui se passe vraiment :**

1. **Avant mesure :** Le qubit EST dans la superposition α|0⟩ + β|1⟩
2. **Pendant la mesure :** Interaction avec l'appareil → la superposition "collapse"
3. **Après mesure :** Le qubit est définitivement |0⟩ OU |1⟩

### 1.2.4 Code Python : Classe Qubit Complète

```python
import numpy as np
import matplotlib.pyplot as plt

class Qubit:
    """
    Représentation complète d'un qubit quantique.
    
    Un qubit est dans l'état |ψ⟩ = α|0⟩ + β|1⟩
    avec la contrainte |α|² + |β|² = 1
    """
    
    def __init__(self, alpha, beta):
        """
        Initialise un qubit dans l'état α|0⟩ + β|1⟩
        
        Args:
            alpha: amplitude pour |0⟩ (nombre complexe)
            beta: amplitude pour |1⟩ (nombre complexe)
        """
        # Conversion en nombres complexes
        alpha = complex(alpha)
        beta = complex(beta)
        
        # Normalisation automatique
        norm = np.sqrt(np.abs(alpha)**2 + np.abs(beta)**2)
        
        if norm == 0:
            raise ValueError("Les amplitudes ne peuvent pas être toutes deux nulles!")
        
        self.alpha = alpha / norm
        self.beta = beta / norm
        
        # Vecteur d'état
        self.state_vector = np.array([self.alpha, self.beta], dtype=complex)
        
    def probabilities(self):
        """
        Calcule les probabilités de mesure P(0) et P(1)
        selon la règle de Born : P(i) = |amplitude_i|²
        
        Returns:
            tuple: (P(0), P(1))
        """
        p0 = np.abs(self.alpha)**2
        p1 = np.abs(self.beta)**2
        return p0, p1
    
    def measure(self):
        """
        Effectue une mesure unique du qubit.
        La mesure provoque le collapse de l'état quantique !
        
        Returns:
            int: 0 ou 1
        """
        p0, p1 = self.probabilities()
        
        # Tirage aléatoire selon les probabilités
        result = 0 if np.random.random() < p0 else 1
        
        # COLLAPSE : le qubit devient |0⟩ ou |1⟩
        if result == 0:
            self.alpha = 1
            self.beta = 0
        else:
            self.alpha = 0
            self.beta = 1
            
        self.state_vector = np.array([self.alpha, self.beta], dtype=complex)
        
        return result
    
    def measure_many(self, n=1000):
        """
        Effectue n mesures (en recréant le qubit à chaque fois).
        Cela permet de vérifier statistiquement les probabilités quantiques.
        
        Args:
            n: nombre de mesures
            
        Returns:
            list: liste des résultats (0 ou 1)
        """
        # Sauvegarder l'état initial
        alpha_initial = self.alpha
        beta_initial = self.beta
        
        results = []
        for _ in range(n):
            # Recréer le qubit dans l'état initial
            self.alpha = alpha_initial
            self.beta = beta_initial
            self.state_vector = np.array([self.alpha, self.beta], dtype=complex)
            
            # Mesurer
            results.append(self.measure())
        
        return results
    
    def get_bloch_angles(self):
        """
        Calcule les angles θ (theta) et φ (phi) sur la sphère de Bloch.
        
        |ψ⟩ = cos(θ/2)|0⟩ + e^(iφ)sin(θ/2)|1⟩
        
        Returns:
            tuple: (theta, phi) en radians
        """
        # θ = 2 * arccos(|α|)
        theta = 2 * np.arccos(np.abs(self.alpha))
        
        # φ = arg(β) - arg(α)
        if np.abs(self.beta) > 1e-10:  # Éviter division par zéro
            phi = np.angle(self.beta) - np.angle(self.alpha)
        else:
            phi = 0
        
        return theta, phi
    
    def get_bloch_coordinates(self):
        """
        Calcule les coordonnées cartésiennes (x, y, z) sur la sphère de Bloch.
        
        Returns:
            tuple: (x, y, z)
        """
        theta, phi = self.get_bloch_angles()
        
        x = np.sin(theta) * np.cos(phi)
        y = np.sin(theta) * np.sin(phi)
        z = np.cos(theta)
        
        return x, y, z
    
    def __repr__(self):
        """Représentation textuelle du qubit"""
        # Formatage joli des nombres complexes
        def format_complex(c):
            if np.abs(c.imag) < 1e-10:
                return f"{c.real:.3f}"
            elif np.abs(c.real) < 1e-10:
                return f"{c.imag:.3f}i"
            else:
                sign = "+" if c.imag >= 0 else ""
                return f"{c.real:.3f}{sign}{c.imag:.3f}i"
        
        alpha_str = format_complex(self.alpha)
        beta_str = format_complex(self.beta)
        
        return f"|ψ⟩ = ({alpha_str})|0⟩ + ({beta_str})|1⟩"
    
    def __str__(self):
        """Version simplifiée pour print()"""
        return self.__repr__()


# ============================================================
# DÉMONSTRATIONS
# ============================================================

print("="*70)
print("CLASSE QUBIT - DÉMONSTRATIONS")
print("="*70)

# 1. État |0⟩
print("\n1. ÉTAT |0⟩")
print("-" * 70)
q0 = Qubit(1, 0)
print(f"État : {q0}")
p0, p1 = q0.probabilities()
print(f"Probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
theta, phi = q0.get_bloch_angles()
print(f"Angles Bloch : θ = {np.degrees(theta):.1f}°, φ = {np.degrees(phi):.1f}°")

# 2. État |1⟩
print("\n2. ÉTAT |1⟩")
print("-" * 70)
q1 = Qubit(0, 1)
print(f"État : {q1}")
p0, p1 = q1.probabilities()
print(f"Probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
theta, phi = q1.get_bloch_angles()
print(f"Angles Bloch : θ = {np.degrees(theta):.1f}°, φ = {np.degrees(phi):.1f}°")

# 3. État |+⟩ = (|0⟩ + |1⟩)/√2
print("\n3. ÉTAT |+⟩ = (|0⟩ + |1⟩)/√2")
print("-" * 70)
q_plus = Qubit(1/np.sqrt(2), 1/np.sqrt(2))
print(f"État : {q_plus}")
p0, p1 = q_plus.probabilities()
print(f"Probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
theta, phi = q_plus.get_bloch_angles()
print(f"Angles Bloch : θ = {np.degrees(theta):.1f}°, φ = {np.degrees(phi):.1f}°")

# 4. État avec phase : (|0⟩ + i|1⟩)/√2
print("\n4. ÉTAT AVEC PHASE : (|0⟩ + i|1⟩)/√2")
print("-" * 70)
q_phase = Qubit(1/np.sqrt(2), 1j/np.sqrt(2))
print(f"État : {q_phase}")
p0, p1 = q_phase.probabilities()
print(f"Probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
theta, phi = q_phase.get_bloch_angles()
print(f"Angles Bloch : θ = {np.degrees(theta):.1f}°, φ = {np.degrees(phi):.1f}°")

# 5. État asymétrique : (√3/2)|0⟩ + (1/2)|1⟩
print("\n5. ÉTAT ASYMÉTRIQUE : (√3/2)|0⟩ + (1/2)|1⟩")
print("-" * 70)
q_asym = Qubit(np.sqrt(3)/2, 1/2)
print(f"État : {q_asym}")
p0, p1 = q_asym.probabilities()
print(f"Probabilités : P(0) = {p0:.3f} (75%), P(1) = {p1:.3f} (25%)")
theta, phi = q_asym.get_bloch_angles()
print(f"Angles Bloch : θ = {np.degrees(theta):.1f}°, φ = {np.degrees(phi):.1f}°")

print("\n" + "="*70)
```

---

## 📊 CHAPITRE 1.3 : PROBABILITÉS ET MESURE

### 1.3.1 La Règle de Born

Lors de la mesure d'un qubit |ψ⟩ = α|0⟩ + β|1⟩ :

```
P(mesurer |0⟩) = |α|² = α* · α
P(mesurer |1⟩) = |β|² = β* · β
```

où α* désigne le conjugué complexe de α.

**Pour les nombres complexes :**
```
Si α = a + bi, alors α* = a - bi
Et |α|² = α* · α = (a - bi)(a + bi) = a² + b²
```

**Max Born** (Prix Nobel 1954) a découvert cette interprétation probabiliste de la mécanique quantique.

### 1.3.2 Exemples de Calculs

**Exemple 1 : État |+⟩**
```
|+⟩ = (1/√2)|0⟩ + (1/√2)|1⟩

P(0) = |1/√2|² = 1/2 = 50%
P(1) = |1/√2|² = 1/2 = 50%
```

**Exemple 2 : État avec phase**
```
|ψ⟩ = (1/√2)|0⟩ + (i/√2)|1⟩

P(0) = |1/√2|² = 1/2 = 50%
P(1) = |i/√2|² = |i|²/2 = 1/2 = 50%

Note : |i|² = i* · i = (-i) · i = 1
```

**Exemple 3 : État asymétrique**
```
|ψ⟩ = (√3/2)|0⟩ + (1/2)|1⟩

P(0) = |√3/2|² = 3/4 = 75%
P(1) = |1/2|² = 1/4 = 25%

Vérification : 3/4 + 1/4 = 1 ✓
```

### 1.3.3 Code : Simulation de Mesures et Convergence Statistique

```python
def test_quantum_measurement(alpha, beta, n_measurements=10000, label=""):
    """
    Teste la convergence des mesures quantiques vers les probabilités théoriques.
    
    Args:
        alpha, beta: amplitudes du qubit
        n_measurements: nombre de mesures à effectuer
        label: nom de l'état pour l'affichage
    """
    print("="*70)
    print(f"TEST DE MESURE : {label}")
    print("="*70)
    
    # Créer le qubit
    q = Qubit(alpha, beta)
    print(f"\nÉtat : {q}")
    
    # Probabilités théoriques
    p0_theory, p1_theory = q.probabilities()
    print(f"\nProbabilités théoriques :")
    print(f"  P(0) = {p0_theory:.6f} = {p0_theory*100:.2f}%")
    print(f"  P(1) = {p1_theory:.6f} = {p1_theory*100:.2f}%")
    
    # Effectuer les mesures
    results = q.measure_many(n_measurements)
    
    # Calculer les probabilités mesurées
    count_0 = results.count(0)
    count_1 = results.count(1)
    p0_measured = count_0 / n_measurements
    p1_measured = count_1 / n_measurements
    
    print(f"\nRésultats après {n_measurements} mesures :")
    print(f"  P(0) mesuré = {p0_measured:.6f} = {p0_measured*100:.2f}%")
    print(f"  P(1) mesuré = {p1_measured:.6f} = {p1_measured*100:.2f}%")
    
    # Calculer l'écart
    error_0 = abs(p0_measured - p0_theory)
    error_1 = abs(p1_measured - p1_theory)
    
    print(f"\nÉcart avec la théorie :")
    print(f"  Δ P(0) = {error_0:.6f}")
    print(f"  Δ P(1) = {error_1:.6f}")
    
    # Vérification statistique (loi des grands nombres)
    # L'écart devrait être O(1/√n)
    expected_std = 1 / np.sqrt(n_measurements)
    print(f"\nÉcart théorique attendu : ~{expected_std:.6f}")
    print(f"✓ Convergence OK" if error_0 < 3*expected_std else "✗ Problème de convergence")
    
    return results, p0_measured, p1_measured


# Tests sur différents états
print("\n\n")
test_quantum_measurement(1, 0, 10000, "État |0⟩")

print("\n\n")
test_quantum_measurement(1/np.sqrt(2), 1/np.sqrt(2), 10000, "État |+⟩")

print("\n\n")
test_quantum_measurement(np.sqrt(3)/2, 1/2, 10000, "État asymétrique (√3/2)|0⟩ + (1/2)|1⟩")

print("\n\n")
test_quantum_measurement(1/np.sqrt(2), 1j/np.sqrt(2), 10000, "État avec phase (|0⟩ + i|1⟩)/√2")
```

### 1.3.4 Visualisation : Convergence vers la Théorie

```python
def visualize_convergence(alpha, beta, max_measurements=5000, title=""):
    """
    Visualise comment les probabilités mesurées convergent
    vers les probabilités théoriques au fur et à mesure des mesures.
    
    Démontre la loi des grands nombres en action !
    """
    qubit = Qubit(alpha, beta)
    p0_theory, p1_theory = qubit.probabilities()
    
    # Effectuer les mesures une par une
    measurements = []
    running_p0 = []
    running_p1 = []
    
    for i in range(1, max_measurements + 1):
        # Recréer le qubit et mesurer
        q = Qubit(alpha, beta)
        result = q.measure()
        measurements.append(result)
        
        # Calculer les probabilités empiriques cumulatives
        current_p0 = measurements.count(0) / i
        current_p1 = measurements.count(1) / i
        running_p0.append(current_p0)
        running_p1.append(current_p1)
    
    # Créer le graphique
    plt.figure(figsize=(14, 6))
    
    # Subplot 1 : P(0)
    plt.subplot(1, 2, 1)
    plt.plot(range(1, max_measurements + 1), running_p0, 
             label='P(0) mesuré', alpha=0.7, linewidth=1, color='blue')
    plt.axhline(y=p0_theory, color='red', linestyle='--', 
                linewidth=2, label=f'P(0) théorique = {p0_theory:.4f}')
    plt.xlabel('Nombre de mesures', fontsize=12)
    plt.ylabel('Probabilité P(0)', fontsize=12)
    plt.title('Convergence de P(0)', fontsize=14, fontweight='bold')
    plt.legend(fontsize=10)
    plt.grid(True, alpha=0.3)
    plt.ylim([0, 1])
    
    # Subplot 2 : P(1)
    plt.subplot(1, 2, 2)
    plt.plot(range(1, max_measurements + 1), running_p1, 
             label='P(1) mesuré', alpha=0.7, linewidth=1, color='green')
    plt.axhline(y=p1_theory, color='red', linestyle='--', 
                linewidth=2, label=f'P(1) théorique = {p1_theory:.4f}')
    plt.xlabel('Nombre de mesures', fontsize=12)
    plt.ylabel('Probabilité P(1)', fontsize=12)
    plt.title('Convergence de P(1)', fontsize=14, fontweight='bold')
    plt.legend(fontsize=10)
    plt.grid(True, alpha=0.3)
    plt.ylim([0, 1])
    
    plt.suptitle(f'Convergence Statistique - {title}\n{qubit}', 
                 fontsize=16, fontweight='bold')
    plt.tight_layout()
    plt.show()
    
    # Statistiques finales
    print(f"\n{'='*70}")
    print(f"CONVERGENCE FINALE après {max_measurements} mesures")
    print(f"{'='*70}")
    print(f"P(0) : théorique = {p0_theory:.6f}, mesuré = {running_p0[-1]:.6f}, écart = {abs(running_p0[-1] - p0_theory):.6f}")
    print(f"P(1) : théorique = {p1_theory:.6f}, mesuré = {running_p1[-1]:.6f}, écart = {abs(running_p1[-1] - p1_theory):.6f}")


# Test avec l'état |+⟩
visualize_convergence(1/np.sqrt(2), 1/np.sqrt(2), 5000, "État |+⟩")

# Test avec un état asymétrique
visualize_convergence(np.sqrt(3)/2, 1/2, 5000, "État (√3/2)|0⟩ + (1/2)|1⟩")
```

---

## 🌐 CHAPITRE 1.4 : LA SPHÈRE DE BLOCH

### 1.4.1 Représentation Géométrique

Tout état d'un qubit peut être représenté comme un point sur une **sphère de rayon 1** appelée **sphère de Bloch**.

**Formule générale :**
```
|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ)sin(θ/2)|1⟩
```

**Paramètres :**
- `θ` (thêta) : **angle polaire**, 0 ≤ θ ≤ π (latitude)
- `φ` (phi) : **angle azimutal**, 0 ≤ φ ≤ 2π (longitude)

**Coordonnées cartésiennes :**
```
x = sin(θ)cos(φ)
y = sin(θ)sin(φ)
z = cos(θ)
```

**Pourquoi une sphère ?**
- Les 2 nombres complexes (α, β) donnent 4 paramètres réels
- La normalisation |α|² + |β|² = 1 retire 1 degré de liberté
- La phase globale (non observable) retire encore 1 degré de liberté
- Reste 2 paramètres : θ et φ → surface d'une sphère !

### 1.4.2 États Remarquables

**Pôles :**
```
Pôle Nord (θ=0) :       |0⟩
Pôle Sud (θ=π) :        |1⟩
```

**Équateur (θ=π/2) :**
```
φ = 0 :       |+⟩ = (|0⟩ + |1⟩)/√2
φ = π :       |−⟩ = (|0⟩ − |1⟩)/√2
φ = π/2 :     |i+⟩ = (|0⟩ + i|1⟩)/√2
φ = 3π/2 :    |i−⟩ = (|0⟩ − i|1⟩)/√2
```

**Propriété fondamentale :**
États diamétralement opposés sur la sphère = états **orthogonaux**
```
⟨0|1⟩ = 0
⟨+|−⟩ = 0
⟨i+|i−⟩ = 0
```

### 1.4.3 Code : Sphère de Bloch Interactive

```python
from mpl_toolkits.mplot3d import Axes3D

class BlochSphere:
    """
    Visualisation de la sphère de Bloch avec capacité d'ajouter
    plusieurs états quantiques.
    """
    
    def __init__(self, figsize=(12, 10)):
        self.fig = plt.figure(figsize=figsize)
        self.ax = self.fig.add_subplot(111, projection='3d')
        self.states = []
        
    def draw_sphere(self):
        """Dessine la sphère de Bloch avec ses axes et labels"""
        # Génération de la sphère
        u = np.linspace(0, 2 * np.pi, 100)
        v = np.linspace(0, np.pi, 100)
        x = np.outer(np.cos(u), np.sin(v))
        y = np.outer(np.sin(u), np.sin(v))
        z = np.outer(np.ones(np.size(u)), np.cos(v))
        
        # Sphère translucide
        self.ax.plot_surface(x, y, z, alpha=0.1, color='lightblue')
        
        # Axes principaux (X, Y, Z)
        axis_length = 1.3
        
        # Axe Z (vertical)
        self.ax.plot([0, 0], [0, 0], [-axis_length, axis_length], 
                     'k-', linewidth=2)
        
        # Axe X
        self.ax.plot([-axis_length, axis_length], [0, 0], [0, 0], 
                     'k-', linewidth=1.5, alpha=0.6)
        
        # Axe Y
        self.ax.plot([0, 0], [-axis_length, axis_length], [0, 0], 
                     'k-', linewidth=1.5, alpha=0.6)
        
        # Labels des états de base
        self.ax.text(0, 0, 1.4, '|0⟩', fontsize=18, weight='bold', 
                     ha='center', color='blue')
        self.ax.text(0, 0, -1.4, '|1⟩', fontsize=18, weight='bold', 
                     ha='center', color='red')
        self.ax.text(1.4, 0, 0, '|+⟩', fontsize=14, ha='center', color='green')
        self.ax.text(-1.4, 0, 0, '|−⟩', fontsize=14, ha='center', color='orange')
        self.ax.text(0, 1.4, 0, '|i+⟩', fontsize=14, ha='center', color='purple')
        self.ax.text(0, -1.4, 0, '|i−⟩', fontsize=14, ha='center', color='brown')
        
        # Équateur (cercle à z=0)
        theta_eq = np.linspace(0, 2*np.pi, 100)
        self.ax.plot(np.cos(theta_eq), np.sin(theta_eq), 0, 
                     'k--', alpha=0.3, linewidth=1)
        
        # Méridiens
        for angle in [0, np.pi/2, np.pi, 3*np.pi/2]:
            phi_circle = np.linspace(0, np.pi, 50)
            x_circle = np.sin(phi_circle) * np.cos(angle)
            y_circle = np.sin(phi_circle) * np.sin(angle)
            z_circle = np.cos(phi_circle)
            self.ax.plot(x_circle, y_circle, z_circle, 'k--', alpha=0.2, linewidth=0.5)
        
    def add_state_from_qubit(self, qubit, label=None, color='purple'):
        """
        Ajoute un état quantique à la sphère à partir d'un objet Qubit
        
        Args:
            qubit: objet Qubit
            label: nom de l'état (optionnel)
            color: couleur de la flèche
        """
        if label is None:
            label = str(qubit)
        
        # Coordonnées sur la sphère
        x, y, z = qubit.get_bloch_coordinates()
        
        # Vecteur d'état (flèche depuis l'origine)
        self.ax.quiver(0, 0, 0, x, y, z, 
                       color=color, arrow_length_ratio=0.15, 
                       linewidth=2.5, alpha=0.8)
        
        # Point sur la sphère
        self.ax.scatter([x], [y], [z], color=color, s=150, 
                        edgecolors='black', linewidths=2, zorder=10)
        
        # Label
        self.ax.text(x*1.15, y*1.15, z*1.15, label, 
                     fontsize=11, weight='bold', color=color)
        
        # Sauvegarder l'info
        self.states.append({
            'qubit': qubit,
            'label': label,
            'color': color,
            'coords': (x, y, z)
        })
        
    def add_state_from_amplitudes(self, alpha, beta, label='|ψ⟩', color='purple'):
        """
        Ajoute un état à partir de ses amplitudes
        
        Args:
            alpha, beta: amplitudes
            label: nom
            color: couleur
        """
        qubit = Qubit(alpha, beta)
        self.add_state_from_qubit(qubit, label, color)
        
    def show(self, title='Sphère de Bloch', elevation=20, azimuth=45):
        """
        Affiche la sphère avec les états ajoutés
        
        Args:
            title: titre du graphique
            elevation: angle de vue vertical
            azimuth: angle de vue horizontal
        """
        self.ax.set_xlim([-1.5, 1.5])
        self.ax.set_ylim([-1.5, 1.5])
        self.ax.set_zlim([-1.5, 1.5])
        self.ax.set_xlabel('X', fontsize=12, fontweight='bold')
        self.ax.set_ylabel('Y', fontsize=12, fontweight='bold')
        self.ax.set_zlabel('Z', fontsize=12, fontweight='bold')
        self.ax.set_box_aspect([1,1,1])
        
        # Angle de vue
        self.ax.view_init(elev=elevation, azim=azimuth)
        
        plt.title(title, fontsize=16, weight='bold', pad=20)
        plt.tight_layout()
        plt.show()
        
    def print_states_info(self):
        """Affiche les informations détaillées sur tous les états"""
        print("\n" + "="*70)
        print("ÉTATS QUANTIQUES SUR LA SPHÈRE DE BLOCH")
        print("="*70)
        
        for i, state in enumerate(self.states, 1):
            qubit = state['qubit']
            print(f"\n{i}. {state['label']}")
            print(f"   État complet : {qubit}")
            
            # Amplitudes
            print(f"   Amplitudes : α = {qubit.alpha:.4f}, β = {qubit.beta:.4f}")
            
            # Angles Bloch
            theta, phi = qubit.get_bloch_angles()
            print(f"   Angles Bloch : θ = {np.degrees(theta):.2f}°, φ = {np.degrees(phi):.2f}°")
            
            # Coordonnées
            x, y, z = state['coords']
            print(f"   Coordonnées : ({x:.4f}, {y:.4f}, {z:.4f})")
            
            # Probabilités
            p0, p1 = qubit.probabilities()
            print(f"   Probabilités : P(0) = {p0:.4f}, P(1) = {p1:.4f}")


# ============================================================
# DÉMONSTRATION : Sphère de Bloch avec États Classiques
# ============================================================

print("\n" + "="*70)
print("VISUALISATION : Sphère de Bloch avec États Remarquables")
print("="*70)

sphere = BlochSphere(figsize=(14, 12))
sphere.draw_sphere()

# États de base (pôles)
sphere.add_state_from_amplitudes(1, 0, '|0⟩', 'blue')
sphere.add_state_from_amplitudes(0, 1, '|1⟩', 'red')

# États de superposition (équateur)
sphere.add_state_from_amplitudes(1/np.sqrt(2), 1/np.sqrt(2), '|+⟩', 'green')
sphere.add_state_from_amplitudes(1/np.sqrt(2), -1/np.sqrt(2), '|−⟩', 'orange')
sphere.add_state_from_amplitudes(1/np.sqrt(2), 1j/np.sqrt(2), '|i+⟩', 'purple')
sphere.add_state_from_amplitudes(1/np.sqrt(2), -1j/np.sqrt(2), '|i−⟩', 'brown')

# Un état quelconque
sphere.add_state_from_amplitudes(np.sqrt(3)/2, 1/2, '|ψ⟩', 'magenta')

sphere.show(title='États Quantiques Remarquables sur la Sphère de Bloch')
sphere.print_states_info()
```

### 1.4.4 Vérification : États Orthogonaux

```python
def check_orthogonality(alpha1, beta1, alpha2, beta2, label1, label2):
    """
    Vérifie si deux états sont orthogonaux
    """
    q1 = Qubit(alpha1, beta1)
    q2 = Qubit(alpha2, beta2)
    
    # Produit scalaire ⟨ψ1|ψ2⟩
    inner_product = np.vdot(q1.state_vector, q2.state_vector)
    
    print(f"\n{label1} et {label2} :")
    print(f"  ⟨{label1}|{label2}⟩ = {inner_product:.6f}")
    
    if np.abs(inner_product) < 1e-10:
        print(f"  ✓ États ORTHOGONAUX")
        
        # Vérifier s'ils sont diamétralement opposés sur la sphère
        x1, y1, z1 = q1.get_bloch_coordinates()
        x2, y2, z2 = q2.get_bloch_coordinates()
        
        # Vecteurs opposés si v2 = -v1
        if np.allclose([x2, y2, z2], [-x1, -y1, -z1], atol=1e-6):
            print(f"  ✓ Diamétralement OPPOSÉS sur la sphère de Bloch")
    else:
        print(f"  ✗ États NON orthogonaux")


print("="*70)
print("VÉRIFICATION : Orthogonalité des États")
print("="*70)

# |0⟩ et |1⟩
check_orthogonality(1, 0, 0, 1, "|0⟩", "|1⟩")

# |+⟩ et |−⟩
check_orthogonality(1/np.sqrt(2), 1/np.sqrt(2), 
                   1/np.sqrt(2), -1/np.sqrt(2), "|+⟩", "|−⟩")

# |i+⟩ et |i−⟩
check_orthogonality(1/np.sqrt(2), 1j/np.sqrt(2), 
                   1/np.sqrt(2), -1j/np.sqrt(2), "|i+⟩", "|i−⟩")

# |0⟩ et |+⟩ (NON orthogonaux)
check_orthogonality(1, 0, 1/np.sqrt(2), 1/np.sqrt(2), "|0⟩", "|+⟩")

print("\n" + "="*70)
```

---

## 🎭 CHAPITRE 1.5 : PHASE GLOBALE VS PHASE RELATIVE

### 1.5.1 Phase Globale (Non Observable)

**Définition :**
Multiplier tout l'état par un facteur de phase e^(iγ) ne change PAS l'état physique.

```
|ψ⟩ = α|0⟩ + β|1⟩
e^(iγ)|ψ⟩ = e^(iγ)α|0⟩ + e^(iγ)β|1⟩
```

**Ces deux états sont physiquement IDENTIQUES.**

**Preuve :**
```
P(0) pour |ψ⟩ = |α|²
P(0) pour e^(iγ)|ψ⟩ = |e^(iγ)α|² = |e^(iγ)|² |α|² = 1 × |α|² = |α|²
```

La phase globale disparaît dans toutes les mesures car |e^(iγ)|² = 1 !

**Sur la sphère de Bloch :**
Une phase globale ne change PAS la position du point sur la sphère.

### 1.5.2 Phase Relative (Observable !)

**Définition :**
La différence de phase ENTRE α et β EST observable et change l'état physique.

**Exemple crucial :**
```
|+⟩ = (|0⟩ + |1⟩)/√2       (phase relative = 0)
|−⟩ = (|0⟩ − |1⟩)/√2       (phase relative = π)
```

**Ces états sont DIFFÉRENTS !**

**Dans la base {|0⟩, |1⟩} :**
- Même probabilités (50/50)

**Dans la base {|+⟩, |−⟩} :**
- |+⟩ mesuré dans base {|+⟩, |−⟩} → 100% chance de |+⟩
- |−⟩ mesuré dans base {|+⟩, |−⟩} → 100% chance de |−⟩

**Sur la sphère de Bloch :**
La phase relative change la position sur l'équateur (angle φ).

### 1.5.3 Code : Démonstration de la Phase Relative

```python
def measure_in_basis(state_vector, basis):
    """
    Mesure un état dans une base donnée
    
    Args:
        state_vector: vecteur d'état [α, β]
        basis: dictionnaire {'label': vecteur_base}
    
    Returns:
        dict: probabilités pour chaque état de base
    """
    probabilities = {}
    
    for label, basis_state in basis.items():
        # Produit scalaire ⟨basis_state|state_vector⟩
        amplitude = np.vdot(basis_state, state_vector)
        prob = np.abs(amplitude)**2
        probabilities[label] = prob
        
    return probabilities


def demonstrate_phase_effect():
    """
    Démontre que la phase relative est observable en changeant de base
    """
    print("="*70)
    print("DÉMONSTRATION : Phase Relative Observable")
    print("="*70)
    
    # Définir les états
    state_plus = np.array([1, 1]) / np.sqrt(2)   # |+⟩
    state_minus = np.array([1, -1]) / np.sqrt(2)  # |−⟩
    
    # Base computationnelle {|0⟩, |1⟩}
    computational_basis = {
        '|0⟩': np.array([1, 0], dtype=complex),
        '|1⟩': np.array([0, 1], dtype=complex)
    }
    
    # Base de Hadamard {|+⟩, |−⟩}
    hadamard_basis = {
        '|+⟩': np.array([1, 1], dtype=complex) / np.sqrt(2),
        '|−⟩': np.array([1, -1], dtype=complex) / np.sqrt(2)
    }
    
    # Test 1 : |+⟩
    print("\n1. État |+⟩ = (|0⟩ + |1⟩)/√2")
    print("-" * 70)
    
    print("\n   Mesure dans base {|0⟩, |1⟩} :")
    probs = measure_in_basis(state_plus, computational_basis)
    for label, prob in probs.items():
        print(f"      P({label}) = {prob:.4f} = {prob*100:.1f}%")
    
    print("\n   Mesure dans base {|+⟩, |−⟩} :")
    probs = measure_in_basis(state_plus, hadamard_basis)
    for label, prob in probs.items():
        print(f"      P({label}) = {prob:.4f} = {prob*100:.1f}%")
    
    # Test 2 : |−⟩
    print("\n2. État |−⟩ = (|0⟩ − |1⟩)/√2")
    print("-" * 70)
    
    print("\n   Mesure dans base {|0⟩, |1⟩} :")
    probs = measure_in_basis(state_minus, computational_basis)
    for label, prob in probs.items():
        print(f"      P({label}) = {prob:.4f} = {prob*100:.1f}%")
    
    print("\n   Mesure dans base {|+⟩, |−⟩} :")
    probs = measure_in_basis(state_minus, hadamard_basis)
    for label, prob in probs.items():
        print(f"      P({label}) = {prob:.4f} = {prob*100:.1f}%")
    
    # Conclusion
    print("\n" + "="*70)
    print("CONCLUSION :")
    print("="*70)
    print("✓ Dans la base {|0⟩, |1⟩} : |+⟩ et |−⟩ donnent les mêmes probabilités")
    print("✓ Dans la base {|+⟩, |−⟩} : résultats complètement différents !")
    print("✓ La phase relative EST observable en changeant de base de mesure")
    print("="*70)


# Exécuter la démonstration
demonstrate_phase_effect()


# Visualisation sur la sphère de Bloch
print("\n\n")
print("="*70)
print("VISUALISATION : |+⟩ et |−⟩ sur la Sphère de Bloch")
print("="*70)

sphere2 = BlochSphere(figsize=(12, 10))
sphere2.draw_sphere()

sphere2.add_state_from_amplitudes(1/np.sqrt(2), 1/np.sqrt(2), '|+⟩', 'green')
sphere2.add_state_from_amplitudes(1/np.sqrt(2), -1/np.sqrt(2), '|−⟩', 'orange')

sphere2.show(title='Phase Relative : |+⟩ vs |−⟩')
sphere2.print_states_info()

print("\nNote : |+⟩ et |−⟩ sont sur l'équateur mais à φ différents (0 et π)")
print("Cette différence de phase est OBSERVABLE !")
```

---

## 💥 CHAPITRE 1.6 : LE COLLAPSE DE LA MESURE

### 1.6.1 Postulat de Mesure de Von Neumann

**Avant mesure :**
Le qubit existe dans une superposition
```
|ψ⟩ = α|0⟩ + β|1⟩
```

**Pendant la mesure :**
- Le système interagit avec l'appareil de mesure
- Corrélation quantique créée (intrication avec l'environnement)
- Processus irréversible et instantané

**Résultat de la mesure :**
- Avec probabilité |α|² → on mesure 0
- Avec probabilité |β|² → on mesure 1

**Après mesure :**
Le qubit n'est PLUS en superposition !
```
Si on a mesuré 0 : |ψ⟩ → |0⟩
Si on a mesuré 1 : |ψ⟩ → |1⟩
```

### 1.6.2 Propriétés du Collapse

**1. Irréversibilité**
On ne peut pas "dé-mesurer" un qubit. L'information sur α et β est perdue.

**2. Perte d'information**
Avant : état quantique avec infinité de valeurs (α, β)
Après : 1 bit classique (0 ou 1)

**3. Théorème de non-clonage**
Impossible de copier un état quantique inconnu (Wootters & Zurek, 1982)
→ Conséquence directe du collapse !

**4. Mesures répétées**
Si on mesure deux fois de suite dans la même base → même résultat
```
Mesure 1 : |ψ⟩ → |0⟩
Mesure 2 : |0⟩ → |0⟩  (résultat certain, probabilité 100%)
```

### 1.6.3 Code : Simulation du Collapse

```python
class QuantumMeasurement:
    """
    Classe pour démontrer le collapse quantique et ses propriétés.
    """
    
    def __init__(self, alpha, beta):
        """
        Initialise un système de mesure quantique
        """
        # Normalisation
        norm = np.sqrt(np.abs(alpha)**2 + np.abs(beta)**2)
        
        # État initial (avant toute mesure)
        self.initial_alpha = alpha / norm
        self.initial_beta = beta / norm
        
        # État actuel (peut changer après mesure)
        self.current_alpha = self.initial_alpha
        self.current_beta = self.initial_beta
        
        # Historique
        self.measured = False
        self.measurement_result = None
        self.measurement_count = 0
        
    def get_state(self):
        """Retourne l'état actuel sous forme de string"""
        def format_complex(c):
            if np.abs(c.imag) < 1e-10:
                return f"{c.real:.3f}"
            elif np.abs(c.real) < 1e-10:
                return f"{c.imag:.3f}i"
            else:
                sign = "+" if c.imag >= 0 else ""
                return f"{c.real:.3f}{sign}{c.imag:.3f}i"
        
        alpha_str = format_complex(self.current_alpha)
        beta_str = format_complex(self.current_beta)
        
        return f"({alpha_str})|0⟩ + ({beta_str})|1⟩"
    
    def probabilities(self):
        """Probabilités de mesure de l'état actuel"""
        p0 = np.abs(self.current_alpha)**2
        p1 = np.abs(self.current_beta)**2
        return p0, p1
    
    def measure(self):
        """
        Effectue une mesure et provoque le collapse !
        
        Returns:
            int: 0 ou 1
        """
        p0, p1 = self.probabilities()
        
        # Tirage aléatoire selon les probabilités
        result = 0 if np.random.random() < p0 else 1
        
        # 💥 COLLAPSE ! 💥
        if result == 0:
            self.current_alpha = 1
            self.current_beta = 0
        else:
            self.current_alpha = 0
            self.current_beta = 1
        
        # Mettre à jour l'historique
        self.measured = True
        self.measurement_result = result
        self.measurement_count += 1
        
        return result
    
    def reset(self):
        """Réinitialise à l'état initial (simule un nouveau qubit)"""
        self.current_alpha = self.initial_alpha
        self.current_beta = self.initial_beta
        self.measured = False
        self.measurement_result = None
        self.measurement_count = 0


def demonstrate_collapse():
    """
    Démontre le collapse quantique avec mesures répétées
    """
    print("="*70)
    print("DÉMONSTRATION : COLLAPSE QUANTIQUE")
    print("="*70)
    
    # Créer un état en superposition
    qm = QuantumMeasurement(1/np.sqrt(2), 1/np.sqrt(2))
    
    print(f"\nÉtat initial : |ψ⟩ = {qm.get_state()}")
    p0, p1 = qm.probabilities()
    print(f"Probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
    print("\n" + "→"*35)
    
    # Première mesure
    print("\n📊 PREMIÈRE MESURE")
    print("-" * 70)
    result1 = qm.measure()
    print(f"Résultat mesuré : {result1}")
    print(f"État après collapse : |ψ⟩ = {qm.get_state()}")
    p0, p1 = qm.probabilities()
    print(f"Nouvelles probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
    
    # Deuxième mesure (sans réinitialisation)
    print("\n📊 DEUXIÈME MESURE (même qubit, sans réinitialisation)")
    print("-" * 70)
    result2 = qm.measure()
    print(f"Résultat mesuré : {result2}")
    print(f"État après mesure : |ψ⟩ = {qm.get_state()}")
    
    if result1 == result2:
        print("✓ Le résultat est IDENTIQUE à la première mesure !")
        print("✓ Une fois collapsed, l'état reste dans |0⟩ ou |1⟩")
    
    # Troisième mesure
    print("\n📊 TROISIÈME MESURE (toujours le même qubit)")
    print("-" * 70)
    result3 = qm.measure()
    print(f"Résultat mesuré : {result3}")
    print(f"Résultats des 3 mesures : {result1}, {result2}, {result3}")
    print("✓ Toutes les mesures donnent le même résultat après le collapse !")
    
    # Réinitialisation et nouvelle mesure
    print("\n" + "→"*35)
    print("\n🔄 RÉINITIALISATION (nouveau qubit)")
    print("-" * 70)
    qm.reset()
    print(f"État réinitialisé : |ψ⟩ = {qm.get_state()}")
    p0, p1 = qm.probabilities()
    print(f"Probabilités : P(0) = {p0:.3f}, P(1) = {p1:.3f}")
    
    print("\n📊 QUATRIÈME MESURE (nouveau qubit)")
    print("-" * 70)
    result4 = qm.measure()
    print(f"Résultat mesuré : {result4}")
    print(f"Cette fois le résultat PEUT être différent : {result4}")
    
    if result4 != result1:
        print("✓ Résultat différent ! La probabilité quantique est de retour.")
    else:
        print("✓ Par hasard, même résultat (probabilité 50%)")
    
    print("\n" + "="*70)
    print("RÉSUMÉ DU COLLAPSE :")
    print("="*70)
    print("1. Avant mesure : superposition α|0⟩ + β|1⟩")
    print("2. Mesure : collapse vers |0⟩ ou |1⟩ selon probabilités")
    print("3. Après mesure : état définitif, mesures répétées donnent même résultat")
    print("4. Nouveau qubit : nécessaire pour retrouver les probabilités quantiques")
    print("="*70)


# Exécuter la démonstration
demonstrate_collapse()


# Expérience statistique : vérifier que mesures répétées donnent toujours le même résultat
print("\n\n")
print("="*70)
print("EXPÉRIENCE : Mesures Répétées Après Collapse")
print("="*70)

qm2 = QuantumMeasurement(np.sqrt(3)/2, 1/2)
print(f"\nÉtat : |ψ⟩ = {qm2.get_state()}")

# Première mesure
first_result = qm2.measure()
print(f"\nPremière mesure : {first_result}")

# 10 mesures supplémentaires sans réinitialiser
print(f"\n10 mesures successives (même qubit) :")
all_same = True
for i in range(10):
    result = qm2.measure()
    print(f"  Mesure {i+2} : {result}")
    if result != first_result:
        all_same = False

if all_same:
    print(f"\n✓ Toutes les mesures donnent {first_result} !")
    print("✓ Le collapse est irréversible")
else:
    print("\n✗ Erreur dans le code ! (ne devrait jamais arriver)")

print("="*70)
```

---

## 🎯 EXERCICES PRATIQUES

### Exercice 1.1 : Manipulation d'États

**Objectif :** Maîtriser la représentation et l'analyse des qubits

**Énoncé :**
Pour chacun des états suivants :
1. Crée le qubit en Python
2. Affiche sa représentation
3. Vérifie la normalisation
4. Calcule et affiche P(0) et P(1)
5. Calcule les angles θ et φ sur la sphère de Bloch
6. Affiche les coordonnées (x, y, z)

**États à analyser :**
```python
a) |ψ₁⟩ = |0⟩
b) |ψ₂⟩ = |1⟩
c) |ψ₃⟩ = (|0⟩ + |1⟩)/√2
d) |ψ₄⟩ = (|0⟩ − |1⟩)/√2
e) |ψ₅⟩ = (3|0⟩ + 4i|1⟩)/5
f) |ψ₆⟩ = cos(π/6)|0⟩ + sin(π/6)|1⟩
g) |ψ₇⟩ = (2|0⟩ + i|1⟩)/√5
```

**Template de solution :**
```python
def analyze_state(alpha, beta, label):
    """
    Analyse complète d'un état quantique
    """
    print(f"\n{'='*70}")
    print(f"ANALYSE DE L'ÉTAT : {label}")
    print('='*70)
    
    # Créer le qubit
    q = Qubit(alpha, beta)
    print(f"\nÉtat : {q}")
    
    # Vérifier normalisation
    norm_squared = np.abs(q.alpha)**2 + np.abs(q.beta)**2
    print(f"Normalisation : |α|² + |β|² = {norm_squared:.6f}")
    print(f"{'✓' if np.abs(norm_squared - 1) < 1e-10 else '✗'} État normalisé")
    
    # Probabilités
    p0, p1 = q.probabilities()
    print(f"\nProbabilités de mesure :")
    print(f"  P(0) = {p0:.6f} = {p0*100:.2f}%")
    print(f"  P(1) = {p1:.6f} = {p1*100:.2f}%")
    
    # Angles Bloch
    theta, phi = q.get_bloch_angles()
    print(f"\nAngles sur la sphère de Bloch :")
    print(f"  θ (theta) = {theta:.6f} rad = {np.degrees(theta):.2f}°")
    print(f"  φ (phi)   = {phi:.6f} rad = {np.degrees(phi):.2f}°")
    
    # Coordonnées cartésiennes
    x, y, z = q.get_bloch_coordinates()
    print(f"\nCoordonnées cartésiennes :")
    print(f"  x = {x:.6f}")
    print(f"  y = {y:.6f}")
    print(f"  z = {z:.6f}")
    print(f"  Norme = {np.sqrt(x**2 + y**2 + z**2):.6f} (doit être 1)")
    
    return q


# À TOI DE JOUER ! Analyse tous les états
# Par exemple pour a) :
analyze_state(1, 0, "|ψ₁⟩ = |0⟩")

# Continue avec les autres...
```

---

### Exercice 1.2 : Produits Scalaires et Orthogonalité

**Objectif :** Comprendre l'orthogonalité quantique

**Énoncé :**
Calcule les produits scalaires suivants et interprète le résultat :

```python
a) ⟨0|0⟩
b) ⟨0|1⟩
c) ⟨1|0⟩
d) ⟨1|1⟩
e) ⟨+|−⟩
f) ⟨+|+⟩
g) ⟨0|+⟩
h) ⟨1|+⟩
i) ⟨i+|i−⟩
```

**Questions :**
1. Quels états sont orthogonaux ?
2. Que vaut ⟨ψ|φ⟩ si ⟨φ|ψ⟩ = a + bi ?
3. Pourquoi |⟨0|+⟩|² = 1/2 ?

**Template de solution :**
```python
def compute_inner_product(q1, q2, label1, label2):
    """
    Calcule le produit scalaire entre deux qubits
    """
    inner = np.vdot(q1.state_vector, q2.state_vector)
    prob = np.abs(inner)**2
    
    print(f"\n⟨{label1}|{label2}⟩ = {inner:.4f}")
    print(f"|⟨{label1}|{label2}⟩|² = {prob:.4f}")
    
    if np.abs(inner) < 1e-10:
        print("→ États ORTHOGONAUX")
    elif np.abs(prob - 1) < 1e-10:
        print("→ États IDENTIQUES")
    else:
        print(f"→ Probabilité de transition : {prob*100:.2f}%")
    
    return inner, prob


# Définir les états
q_0 = Qubit(1, 0)
q_1 = Qubit(0, 1)
q_plus = Qubit(1/np.sqrt(2), 1/np.sqrt(2))
q_minus = Qubit(1/np.sqrt(2), -1/np.sqrt(2))

# À TOI : calcule tous les produits scalaires
compute_inner_product(q_0, q_0, "0", "0")
# ... continue
```

---

### Exercice 1.3 : Mesures Statistiques

**Objectif :** Vérifier expérimentalement la loi de Born

**Énoncé :**
1. Crée l'état |ψ⟩ = (√3/2)|0⟩ + (1/2)|1⟩
2. Effectue 100, 1000, 10000, 100000 mesures
3. Pour chaque série, calcule :
   - P(0) mesuré
   - P(1) mesuré
   - Écart avec la théorie
4. Trace l'évolution de l'écart en fonction de n
5. Vérifie que l'écart ≈ O(1/√n)

**Solution :**
```python
def statistical_test(alpha, beta, measurement_counts=[100, 1000, 10000, 100000]):
    """
    Teste la convergence statistique pour différents nombres de mesures
    """
    q = Qubit(alpha, beta)
    p0_theory, p1_theory = q.probabilities()
    
    print(f"\nÉtat : {q}")
    print(f"Probabilités théoriques : P(0) = {p0_theory:.6f}, P(1) = {p1_theory:.6f}")
    print("\n" + "="*70)
    print(f"{'N mesures':<15} {'P(0) mesuré':<15} {'P(1) mesuré':<15} {'Écart P(0)':<15}")
    print("="*70)
    
    errors = []
    
    for n in measurement_counts:
        results = q.measure_many(n)
        p0_meas = results.count(0) / n
        p1_meas = results.count(1) / n
        error = abs(p0_meas - p0_theory)
        errors.append(error)
        
        print(f"{n:<15} {p0_meas:<15.6f} {p1_meas:<15.6f} {error:<15.6f}")
    
    print("="*70)
    
    # Vérifier O(1/√n)
    print("\nVérification de la loi O(1/√n) :")
    for n, error in zip(measurement_counts, errors):
        expected = 1 / np.sqrt(n)
        print(f"  n={n:>6} : écart = {error:.6f}, attendu ≈ {expected:.6f}")
    
    return errors


# À TOI !
statistical_test(np.sqrt(3)/2, 1/2)
```

---

### Exercice 1.4 : Visualisation Bloch Complète

**Objectif :** Maîtriser la représentation géométrique

**Énoncé :**
Crée une sphère de Bloch et ajoute les états suivants :
1. Les 6 états de base : |0⟩, |1⟩, |+⟩, |−⟩, |i+⟩, |i−⟩
2. Un état quelconque de ton choix
3. L'état diamétralement opposé à ton état

Vérifie que ton état et son opposé sont orthogonaux.

---

### Exercice 1.5 : Phase Relative Observable

**Objectif :** Observer l'effet de la phase en changeant de base

**Énoncé :**
Considère ces états :
```
|ψ₁⟩ = (|0⟩ + |1⟩)/√2
|ψ₂⟩ = (|0⟩ + e^(iπ/4)|1⟩)/√2
|ψ₃⟩ = (|0⟩ + e^(iπ/2)|1⟩)/√2
|ψ₄⟩ = (|0⟩ + e^(iπ)|1⟩)/√2
```

1. Mesure dans la base {|0⟩, |1⟩} - compare les probabilités
2. Crée une base personnalisée avec φ = π/4
3. Mesure dans cette base - que remarques-tu ?

**Bonus :** Visualise tous ces états sur la sphère de Bloch.

---

## 📊 RÉSUMÉ DU CHAPITRE

### Concepts Clés Maîtrisés

✅ **Qubit** : Superposition quantique α|0⟩ + β|1⟩ avec |α|² + |β|² = 1

✅ **Notation de Dirac** : Kets |ψ⟩, Bras ⟨ψ|, Brackets ⟨φ|ψ⟩

✅ **Probabilités** : P(0) = |α|², P(1) = |β|² (Règle de Born)

✅ **Sphère de Bloch** : Représentation géométrique avec angles θ et φ

✅ **Phase** : Globale (non observable) vs Relative (observable en changeant de base)

✅ **Mesure** : Collapse irréversible vers |0⟩ ou |1⟩

✅ **Orthogonalité** : ⟨φ|ψ⟩ = 0 ⟺ états perpendiculaires sur sphère de Bloch

### Formules Essentielles

```
État général :
|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ)sin(θ/2)|1⟩

Normalisation :
|α|² + |β|² = 1

Probabilités (Règle de Born) :
P(0) = |α|²
P(1) = |β|²

Produit scalaire :
⟨φ|ψ⟩ = α*₁β₁ + α*₂β₂

Coordonnées Bloch :
x = sin(θ)cos(φ)
y = sin(θ)sin(φ)
z = cos(θ)

États remarquables :
|0⟩ : θ=0
|1⟩ : θ=π
|+⟩ : θ=π/2, φ=0
|−⟩ : θ=π/2, φ=π
```

### Code Python - Récapitulatif

**Classes principales :**
```python
Qubit(alpha, beta)              # État quantique
  .probabilities()              # P(0), P(1)
  .measure()                    # Mesure unique
  .measure_many(n)              # n mesures
  .get_bloch_angles()           # θ, φ
  .get_bloch_coordinates()      # x, y, z

BlochSphere()                   # Visualisation
  .draw_sphere()
  .add_state_from_amplitudes(α, β, label, color)
  .show()
```

---

## 🚀 PROCHAINE ÉTAPE : PARTIE 2

Dans la **Partie 2 : Portes Quantiques**, tu vas apprendre à :
- Manipuler les qubits avec des portes (X, Y, Z, H, Phase)
- Créer des superpositions avec Hadamard
- Intriquer des qubits avec CNOT
- Construire des circuits quantiques
- Comprendre les matrices unitaires

**Prérequis pour la Partie 2 :**
✅ Maîtriser tous les concepts de cette partie
✅ Être à l'aise avec les matrices 2×2 et leur multiplication
✅ Comprendre la notation de Dirac

---

## 💡 RESSOURCES COMPLÉMENTAIRES

### Livres Recommandés

**Niveau débutant :**
- "Quantum Computing: A Gentle Introduction" - Rieffel & Polak
- "Dancing with Qubits" - Robert Sutor

**Niveau avancé :**
- "Quantum Computation and Quantum Information" - Nielsen & Chuang (LA bible)
- "Quantum Computing Since Democritus" - Scott Aaronson

**Physique quantique :**
- "Principes de la mécanique quantique" - R. Shankar
- "Modern Quantum Mechanics" - J.J. Sakurai

### Outils Interactifs

**Simulateurs visuels :**
- **Quirk** (quirk.algoritmica.org) : simulateur de circuits, très visuel
- **IBM Quantum Composer** : circuits sur hardware réel
- **Bloch Sphere Simulator** : diverses implémentations en ligne

**Frameworks de programmation :**
- **Qiskit** (IBM) : le plus complet, excellente doc
- **Cirq** (Google) : plus bas niveau, flexible
- **Pennylane** (Xanadu) : focus machine learning quantique

### Cours en Ligne

**Gratuits :**
- IBM Qiskit Textbook (qiskit.org/textbook)
- Microsoft Quantum Katas
- Quantum Country (quantum.country)

**Universités :**
- MIT 8.370 : Quantum Computation
- Caltech CS/Ph 120 : Quantum Computation
- edX : Quantum Mechanics and Quantum Computation (Berkeley)

---

## ✨ LEARNING SCHOOLING FOUNDATION

### Notre Mission

Ce guide fait partie du **Learning Schooling Foundation (LSF)**, une initiative pour rendre l'éducation élite accessible à tous, partout dans le monde.

**Nos principes fondateurs :**

```
🌍 UNIVERSEL
Le savoir ne doit pas être un privilège réservé aux riches
ou à ceux qui vivent dans les "bonnes" villes.

💎 ÉLITE
Contenu de niveau MIT/Caltech/Stanford,
pas du contenu dilué ou simplifié.

🆓 GRATUIT
100% gratuit, pour toujours.
Pas de paywall, pas de premium, jamais.

🔓 OPEN SOURCE
Tout sur GitHub sous licence CC BY-NC 4.0.
Forkable, modifiable, partageable.

🚫 ZÉRO TRACKING
Pas de cookies, pas d'analytics, pas de data.
On ne sait pas qui tu es et on ne veut pas savoir.

🙏 INDÉPENDANT
Pas d'entreprise, pas d'investisseurs, pas d'actionnaires.
Juste du contenu gratuit pour l'humanité.
```

### En Mémoire

Cette fondation existe grâce aux pionniers qui ont lutté pour que le savoir soit libre :

**Richard Stallman** - Pour la philosophie du logiciel libre
**Aaron Swartz (1986-2013)** - Pour son combat pour l'Open Access

*Leur vision : La connaissance comme droit humain universel, pas comme privilège commercial.*

*Nous continuons leur combat.*

---

## 📄 LICENCE

**Creative Commons Attribution-NonCommercial 4.0 (CC BY-NC 4.0)**

Tu es libre de :
- **Partager** : copier, distribuer le matériel
- **Adapter** : remixer, transformer, créer à partir du matériel

Selon les conditions suivantes :
- **Attribution** : Tu dois créditer l'œuvre, fournir un lien vers la licence
- **NonCommercial** : Tu ne peux pas utiliser le matériel à des fins commerciales

**Pas de restrictions supplémentaires** : Tu ne peux pas ajouter de DRM ou de mesures techniques qui empêcheraient l'utilisation du matériel.

---

**© 2024 Learning Schooling Foundation**

**Contact :** github.com/learning-schooling-foundation

**Contribuer :** Les pull requests sont les bienvenues !

---

*"Le savoir appartient à l'humanité."*

**Bon apprentissage ! 🚀⚛️**
