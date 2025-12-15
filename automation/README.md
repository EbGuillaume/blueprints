# IKEA BILRESA Scroll Wheel Controller Blueprint (Matter)

Ce blueprint permet de contrôler facilement jusqu'à 3 lumières avec la télécommande IKEA BILRESA connectée en Matter à Home Assistant.

## Fonctionnalités

- **3 positions LED** : Contrôlez 3 lumières différentes en changeant de position avec le bouton sous les LEDs
- **Rotation de molette** : Ajustez la luminosité en tournant la molette (sens horaire pour augmenter, anti-horaire pour diminuer)
- **Actions sur clics** :
  - Clic simple (par défaut : allumer/éteindre)
  - Double clic (par défaut : luminosité 100%)
  - Triple clic (configurable)
  - Appui long (par défaut : éteindre)
- **Configuration flexible** : Personnalisez les actions de chaque type de clic

## Structure de la télécommande BILRESA

La télécommande dispose de :
- **Une molette rotative et cliquable** :
  - Rotation sens horaire (augmente la luminosité)
  - Rotation sens anti-horaire (diminue la luminosité)
  - Clic, double-clic, triple-clic et appui long
- **Un bouton de changement de position** : Situé sous les 3 LEDs, permet de basculer entre 3 positions (LED 1, 2 ou 3)
- **3 LEDs** : Indiquent quelle position est active (et donc quelle lumière est contrôlée)

Cela donne au total **9 entités event** dans Home Assistant :
- Boutons 1, 2, 3 : Position LED 1
- Boutons 4, 5, 6 : Position LED 2
- Boutons 7, 8, 9 : Position LED 3

Pour chaque position :
- Bouton X1 : Rotation molette sens horaire
- Bouton X2 : Rotation molette sens anti-horaire
- Bouton X3 : Clics sur la molette

## Installation

### Méthode 1 : Importation directe

