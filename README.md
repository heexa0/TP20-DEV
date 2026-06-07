# TP-20 — Développement Android
### Chaoulid Hafssa · ENSA Marrakech · Génie Informatique GCDSTE · 2025-2026

---

## À propos de ce projet

Ce dépôt contient le projet Android réalisé dans le cadre du TP n°20 du module Développement Mobile. L'application a été initialisée sous Android Studio avec une architecture standard à Activity unique, en Java. Le point de départ est volontairement minimal : l'objectif du TP est de construire les fonctionnalités par-dessus cette base, pas de partir d'un projet déjà rempli.

---

## Identité du projet

| Clé | Valeur |
|---|---|
| Nom de l'application | TP-20_dev |
| Package | `com.example.tp_20_dev` |
| Langage | Java |
| minSdk | 24 (Android 7.0 Nougat) |
| targetSdk | 36 |
| AGP | 9.1.1 |
| Gradle | 9.3.1 |

---

## Structure du projet

```
TP20_dev/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/tp_20_dev/
│   │       │   └── MainActivity.java       ← point d'entrée de l'app
│   │       ├── res/
│   │       │   ├── layout/
│   │       │   │   └── activity_main.xml   ← layout principal
│   │       │   └── values/
│   │       │       ├── strings.xml
│   │       │       ├── colors.xml
│   │       │       └── themes.xml
│   │       └── AndroidManifest.xml
│   └── build.gradle.kts                    ← dépendances et config build
├── gradle/
│   └── libs.versions.toml                  ← catalogue des versions
└── settings.gradle.kts
```

---

## Ce que contient le code de départ

**`MainActivity.java`**

L'Activity principale hérite de `AppCompatActivity`. Elle active le mode EdgeToEdge (affichage plein écran avec gestion automatique des barres système) et applique un padding dynamique via `ViewCompat.setOnApplyWindowInsetsListener` pour que le contenu ne soit jamais masqué par la barre de navigation ou la barre d'état.

```java
EdgeToEdge.enable(this);
setContentView(R.layout.activity_main);
ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
    Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
    v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
    return insets;
});
```

**`activity_main.xml`**

Un `ConstraintLayout` racine contenant un `TextView` centré. C'est le canvas vide sur lequel le TP se construit.

**`AndroidManifest.xml`**

Une seule Activity déclarée, exportée avec un `intent-filter` MAIN/LAUNCHER. Pas de permissions déclarées dans ce template — à ajouter selon les besoins du TP.

---

## Dépendances déclarées

| Bibliothèque | Version | Rôle |
|---|---|---|
| `androidx.appcompat` | 1.6.1 | Compatibilité backward pour les composants UI |
| `com.google.android.material` | 1.10.0 | Composants Material Design |
| `androidx.activity` | 1.8.0 | Gestion du cycle de vie Activity |
| `androidx.constraintlayout` | 2.1.4 | Layout flexible et performant |
| `junit` | 4.13.2 | Tests unitaires |
| `androidx.test.ext:junit` | 1.1.5 | Tests instrumentés |
| `espresso-core` | 3.5.1 | Tests UI automatisés |

---

## Lancer le projet

### Prérequis

- Android Studio Hedgehog ou plus récent
- JDK 11
- Un émulateur Android API 24+ ou un appareil physique avec le débogage USB activé

### Étapes

```bash
# 1. Cloner ou extraire le projet
cd TP20_dev

# 2. Ouvrir dans Android Studio
#    Fichier → Ouvrir → sélectionner le dossier TP20_dev

# 3. Laisser Gradle synchroniser les dépendances (automatique)

# 4. Lancer sur émulateur ou appareil
#    Bouton ▶ dans Android Studio
#    ou via ADB :
adb install app/build/outputs/apk/debug/app-debug.apk
```

### Build en ligne de commande

```bash
# Build debug
./gradlew assembleDebug

# Lancer les tests unitaires
./gradlew test

# Lancer les tests instrumentés (émulateur requis)
./gradlew connectedAndroidTest
```

---

## Notes personnelles sur le TP

Ce projet représente la base de départ fournie pour le TP 20. La structure choisie — une Activity unique en Java avec `ConstraintLayout` — correspond à ce qui est vu en cours. Le choix de Java (plutôt que Kotlin) est cohérent avec le parcours suivi depuis le début du module.

Le mode EdgeToEdge activé par défaut dans les projets Android Studio récents (API 35+) change la façon dont les paddings doivent être gérés : il ne faut plus compter sur le système pour réserver l'espace des barres, mais le calculer manuellement via `WindowInsets`, comme illustré dans `MainActivity`.

---

## Environnement de développement utilisé

- **OS :** Windows 11
- **Android Studio :** Ladybug / Meerkat
- **Émulateur :** Pixel 6 API 34 (x86_64)
- **Contrôle de version :** Git (branche `main`)

---

*Chaoulid Hafssa — ENSA Marrakech — 2025-2026*
