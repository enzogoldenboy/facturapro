# Générateur de Factures

Interface web complète pour créer, personnaliser et exporter des factures professionnelles — sans serveur, sans installation, 100% dans le navigateur.

---

## Fonctionnalités

- **Calcul automatique** des totaux HT, TVA configurable (0–100%) et Total TTC en temps réel
- **Lignes dynamiques** — ajout, suppression et édition inline directement sur la prévisualisation
- **Logo entreprise** — upload PNG/SVG/JPG, affiché dans la facture et dans le PDF exporté avec ratio préservé
- **Prévisualisation live** — chaque modification se reflète instantanément sur la feuille
- **Export PDF A4** — mise en page propre avec barre accent, en-têtes colorés, badge statut et footer
- **Impression** — CSS print qui masque l'interface et laisse uniquement la feuille
- **Couleur accent personnalisable** — 5 swatches + color picker, appliqués uniquement sur la facture (barre, titre, tableau, total)
- **Multi-devises** — €, $, £, CHF
- **Statut** — badge "Payé" ou "En attente" visible sur la feuille et dans le PDF
- **Notes & conditions** — champ libre affiché en bas de facture si renseigné

---

## Utilisation

Le fichier est **standalone** — aucune dépendance à installer, aucun serveur requis.

```bash
# Ouvrir directement dans le navigateur
open generateur-facture.html
```

Ou simplement double-cliquer sur le fichier.

### Remplir une facture

1. **Votre entreprise** — nom, email, adresse, SIRET dans la sidebar gauche
2. **Client** — nom, email, adresse
3. **Facture** — numéro, statut, dates d'émission et d'échéance, TVA, devise
4. **Lignes** — cliquer sur les cellules du tableau pour éditer description, quantité et prix unitaire directement
5. **Logo** — uploader votre logo via la section dédiée (PNG recommandé, fond transparent)
6. **Style** — choisir la couleur accent qui sera appliquée sur la feuille
7. **Exporter** — bouton "Exporter en PDF" ou "Imprimer"

---

## Structure du fichier

```
generateur-facture.html
├── <head>
│   ├── Favicon (logo.png intégré en base64)
│   ├── Fonts : Syne (titres) + Space Grotesk (corps)
│   └── Scripts : jsPDF 2.5.1 + jsPDF-AutoTable 3.8.2 (CDN)
├── <aside class="sidebar">
│   ├── Logo app (fixe, intégré)
│   ├── Upload logo entreprise
│   ├── Champs : entreprise, client, facture
│   ├── Personnalisation couleur accent
│   └── Boutons export / impression
├── <main>
│   ├── Toolbar (prévisualisation + actions)
│   └── Invoice preview (éditable inline)
└── <script>
    ├── State : logoDataUrl, accentColor, rows[]
    ├── renderRows() / addRow() / delRow()
    ├── recalc() — totaux en temps réel
    ├── update() — sync sidebar → preview
    └── exportPDF() — génération jsPDF
```

---

## Personnalisation

### Couleurs disponibles par défaut

| Nom | Hex |
|-----|-----|
| Electric Violet | `#6366F1` |
| Neon Green | `#00DE76` |
| Sunburst Orange | `#FF5722` |
| Deep Coral | `#FF3B2F` |
| Black | `#0D0D0D` |

La couleur accent affecte : la barre supérieure, le titre "FACTURE", la bordure et les en-têtes du tableau, le bloc Total TTC — aussi bien dans la preview que dans le PDF exporté.

### Modifier les valeurs par défaut

Dans le `<script>`, modifier le tableau `rows` pour changer les lignes préremplies :

```js
let rows = [
  {desc: 'Votre prestation', qty: 1, price: 500, tva: 20},
];
```

Pour changer les infos entreprise par défaut, modifier les `value=""` des inputs correspondants dans le HTML.

---

## Dépendances (CDN)

| Librairie | Version | Usage |
|-----------|---------|-------|
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | Génération PDF |
| [jsPDF-AutoTable](https://github.com/simonbengtsson/jsPDF-AutoTable) | 3.8.2 | Tableau des lignes dans le PDF |
| [Google Fonts](https://fonts.google.com) | — | Syne + Space Grotesk |

Aucune autre dépendance. Pas de framework, pas de build tool.

---

## Compatibilité

Testé sur Chrome, Firefox, Edge (versions récentes). L'export PDF utilise l'API Canvas du navigateur pour le logo — nécessite un navigateur moderne.

---

## Licence

Usage libre — projet personnel / portfolio.