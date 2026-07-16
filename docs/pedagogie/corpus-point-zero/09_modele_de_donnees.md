# Modèle de données initial

## 1. Entités principales

### User

Identité applicative, préférences, consentements et contexte.

### PowerProfile

État d’une Puissance dans un contexte donné.

### MotorSnapshot

Photo datée des six Puissances polaires et de la Transcendance.

### ArchetypeDefinition

Nom, Puissance, amplitude, maîtrise et description.

### ExperienceDefinition

Brique pédagogique versionnée.

### PathwayDefinition

Assemblage d’expériences avec logique narrative et transitions visées.

### ExperienceRun

Réalisation concrète d’une expérience par un joueur ou un groupe.

### Evidence

Trace soutenant ou infirmant une hypothèse de profil.

### Feedback

Retour d’un pair, facilitateur, mentor ou système.

### FigureProfile

Figure historique, fictionnelle, mythologique ou composite.

### AssemblyAvatar

Avatar personnel de l’Assemblée Intérieure.

### Recommendation

Proposition explicable de parcours ou d’expérience.

### CommonResource

Méthode, outil, pratique ou protocole du Commun.

## 2. Relations essentielles

```text
User 1—N MotorSnapshot
MotorSnapshot 1—N PowerProfile
ExperienceDefinition N—N PowerStateTransition
PathwayDefinition N—N ExperienceDefinition
ExperienceRun N—N Evidence
FigureProfile 1—N PowerProfile
AssemblyAvatar N—N FigureProfile
Recommendation N—N ExperienceDefinition / PathwayDefinition
CommonResource 1—N ExperienceDefinition
```

## 3. Nœud d’état

```json
{
  "power": "communication",
  "shadow_level": 2,
  "light_level": 1,
  "mastery": "bloque",
  "context": "professionnel"
}
```

## 4. Transition

```json
{
  "from": {
    "power": "communication",
    "shadow_level": 2,
    "light_level": 1,
    "mastery": "bloque"
  },
  "to": {
    "power": "communication",
    "shadow_level": 2,
    "light_level": 1,
    "mastery": "intermediaire"
  },
  "movement_type": "liberation_circulation"
}
```

## 5. Séparer exploré, maîtrisé et activé

Un seul couple O/L ne suffit pas. Prévoir au minimum :

- `explored_shadow_level` ;
- `explored_light_level` ;
- `freely_mastered_shadow_level` ;
- `freely_mastered_light_level` ;
- `current_activation_polarity` ;
- `current_activation_level` ;
- `circulation_mastery` ;
- `confidence_score`.

## 6. Preuve

Une preuve doit comporter :

- type ;
- auteur ou source ;
- date ;
- contexte ;
- contenu ;
- Puissance concernée ;
- interprétation proposée ;
- poids ;
- niveau de confiance ;
- visibilité ;
- consentement ;
- version de l’expérience associée.

## 7. Figures composites

Une Figure de Devenir peut référencer plusieurs sources d’inspiration, chacune associée à une capacité située et à une phase de vie précise.

## 8. Schémas JSON

Les fichiers du dossier `schemas/` sont des brouillons techniques :

- `motor_profile.schema.json`
- `experience.schema.json`
- `pathway.schema.json`
- `figure.schema.json`
- `assembly_avatar.schema.json`
- `evidence.schema.json`
- `recommendation.schema.json`

Ils doivent être ajustés après choix de la stack, de la base de données et du moteur de graphe.