[![Importer ce blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/your-repo/blueprints/blob/main/automation/ikea_bilresa_matter.yaml)

### Méthode 2 : Manuelle

1. Copiez le contenu du fichier `ikea_bilresa_matter.yaml`
2. Dans Home Assistant, allez dans **Paramètres** → **Automatisations & Scènes** → **Blueprints**
3. Cliquez sur **Importer un Blueprint** (bouton en bas à droite)
4. Collez l'URL ou le contenu du blueprint
5. Cliquez sur **Aperçu** puis **Importer**

## Configuration

### Prérequis

Assurez-vous que votre télécommande IKEA BILRESA est :
1. Connectée à Home Assistant via Matter
2. Visible dans **Paramètres** → **Appareils & Services** → **Matter**
3. Que vous voyez les 9 entités event (event.bilresa_scroll_wheel_bouton_1 à bouton_9)

### Étape 1 : Identifier les entités

Dans Home Assistant, notez les noms exacts de vos entités event. Ils devraient ressembler à :
- `event.bilresa_scroll_wheel_bouton_1` (rotation horaire - LED 1)
- `event.bilresa_scroll_wheel_bouton_2` (rotation anti-horaire - LED 1)
- `event.bilresa_scroll_wheel_bouton_3` (clics molette - LED 1)
- `event.bilresa_scroll_wheel_bouton_4` (rotation horaire - LED 2)
- ... et ainsi de suite jusqu'au bouton_9

### Étape 2 : Créer une automatisation à partir du blueprint

1. Allez dans **Paramètres** → **Automatisations & Scènes** → **Automatisations**
2. Cliquez sur **Créer une automatisation** → **Commencer avec un blueprint**
3. Sélectionnez **IKEA BILRESA Scroll Wheel Controller (Matter)**
4. Configurez les paramètres :

#### Configuration des boutons

Sélectionnez les 9 entités event correspondant aux boutons :
- **Bouton 1 à 3** : Position LED 1
- **Bouton 4 à 6** : Position LED 2
- **Bouton 7 à 9** : Position LED 3

#### Configuration des lumières

Sélectionnez jusqu'à 3 lumières à contrôler :
- **Lumière Position 1** : Contrôlée quand la LED 1 est allumée
- **Lumière Position 2** : Contrôlée quand la LED 2 est allumée
- **Lumière Position 3** : Contrôlée quand la LED 3 est allumée

Vous pouvez laisser certaines positions vides si vous ne souhaitez pas contrôler 3 lumières.

#### Configuration des actions

Personnalisez les actions selon vos préférences :
- **Pas de luminosité** : Incrément par cran de rotation (1-25%, défaut : 10%)
- **Action sur clic simple** : Par défaut "Toggle" (allumer/éteindre)
- **Action sur double clic** : Par défaut "Luminosité 100%"
- **Action sur triple clic** : Par défaut "Aucune action"
- **Action sur appui long** : Par défaut "Éteindre"

5. Donnez un nom à votre automatisation
6. Cliquez sur **Enregistrer**

## Utilisation

### Contrôle de base

1. **Changez de position** : Appuyez sur le bouton sous les LEDs pour basculer entre les 3 positions (LED 1, 2 ou 3)
2. **Ajustez la luminosité** : Tournez la molette pour augmenter (sens horaire) ou diminuer (sens anti-horaire) la luminosité de la lumière active
3. **Allumez/Éteignez** : Cliquez une fois sur la molette (par défaut)
4. **Luminosité maximale** : Double-cliquez sur la molette (par défaut)
5. **Éteindre rapidement** : Maintenez la molette enfoncée (appui long, par défaut)

### Exemple de configuration

**Salon avec 3 zones :**
- LED 1 → Plafonnier principal
- LED 2 → Lampe d'ambiance
- LED 3 → Spots de lecture

**Actions :**
- Clic simple : Allumer/Éteindre
- Double clic : Luminosité 100%
- Triple clic : Aucune action
- Appui long : Éteindre
- Rotation : Ajuster luminosité par pas de 10%

## Dépannage

### Les événements ne sont pas détectés

1. Vérifiez que votre télécommande est bien connectée en Matter (pas en Zigbee)
2. Allez dans **Outils de développement** → **Événements**
3. Écoutez les événements `state_changed`
4. Appuyez sur les boutons de la télécommande et vérifiez que les entités event changent d'état
5. Notez les valeurs `event_type` dans les attributs (multi_press_1, multi_press_2, etc.)

### La luminosité ne change pas

1. Vérifiez que votre lumière supporte le contrôle de luminosité
2. Essayez d'augmenter le "Pas de luminosité" à 15-20%
3. Vérifiez que la lumière est bien allumée avant d'ajuster la luminosité

### Les multi-clics ne fonctionnent pas bien

Les événements Matter peuvent parfois être lents à se déclencher. Essayez de :
- Cliquer plus lentement pour les doubles/triples clics
- Utiliser l'appui long comme alternative
- Vérifier dans les logs si les événements sont bien reçus

## Structure des événements Matter

Pour référence, voici la structure des événements générés par la BILRESA :

### Boutons de rotation (1, 2, 4, 5, 7, 8)
```yaml
event_type: multi_press_1  # ou multi_press_2, ..., multi_press_8
previousPosition: 1
totalNumberOfPressesCounted: 1  # ou 2, 3, etc.
```

### Boutons de clic (3, 6, 9)
```yaml
event_type: multi_press_1  # Clic simple
# ou
event_type: multi_press_2  # Double clic
# ou
event_type: multi_press_3  # Triple clic
# ou
event_type: long_press     # Appui long
event_type: long_release   # Relâchement après appui long
```

## Support et contribution

Si vous rencontrez des problèmes ou avez des suggestions :
1. Vérifiez d'abord la section Dépannage ci-dessus
2. Consultez les logs de Home Assistant pour plus d'informations
3. Ouvrez une issue sur GitHub avec les détails de votre configuration

## Licence

Ce blueprint est fourni tel quel, libre d'utilisation et de modification.
