# OpenSquito 🦟

**OpenSquito** est un projet open source de piège à moustiques intelligent, basé sur l’ESP32, conçu pour attirer, détecter et capturer principalement les moustiques **mâles** à l’aide de sons spécifiques, d’une détection acoustique et d’une aspiration contrôlée.

> 🔌 Peut fonctionner **avec ou sans domotique**. Mode **offline autonome** possible, y compris sur **batterie**.

---

## 🌍 Enjeux mondiaux et urgence d’agir

Les moustiques sont **les insectes les plus dangereux du monde animal**, responsables de plus de 700 000 décès humains chaque année en tant que vecteurs de maladies infectieuses graves comme le paludisme, la dengue, le Zika ou la fièvre jaune (sources : [OMS – Malaria Fact Sheet](https://www.who.int/news-room/fact-sheets/detail/malaria), [OMS – Dengue and severe dengue](https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue)). Chaque année, près de 700 millions de personnes contractent une maladie transmise par les moustiques.

La répartition géographique de ces vecteurs s’étend fortement avec le **réchauffement climatique** et l’urbanisation :

* **Europe** : selon l’[ECDC Mosquito Maps](https://www.ecdc.europa.eu/en/disease-vectors/surveillance-and-disease-data/mosquito-maps) et l’[Institut Pasteur](https://www.pasteur.fr/fr/espace-presse/documents-presse/dengue-france-cas-autochtone-2023), **Aedes albopictus** (moustique tigre) est établi dans plus de 20 pays (France, Italie, Espagne, Suisse…), avec des cas autochtones de dengue, chikungunya et Zika.
* **Paludisme autochtone** : des foyers ont été signalés en Grèce, Italie, France et Espagne ([OMS – Malaria in Europe](https://www.who.int/news-room/spotlight/malaria-now-and-then), [ECDC – Paludisme](https://www.ecdc.europa.eu/en/malaria/surveillance-and-disease-data)).
* **Projections climatiques** : les modèles prévoient une extension vers le nord et l’est de l’Europe avec des conditions favorables à la reproduction estivale dès les prochaines décennies ([Nature Climate Change, 2023](https://www.nature.com/articles/s41558-023-01895-0)).
* **Monde** : l’aire de répartition d’**Aedes aegypti** augmente de 3,2–4,4 % par décennie, avec un déplacement vers le nord‑est de l’Amérique et de la Chine prévu d’ici 2050 ([Nature Climate Change, 2023](https://www.nature.com/articles/s41558-023-01895-0)).

## ❓ Pourquoi piéger en priorité les moustiques mâles ?

Les systèmes commerciaux les plus efficaces pour piéger les **femelles** utilisent souvent du **CO₂** comme leurre, émis par combustion de gaz ou via des bonbonnes sous pression. Ces solutions sont coûteuses, encombrantes, et énergivores.

**OpenSquito adopte une approche plus vertueuse et économique** : en ciblant les **mâles**, il suffit de produire un **son** spécifique (simulant le vol des femelles) pour les attirer, sans émissions ni consommables.
Pourquoi piéger en priorité les moustiques mâles ?

* 🎯 **Attraction sonore ciblée** : les mâles recherchent activement le bourdonnement des femelles (≈ 400–600 Hz). Émettre judicieusement dans ces plages de fréquences permet de les attirer sélectivement.
* 🚫 **Briser le cycle de reproduction** : un seul mâle peut féconder plusieurs femelles ; retirer une petite fraction de mâles réduit significativement la descendance.
* 🧪 **Surveillance passive** : mesurer le nombre de mâles capturés offre un indicateur indirect de l’activité globale, utile pour la recherche et l’alerte précoce.
* 🌱 **Approche écologique** : aucun pesticide, peu d’énergie, fonctionnement silencieux.

Cette stratégie complète les méthodes de lutte dirigées contre les femelles (filets, larvicides, stérilisation incompatible) et peut être déployée dans les zones rurales comme urbaines.

---

## 🔧 Fonctionnalités principales

* ✅ **Émission sonore** paramétrable (300–600 Hz) pour attirer les moustiques mâles
* 🎤 **Détection acoustique** par microphone (I2S ou analogique)
* 💨 **Aspiration contrôlée** avec ventilateur silencieux (Noctua 80 mm ≈ 15 CFM)
* 🧠 **Automatisation** via ESPHome + Home Assistant (optionnelle)
* 🔋 **Mode autonome offline** : déclenchement local, stockage de logs sur carte SD ou envoi LoRa/Wi-Fi ponctuel
* 🌐 **Connexion à un réseau citoyen mondial (opensquito.net)** : partage de données de capture pour la cartographie et la recherche

---

## 🧩 Composants recommandés

| Catégorie    | Exemple                                 | Notes                           |
| ------------ | --------------------------------------- | ------------------------------- |
| MCU          | ESP32 (OLIMEX ESP32-POE2)               | POE natif ou USB/batterie       |
| Microphone   | INMP441 (I2S)                           | Faible bruit, facile à intégrer |
| Driver audio | DAC I2S ou PWM                          | Selon la carte                  |
| Ventilateur  | Noctua NF-A8 5V/12V                     | Silencieux, longue durée        |
| Alimentation | POE ↓ 48 V → 5 V DC, Power-Bank, Li-ion | S’adapte aux contextes          |

---

## 🦟 Espèces cibles & adaptation du piège

* **Bande sonore ajustable** : modifiez la fréquence émise pour cibler d’autres genres (Culex, Anopheles…).
* **Paramètres régionaux** : vitesse de ventilation, grille anti-évasion, taille du filet peuvent être adaptés aux espèces locales.
* Un tableau de correspondance fréquence ⇄ espèce la plus réceptive figure dans `docs/species_frequency.md` (compilé par la communauté).

---

## 🌐 Réseau citoyen mondial (OpenSquito.net)

Même sans domotique locale, la version connectée peut :

1. 📡 **Envoyer périodiquement** le comptage de captures (Wi-Fi, LoRa, LTE-M) vers une base de données libre.
2. 🗺️ **Cartographier** l’activité moustique en temps réel (interface publique type MapTiles).
3. 🔔 **Détecter les flambées** régionales et informer les citoyens ou services de santé.

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

Les contributions sont les bienvenues ! Consultez [CONTRIBUTING.md](./CONTRIBUTING.md) pour le processus de fork/PR, le style de code et le Code of Conduct.

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
