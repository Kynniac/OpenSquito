# OpenSquito 🦟

**OpenSquito** est un **projet** open source **en cours de développement** d'un piège à moustiques **innovant** 
Actuellement basé sur un ESP32, mais à terme sera probablement porté sur d'autres MCU à des fins de réduction de coût comme les ARM et STM.

Conçu pour attirer et capturer les moustiques **mâles** à l’aide de sons spécifiques, d’une aspiration contrôlée et d'une détection acoustique, optique ou électrique à des fins de prototypage de différentes déclinaisons à venir.

> 🔌 Pourra fonctionner **avec ou sans domotique**. Mode **offline autonome** possible, y compris sur **batterie + panneau solaire**.

---

## 🌍 Enjeux et urgence d’agir

Les moustiques sont **les insectes les plus dangereux du reigne du vivant**, responsables de plus de 700 000 décès humains chaque année en tant que vecteurs de maladies infectieuses graves comme le paludisme, la dengue, le Zika, Chikungunya ou la fièvre jaune (sources : [OMS – Malaria Fact Sheet](https://www.who.int/news-room/fact-sheets/detail/malaria), [OMS – Dengue and severe dengue](https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue)).

La répartition géographique de ces vecteurs s’étend fortement avec le **réchauffement climatique** et l’urbanisation :

* **Europe** : selon l’[ECDC Mosquito Maps](https://www.ecdc.europa.eu/en/disease-vectors/surveillance-and-disease-data/mosquito-maps) et l’[Institut Pasteur](https://www.pasteur.fr/fr/espace-presse/documents-presse/dengue-france-cas-autochtone-2023), **Aedes albopictus** (moustique tigre) est établi dans plus de 20 pays (France, Italie, Espagne, Suisse…), avec des cas autochtones de dengue, chikungunya et Zika.
* **Paludisme autochtone** : des foyers ont été signalés en Grèce, Italie, France et Espagne ([OMS – Malaria in Europe](https://www.who.int/news-room/spotlight/malaria-now-and-then), [ECDC – Paludisme](https://www.ecdc.europa.eu/en/malaria/surveillance-and-disease-data)).
* **Projections climatiques** : les modèles prévoient une extension vers le nord et l’est de l’Europe avec des conditions favorables à la reproduction estivale dès les prochaines décennies ([Nature Climate Change, 2023](https://www.nature.com/articles/s41558-023-01895-0)).
* **Monde** : l’aire de répartition d’**Aedes aegypti** augmente de 3,2–4,4 % par décennie, avec un déplacement vers le nord‑est de l’Amérique et de la Chine prévu d’ici 2050 ([Nature Climate Change, 2023](https://www.nature.com/articles/s41558-023-01895-0)).

## ❓ Pourquoi piéger en priorité les moustiques mâles qui ne nous piquent pourtant pas?

Les systèmes commerciaux actuels les plus efficaces pour piéger les moustiques (**femelles uniquement**) utilisent souvent du **CO₂** comme leurre, émis par combustion de gaz fossile, ou via des bonbonnes sous pression ou des phéromones. 
Ces solutions sont coûteuses (entre 350 et 1 000€ pièce), encombrantes, utilisent des consommables, relâchent du **CO₂** et sont énergivores.

**OpenSquito adopte une approche diamétralement opposée tout en étant plus vertueuse et économique** 
En ciblant **uniquement les mâles**, il suffit seulement de produire des **sons** spécifiques (simulant le vol des femelles) pour les attirer.
Sans émissions autres que sonores; ni consommables.

**Les avantages de ce projet:** 

* 🎯 **Attraction sonore ciblée** : les mâles recherchent activement le bourdonnement des femelles (≈ 400–600 Hz selon les espèces). 
* 🚫 **Briser le cycle de reproduction** : un seul mâle peut féconder plusieurs femelles ; retirer une petite fraction de mâles réduit significativement la descendance.
* 🧪 **Surveillance passive** : mesurer le nombre de mâles capturés offre un indicateur indirect de l’activité globale, utile pour la recherche et l’alerte précoce.
* 🌱 **Approche écologique** : aucun pesticide, peu d’énergie, pas de consommable, fonctionnement silencieux pour la majorité des cas d'usage. 

Cette stratégie **complète** les méthodes de lutte actuels dirigées contre les femelles (filets, larvicides, moustiques OGM, etc) et peut être déployée dans les zones rurales comme urbaines.

---

## 🔧 Fonctionnalités principales

* ✅ **Émission sonore** paramétrable en fréquences (300–600 Hz) et en intensité pour attirer les moustiques mâles de différentes espèces
* 🎤 **Détection acoustique** par microphone (I2S ou analogique) *à définir selon retex
* 💨 **Aspiration contrôlée** avec ventilateur silencieux PWM
* 🧠 **Automatisation** via ESPHome + Home Assistant (optionnel)
* 🔋 **Mode autonome offline** : déclenchement local, stockage de logs sur carte SD, ou pas.
* 🌐 **Connexion à un réseau citoyen www.opensquito.net** : partage de données de capture pour la cartographie et la recherche

---

## 🧩 Composants recommandés

| Catégorie    | Exemple                                 | Notes                           |
| ------------ | --------------------------------------- | ------------------------------- |
| MCU          | ESP32                                   | WROVER, P4, C3, ou autre        |
| Microphone   | INMP441 (I2S)                           | Faible bruit, facile à intégrer |
| Driver audio | DAC I2S ou PWM                          | MAX98357                        |
| Ventilateur  | PWM 5V/12V                              | Silencieux, longue durée        |
| Alimentation | POE ↓ 48 V → 5 V DC, Power-Bank, Li-ion | S’adapte aux contextes          |

---

## 🦟 Espèces cibles & adaptation du piège

* **Bande sonore ajustable** : modifiez la fréquence émise pour cibler d’autres espèces selon les régions (Culex, Anopheles…).
* **Paramètres régionaux** : vitesse de ventilation, grille anti-évasion, taille du filet peuvent être adaptés aux espèces locales.
* **Un tableau de correspondance fréquence** ⇄ espèce la plus réceptive figure dans `docs/species_frequency.md` (compilé par la communauté).

---

## 🌐 Réseau citoyen www.OpenSquito.net

Même sans domotique locale, la version connectée peut :

1. 📡 **Envoyer périodiquement** le comptage de captures (via Wi-Fi, LoRa, LTE-M) vers une base de données libre et collaborative.
2. 🗺️ **Cartographier** l’activité moustique en temps réel (interface publique type MapTiles).
3. 🔔 **Détecter les flambées** régionales et informer les citoyens ou/et éventuellement les services de santé.

Toutes les données seront anonymisées et publiées sous licence **ODbL** pour encourager la recherche ouverte.

---

## 📦 Structure du dépôt

```text
OpenSquito/
├── src/            # Code source (ESPHome YAML, firmwares, scripts)
├── hardware/       # Schémas, PCB, STL/3D, BOM
├── docs/           # Documentation technique et d'installation
├── examples/       # Configurations d'exemple
├── README.md
├── LICENSE         # Licence MIT (code)
└── CONTRIBUTING.md
```

---

## 📜 Licence

* **Code** : [MIT](./LICENSE)
* **Documentation & designs** : [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
* **Données OpenSquito Net** : [Open Database License (ODbL) 1.0](https://opendatacommons.org/licenses/odbl/)

---

## 🤝 Contribuer

Toutes les contributions sont bienvenues ! Consultez [CONTRIBUTING.md](./CONTRIBUTING.md) pour le processus de fork/PR, le style de code et le Code of Conduct.

---

## 📚 Sources scientifiques

* [OMS – Malaria Fact Sheet](https://www.who.int/news-room/fact-sheets/detail/malaria)
* [OMS – Dengue and severe dengue](https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue)
* [Nature Climate Change – Ryan et al. (2023)](https://www.nature.com/articles/s41558-023-01895-0)
* [ECDC – Mosquito Maps](https://www.ecdc.europa.eu/en/disease-vectors/surveillance-and-disease-data/mosquito-maps)
* [Signalement moustique (France)](https://www.signalement-moustique.fr)
* [Institut Pasteur – Dengue autochtone en France](https://www.pasteur.fr/fr/espace-presse/documents-presse/dengue-france-cas-autochtone-2023)
* [OMS – Malaria in Europe](https://www.who.int/news-room/spotlight/malaria-now-and-then)
* [ECDC – Paludisme en Europe](https://www.ecdc.europa.eu/en/malaria/surveillance-and-disease-data)
