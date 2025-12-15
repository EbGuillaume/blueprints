# Home Assistant Blueprints

Collection de blueprints pour Home Assistant facilitant l'intégration de divers appareils et automatisations.

## Blueprints disponibles

### IKEA BILRESA Scroll Wheel Controller (Matter)

Blueprint pour la télécommande IKEA BILRESA connectée en Matter, permettant de contrôler jusqu'à 3 lumières avec une molette rotative et des actions de clic personnalisables.

**Caractéristiques :**
- Contrôle de 3 lumières différentes via 3 positions LED
- Rotation de molette pour ajuster la luminosité
- Clics simples, doubles, triples et appui long
- Actions entièrement configurables

**Documentation complète :** [automation/README.md](automation/README.md)

**Fichiers :**
- Blueprint : [automation/ikea_bilresa_matter.yaml](automation/ikea_bilresa_matter.yaml)
- Exemple : [automation/example_automation.yaml](automation/example_automation.yaml)

## Installation

### Importer un blueprint

1. Allez dans **Paramètres** → **Automatisations & Scènes** → **Blueprints**
2. Cliquez sur **Importer un Blueprint**
3. Collez l'URL du blueprint depuis ce repository
4. Cliquez sur **Aperçu** puis **Importer**

### Utiliser un blueprint

1. Allez dans **Paramètres** → **Automatisations & Scènes** → **Automatisations**
2. Cliquez sur **Créer une automatisation** → **Commencer avec un blueprint**
3. Sélectionnez le blueprint souhaité
4. Configurez les paramètres selon vos besoins
5. Enregistrez l'automatisation

## Contribution

Les contributions sont les bienvenues ! N'hésitez pas à proposer de nouveaux blueprints ou des améliorations aux blueprints existants.

## Support

Pour toute question ou problème :
1. Consultez la documentation du blueprint concerné
2. Vérifiez les fichiers d'exemple
3. Consultez les logs de Home Assistant pour plus de détails
