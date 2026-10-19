# TV-M-canique-Asservissement-du-disque-Driver-LED-DFTA283

# Moniteur de Télévision Mécanique (NBTV 32 Lignes, 12.5 fps)
## Étage de Commande Numérique et Puissance Analogique — Réf: DFTA283

Ce dépôt rassemble les fichiers de conception matérielle, les simulations et le code source de l'étage de synchronisation et de puissance de mon moniteur de télévision mécanique au standard de la **NBTVA** (32 lignes verticales, 12,5 images par seconde). 

Ce projet fait suite à la requalification de l'étage de traitement vidéo analogique (**DFTA282**).

## 🛠️ Spécifications du Hardware (100% Traversant)

L'architecture est répartie sur deux modules principaux conçus sous EasyEDA :

### 1. Module Driver LED & Amplis Annexes (DFTA283-1)
* **Driver LED Asservi :** Régulation linéaire en courant (AOP `U3.A` + MOSFET `Q3` 042N03L) pour moduler la matrice de LED (*LED ARRAY*) avec compensation d'avance de phase (`C8` de 20 pF) pour stabiliser la boucle locale.
* **Correction de Gamma Matérielle :** Shunt de mesure dynamique à impédance variable combinant résistances de pied et diodes de natures différentes (classique `1N4148` et Schottky `1N5819`) pour compenser la réponse logarithmique de l'œil.
* **Barrière Infrarouge (PULSEDISC) :** Émission à courant constant (`U3.B` + `Q4`) et circuit de mise en forme par photodiode inversée et MOSFET (`Q1` BS170) délivrant des impulsions carrées nettes (0/15V) pour la capture optique des trous du disque.
* **Aiguillage de Phase :** Deux voies indépendantes d'amplification linéaire (Inverseuse `U3.D` avec un gain de -5,6 et Non-Inverseuse `U3.C` avec un gain de +5,7) pour adapter n'importe quelle source vidéo NBTV asymétrique.

### 2. Module Synchro DISC & Commande Moteur (DFTA283-2)
* **PLL Logicielle :** Remplacement du circuit intégré CD4046 par un microcontrôleur **ATtiny85-20U** (`U4`) cadençant l'algorithme de comparaison de phase.
* **Alimentation Flottante :** Masse logique de l'ATtiny85 surélevée sur un rail **ZERO** à +1,8V via une LED rouge (`D6`) faisant office de *level-shifter* passif. L'alimentation locale 5,1V est stabilisée par une diode Zener (`D7`).
* **Nœud de Sommation Évolué :** Filtrage de boucle du second ordre basé sur les travaux de **Klaas Robers** et les analyses de **LabGuy**. Le curseur du potentiomètre `RV8` fait office de nœud de sommation mélangeant l'action proportionnelle nerveuse de l'ATtiny85 (côté gauche via `R49`) et la composante continue de régulation de vitesse moyenne issue de la tension de drain du moteur (côté droit via `R50` et la capacité chimique `C2` de 47 µF). Le point central est stabilisé par `C1` (100 nF).


## 🚀 Prochaine Étape : DFTA284
Ce module valide la fin de la conception électronique. Le projet s'oriente désormais vers le design de l'enclosure (base en Sympan de 15 mm, parois de 5 mm et blocs de maintien en POM noir usinés à la CNC 3018) et l'assemblage mécanique final.

---
**Conçu par :** claudiusmarius  
**Licence :** Open-Source DIY / NBTV Association Community  
