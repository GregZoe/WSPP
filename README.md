# 📈 WSPP — Wall Street Pour les Pauvres

App de simulation de portefeuilles boursiers avec cours en live et prédictions IA.

**URL live →** https://gregzoe.github.io/WSPP/wspp.html

---

## 🎯 Concept

Tester 3 stratégies d'investissement différentes avec 500€ chacun, sur des ETFs (S&P 500, défense, obligations, IA...), avec des signaux IA qui prédisent les hausses/baisses à 1j, 3j, 5j et 10j.

---

## 👤 Les 3 portefeuilles

| Utilisateur | Profil | Couleur | Capital |
|---|---|---|---|
| Papa | Équilibré | Bleu #3B82F6 | 500€ |
| Nayla | Croissance | Violet #8B5CF6 | 500€ |
| Hannan | Défensif | Vert #10B981 | 500€ |

### Papa — Équilibré
| ETF | Ticker réel | Investi |
|---|---|---|
| ETF Défense Europe | ITA | 150€ |
| ETF S&P 500 | SPY | 150€ |
| ETF Obligations 1-3Y | SHY | 100€ |
| ETF Stoxx 600 Europe | VGK | 100€ |

### Nayla — Croissance
| ETF | Ticker réel | Investi |
|---|---|---|
| ETF IA & Robotique | BOTZ | 200€ |
| ETF Nasdaq 100 | QQQ | 150€ |
| ETF Énergie Propre | ICLN | 100€ |
| ETF Marchés Émergents | VWO | 50€ |

### Hannan — Défensif
| ETF | Ticker réel | Investi |
|---|---|---|
| ETF Obligations Souv. | BND | 200€ |
| ETF Dividendes Europe | VYM | 150€ |
| ETF Santé Mondial | VHT | 100€ |
| ETF Stoxx 600 Europe | VGK | 50€ |

---

## 🗓️ Règles du test

- **Début :** 07 mars 2026
- **Check-in :** Chaque vendredi
- **Stop-loss :** -8% → on sort
- **Take profit :** +5% en moins de 2 semaines → on revend la moitié
- **Prochain bilan :** Vendredi 13 mars 2026

---

## 🏗️ Architecture

```
WSPP/
├── wspp.html          ← App web (GitHub Pages)
│
wspp-ml/               ← Sur le Mac, PAS sur GitHub
├── model.py           ← Modèle Random Forest
├── api.py             ← Serveur Flask port 5001
├── requirements.txt   ← Dépendances Python
├── setup.sh           ← Installation automatique
└── predictions.json   ← Généré au lancement
```

---

## 🤖 Serveur IA — Lancement

```bash
# Dans VS Code, ouvrir le dossier wspp-ml
# Puis dans le terminal :

source venv/bin/activate
python3 api.py
```

Le modèle analyse **76 actifs** (11 ETFs + 35 CAC40 + 30 Dow Jones) et génère des prédictions à **1j, 3j, 5j et 10j**.

L'API est disponible sur : `http://localhost:5001/predictions`

⚠️ VS Code doit rester ouvert pour que les signaux IA s'affichent dans l'app.

---

## 📡 Sources de données

| Source | Usage | Clé API |
|---|---|---|
| Twelve Data | Cours en live | `e6ec26e5f3394dc996cc0b27b56d060a` |
| Yahoo Finance (yfinance) | Données historiques pour le ML | Gratuit |

---

## 🧠 Modèle ML

**Algorithme :** Random Forest Classifier (scikit-learn)

**Features (22 indicateurs) :**
- Returns 1j, 3j, 5j, 10j, 20j
- Ratios prix/moyennes mobiles (MA5, MA10, MA20, MA50)
- RSI 14 jours + zones surachat/survente
- MACD + signal + divergence
- Volatilité 5j et 20j
- Bandes de Bollinger (position relative)
- Ratio volume vs moyenne 10j
- Momentum 10j et 20j

**Entraînement :** 5 ans de données historiques, 80% train / 20% test

**Précision typique :** 52–65% selon l'actif

**Refresh :** Automatique toutes les 24h

---

## 📊 Features de l'app

- ✅ Cours en live via Twelve Data (refresh toutes les 5 min)
- ✅ P&L en temps réel par position et par portefeuille
- ✅ Signaux IA ▲▼ sur chaque position (4 horizons)
- ✅ Top 5 hausses / baisses prévues parmi 76 actifs
- ✅ Journal de notes par utilisateur
- ✅ Sauvegarde automatique (localStorage)

---

## 🔮 Roadmap

- [ ] **Phase 2** — Feedback loop : comparer prédictions vs résultats réels
- [ ] **Phase 3** — Modèles plus puissants (XGBoost, LSTM)
- [ ] **Phase 4** — Intégrer sentiment news + données macro
- [ ] **Phase 5** — Alertes automatiques par email/SMS si signal fort

---

## 📅 Historique

| Date | Événement |
|---|---|
| 07/03/2026 | Création des 3 portefeuilles, déploiement app + serveur IA |
| 13/03/2026 | Premier bilan hebdomadaire |

---

*Simulation pédagogique — pas un conseil en investissement.*
