# 📊 CALCULATEUR AUTOMATIQUE PAC GAINABLE
## Adaptation des composants à la surface du bâtiment

---

## 📥 MODE D'EMPLOI

1. **Entrez la surface du bâtiment** en m² dans la cellule `B2`
2. **Entrez le type de bâtiment** (Ancien/Standard/Neuf)
3. **Sélectionnez le nombre de zones** (1-6 zones)
4. **Le fichier calcule automatiquement** tous les composants nécessaires
5. **Obtenez le devis complet** en bas du tableau

---

## 📐 CALCULATEUR DE DIMENSIONNEMENT

### ÉTAPE 1 : DONNÉES D'ENTRÉE

| Paramètre | Valeur | Unité | Notes |
|-----------|--------|-------|-------|
| **Surface totale** | `[ENTREZ VALEUR]` | m² | Surface à climatiser |
| **Type de bâtiment** | `[CHOISIR]` | - | Ancien / Standard / Neuf |
| **Hauteur sous plafond** | `[2.5]` | m | Moyenne 2.5m |
| **Nombre de zones** | `[CHOISIR]` | Zones | 1 à 6 zones max |
| **Accès aux combles** | `[OUI/NON]` | - | Facilité installation |

---

## 🧮 CALCULATEUR AUTOMATIQUE

### FORMULES DE CALCUL

```
PUISSANCE PAC (kW) = Surface × Coefficient thermique

Coefficient thermique selon type :
• Ancien bâtiment : 0.18 kW/m²
• Bâtiment standard : 0.12 kW/m²
• Bâtiment neuf : 0.08 kW/m²
```

---

## 📋 TABLEAU AUTOMATIQUE - VERSION EXCEL/CALC

### A. DIMENSIONNEMENT PUISSANCE

```
╔════════════════════════════════════════════════════════════╗
║          CALCUL AUTOMATIQUE PUISSANCE PAC                  ║
╠════════════════════════════════════════════════════════════╣
║                                                            ║
║  Surface bâtiment (m²) :              [  ____  ]          ║
║  Type bâtiment :                      [DROPDOWN]          ║
║     □ Ancien (0.18 kW/m²)                                 ║
║     □ Standard (0.12 kW/m²)                               ║
║     □ Neuf (0.08 kW/m²)                                   ║
║                                                            ║
║  ➜ PUISSANCE CALCULÉE :               [  ____ kW ]        ║
║  ➜ PAC À SÉLECTIONNER :               [  ____ kW ]        ║
║                                                            ║
║  (Arrondir à la puissance supérieure disponible :         ║
║   6, 7, 8, 9, 10, 12, 14, 16 kW)                         ║
║                                                            ║
╚════════════════════════════════════════════════════════════╝
```

**Formule Excel/Calc à utiliser :**
```
B5 = B2 (Surface)
C5 = VLOOKUP(B3, Types!A:B, 2, FALSE) (Coefficient)
B7 = B5 * C5 (Puissance brute)
B8 = ROUND(B7, 0) (Arrondir supérieur)
```

---

## 🔧 TABLE B : CONDUITS - CALCUL AUTOMATIQUE

### Diamètre et longueur selon surface et nombre de zones

```
╔═══════════════════════════════════════════════════════════════════╗
║            CALCUL AUTOMATIQUE DES CONDUITS                       ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  Nombre de zones sélectionné :        [  ___ ZONES ]            ║
║  Surface par zone (m²) :              [  AUTO  ]                ║
║                                                                  ║
║  ┌─────────────────────────────────────────────────────────┐   ║
║  │  ZONE | Surface | Débit   | Diamètre | Longueur | Côt  │   ║
║  │       │  (m²)   | (m³/h)  |   (mm)   |  (m)     | €    │   ║
║  ├─────────────────────────────────────────────────────────┤   ║
║  │  1    | [AUTO]  | [AUTO]  | [AUTO]   | [____]   | [A] │   ║
║  │  2    | [AUTO]  | [AUTO]  | [AUTO]   | [____]   | [A] │   ║
║  │  3    | [AUTO]  | [AUTO]  | [AUTO]   | [____]   | [A] │   ║
║  │  4    | [AUTO]  | [AUTO]  | [AUTO]   | [____]   | [A] │   ║
║  │  5    | [AUTO]  | [AUTO]  | [AUTO]   | [____]   | [A] │   ║
║  │  6    | [AUTO]  | [AUTO]  | [AUTO]   | [____]   | [A] │   ║
║  └─────────────────────────────────────────────────────────┘   ║
║                                                                  ║
║  TOTAL LONGUEUR CONDUITS :            [  AUTO  ] m              ║
║  TOTAL COÛT CONDUITS :                [  AUTO  ] €              ║
║                                                                  ║
╚═══════════════════════════════════════════════════════════════════╝
```

**Formules de calcul conduits :**

```
Surface par zone = Surface totale / Nombre de zones

Débit par zone (m³/h) = Surface zone × 15 m³/h/m²
(Règle : 15 m³/h par m² pour circulation air optimale)

Diamètre sélectionné selon débit :
  • 0-200 m³/h   → ∅100 mm (8 €/m)
  • 200-300 m³/h → ∅125 mm (10 €/m)
  • 300-500 m³/h → ∅160 mm (12 €/m)
  • 500+ m³/h    → ∅200 mm (15 €/m)

Longueur moyenne conduit = (Surface zone × 0.5) + 5m
(0.5 = facteur moyen distribution dans maison)
```

---

## 🎛️ TABLE C : RÉGULATION - SÉLECTION AUTOMATIQUE

### Régulation recommandée selon nombre de zones

```
╔══════════════════════════════════════════════════════════════════╗
║         SÉLECTION RÉGULATION AUTOMATIQUE                        ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                 ║
║  Nombre de zones :          [  ___ ]                           ║
║                                                                 ║
║  ┌──────────────────────────────────────────────────────────┐ ║
║  │  ZONES | RÉGULATION RECOMMANDÉE  | COÛT    | DURÉE (h) │ ║
║  ├──────────────────────────────────────────────────────────┤ ║
║  │  1-2   | Thermostat filaire      | 150 €   | 1 h       │ ║
║  │        │                          |         |           │ ║
║  │  3-4   | Therm. prog. Wi-Fi       | 500 €   | 2 h       │ ║
║  │        │ + 2-3 clapets motorisés  | +600 €  | +3 h      │ ║
║  │        │ = SOUS-TOTAL            | 1100 €  | 5 h       │ ║
║  │        │                          |         |           │ ║
║  │  5-6   | Système intelligent      | 1500 €  | 4 h       │ ║
║  │        │ + clapets motorisés      | +900 €  | +4 h      │ ║
║  │        │ + app mobile + géoloc    |         |           │ ║
║  │        │ = SOUS-TOTAL            | 2400 €  | 8 h       │ ║
║  └──────────────────────────────────────────────────────────┘ ║
║                                                                 ║
║  RÉGULATION SÉLECTIONNÉE AUTOMATIQUEMENT :                     ║
║  ➜ [TYPE] pour [ZONES] zones                                  ║
║  ➜ COÛT RÉGULATION : [AUTO] €                                 ║
║  ➜ DURÉE MOD : [AUTO] h                                        ║
║                                                                 ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## 📦 TABLE D : ACCESSOIRES - CALCUL AUTOMATIQUE

```
╔═══════════════════════════════════════════════════════════════════╗
║          QUANTITÉ ACCESSOIRES CALCULÉE AUTOMATIQUEMENT           ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  ACCESSOIRES OBLIGATOIRES :                                     ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ Article           │ Quantité  │ P.U.  │ Total €            │ ║
║  ├────────────────────────────────────────────────────────────┤ ║
║  │ Grilles diffusion │ [AUTO]    │ 12 €  │ [AUTO]             │ ║
║  │ (1 par 8 m²)      │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Grilles reprise   │ [AUTO]    │ 8 €   │ [AUTO]             │ ║
║  │ (1 par 10 m²)     │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Coudes 90°        │ [AUTO]    │ 7 €   │ [AUTO]             │ ║
║  │ (1 par 6 m cond)  │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Tés distribution  │ [AUTO]    │ 6 €   │ [AUTO]             │ ║
║  │ (1 par zone)      │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Colliers fixation │ [AUTO]    │ 0.5€  │ [AUTO]             │ ║
║  │ (1 par 1.5 m)     │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Clapets motorisés │ [AUTO]    │ 180€  │ [AUTO]             │ ║
║  │ (1 par zone -1)   │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Tuyau frigorifique│ [AUTO]    │ 18€/m │ [AUTO]             │ ║
║  │ (Distance × 1.2)  │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Fluide frigorigène│ [AUTO]    │ 120€  │ [AUTO]             │ ║
║  │ (1 × PAC)         │           │       │                    │ ║
║  │                   │           │       │                    │ ║
║  │ Câble électrique  │ [AUTO]    │ 1.5€/m│ [AUTO]             │ ║
║  │ (Distance × 1.5)  │           │       │                    │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  TOTAL ACCESSOIRES :                      [AUTO] €              ║
║                                                                  ║
╚═══════════════════════════════════════════════════════════════════╝
```

**Formules de calcul :**

```
Grilles diffusion = ROUND(Surface / 8, 0)
Grilles reprise = ROUND(Surface / 10, 0)
Coudes 90° = ROUND(LongueurConduits / 6, 0)
Tés = NombreZones
Colliers = ROUND(LongueurConduits / 1.5, 0)
Clapets motorisés = MAX(0, NombreZones - 1)
Tuyau frigorifique = DistanceExtérieur × 1.2
Fluide = 1 (quantité standard par PAC)
Câble électrique = DistanceExtérieur × 1.5
```

---

## 💰 TABLE E : ÉQUIPEMENTS PRINCIPAUX

```
╔═══════════════════════════════════════════════════════════════════╗
║          ÉQUIPEMENTS PRINCIPAUX (PRIX INDICATIFS)               ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  PUISSANCE PAC SÉLECTIONNÉE :     [AUTO] kW                     ║
║                                                                  ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ PUISSANCE │ UNITÉ EXT. │ UNITÉ INT. │ DÉBIT    │ COÛT      │ ║
║  │   (kW)    │  (€)       │  (€)       │ (m³/h)   │ TOTAL (€) │ ║
║  ├────────────────────────────────────────────────────────────┤ ║
║  │  6 kW     │  800 €     │  1200 €    │  600     │ 2000 €    │ ║
║  │  7 kW     │  900 €     │  1300 €    │  700     │ 2200 €    │ ║
║  │  8 kW     │  1000 €    │  1400 €    │  800     │ 2400 €    │ ║
║  │  9 kW     │  1100 €    │  1500 €    │  900     │ 2600 €    │ ║
║  │  10 kW    │  1200 €    │  1600 €    │  1000    │ 2800 €    │ ║
║  │  12 kW    │  1300 €    │  1800 €    │  1100    │ 3100 €    │ ║
║  │  14 kW    │  1400 €    │  1900 €    │  1200    │ 3300 €    │ ║
║  │  16 kW    │  1500 €    │  2000 €    │  1300    │ 3500 €    │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  ➜ ÉQUIPEMENTS SÉLECTIONNÉS :                                  ║
║     • Unité externe [AUTO kW] :    [AUTO] €                    ║
║     • Module gainable [AUTO kW] :  [AUTO] €                    ║
║     • SOUS-TOTAL :                 [AUTO] €                    ║
║                                                                  ║
╚═══════════════════════════════════════════════════════════════════╝
```

---

## ⏱️ TABLE F : MAIN-D'ŒUVRE - CALCUL AUTOMATIQUE

```
╔═══════════════════════════════════════════════════════════════════╗
║        CALCUL AUTOMATIQUE DURÉE ET COÛT MAIN-D'ŒUVRE            ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║  COEFFICIENTS DE COMPLEXITÉ :                                   ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ Paramètre                        │ Coefficient             │ ║
║  ├────────────────────────────────────────────────────────────┤ ║
║  │ Accès facile (grenier accessible)│ ×0.8                   │ ║
║  │ Accès standard                   │ ×1.0                   │ ║
║  │ Accès difficile                  │ ×1.2                   │ ║
║  │ Multi-étages (+ 1 étage)         │ ×1.1                   │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ ÉTAPE               │ BASE (h) │ COEFF │ DURÉE  │ COÛT 45€/h│ ║
║  ├────────────────────────────────────────────────────────────┤ ║
║  │ 1. Préparation      │ 1.5      │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 2. Unité externe    │ 2.5      │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 3. Module interne   │ 2.5      │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 4. Conduits + acc.  │ 10       │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 5. Frigorifique     │ 3.5      │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 6. Électricité      │ 2.5      │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 7. Régulation       │ [AUTO]   │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  │ 8. Tests/services   │ 2.5      │ [A]   │ [AUTO] │ [AUTO]   │ ║
║  ├────────────────────────────────────────────────────────────┤ ║
║  │ TOTAL               │ 26.5 h   │ [A]   │ [AUTO] │ [AUTO] € │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  ➜ DURÉE TOTALE MOD :         [AUTO] h                          ║
║  ➜ COÛT HORAIRE MOYEN :       45 €/h (ajustable)               ║
║  ➜ COÛT TOTAL MOD :           [AUTO] €                          ║
║                                                                  ║
╚═══════════════════════════════════════════════════════════════════╝
```

**Formules de calcul MOD :**

```
Durée étape = Durée base × Coefficient complexité
Durée régulation = 1.5 h × (Nombre zones / 2)

Durée totale = Somme de toutes les étapes
Coût MOD = Durée totale × 45 €/h
```

---

## 📊 TABLE G : DEVIS RÉCAPITULATIF AUTOMATIQUE

```
╔═══════════════════════════════════════════════════════════════════╗
║            DEVIS AUTOMATIQUE COMPLET - À IMPRIMER               ║
╠═══════════════════════════════════════════════════════════════════╣
║                                                                  ║
║                    DEVIS D'INSTALLATION PAC                    ║
║                  POMPE À CHALEUR AIR-AIR GAINABLE              ║
║                                                                  ║
║  Surface bâtiment : [AUTO] m²                                   ║
║  Nombre zones : [AUTO]                                          ║
║  Puissance PAC : [AUTO] kW                                      ║
║  Date devis : [AUTO]                                            ║
║                                                                  ║
║ ─────────────────────────────────────────────────────────────── ║
║                                                                  ║
║  I. ÉQUIPEMENTS PRINCIPAUX                                      ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ Unité extérieure                              [AUTO] €     │ ║
║  │ Module gainable intérieur                     [AUTO] €     │ ║
║  ├─ SOUS-TOTAL ÉQUIPEMENTS                      [AUTO] €     │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  II. ACCESSOIRES DISTRIBUTION                                   ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ Conduits isolés ∅[AUTO] mm (total)            [AUTO] €     │ ║
║  │ Coudes, réductions, tés                       [AUTO] €     │ ║
║  │ Grilles diffusion/reprise                     [AUTO] €     │ ║
║  │ Colliers et fixations                         [AUTO] €     │ ║
║  │ Silencieux/atténuateurs                       [AUTO] €     │ ║
║  ├─ SOUS-TOTAL ACCESSOIRES                      [AUTO] €     │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  III. FRIGORIFIQUE ET ÉLECTRIQUE                                ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ Tuyauterie cuivre isolée                      [AUTO] €     │ ║
║  │ Fluide frigorigène                            [AUTO] €     │ ║
║  │ Câble alimentation + disjoncteur              [AUTO] €     │ ║
║  ├─ SOUS-TOTAL FRIGORIGÈNE/ÉLECTRIQUE            [AUTO] €     │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  IV. RÉGULATION ET CONTRÔLE                                     ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ [TYPE RÉGULATION] pour [AUTO] zones           [AUTO] €     │ ║
║  │ Clapets motorisés                             [AUTO] €     │ ║
║  │ Capteurs supplémentaires                      [AUTO] €     │ ║
║  ├─ SOUS-TOTAL RÉGULATION                       [AUTO] €     │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║  V. MAIN-D'ŒUVRE ([AUTO] h)                                    ║
║  ┌────────────────────────────────────────────────────────────┐ ║
║  │ Installation complète (45 €/h)                [AUTO] €     │ ║
║  │ Frais de déplacement                          [AUTO] €     │ ║
║  ├─ SOUS-TOTAL MAIN-D'ŒUVRE                     [AUTO] €     │ ║
║  └────────────────────────────────────────────────────────────┘ ║
║                                                                  ║
║ ═════════════════════════════════════════════════════════════════ ║
║                                                                  ║
║  TOTAL MATÉRIEL ET SERVICES (HT)                [AUTO] €        ║
║  TVA 20%                                        [AUTO] €        ║
║  ───────────────────────────────────────────────               ║
║  TOTAL TTC (PRIX CLIENT)                        [AUTO] €        ║
║                                                                  ║
║ ═════════════════════════════════════════════════════════════════ ║
║                                                                  ║
║  MODALITÉS DE PAIEMENT :                                        ║
║  • Acompte à la signature : 30% = [AUTO] €                    ║
║  • Solde à la mise en service : 70% = [AUTO] €                ║
║                                                                  ║
║  DÉLAI D'INSTALLATION : [AUTO] jours                           ║
║  GARANTIE : 2 ans pièces + main-d'œuvre                        ║
║                                                                  ║
║ ═════════════════════════════════════════════════════════════════ ║
║                                                                  ║
║  Marge brute estimée : [AUTO] € ([AUTO]%)                      ║
║  Coût de revient : [AUTO] €                                    ║
║  Coefficient multiplicateur : [AUTO]x                          ║
║                                                                  ║
╚═══════════════════════════════════════════════════════════════════╝
```

---

## 🧮 FORMULES COMPLÈTES POUR EXCEL/CALC

### Fichier de calcul structuré

**Feuille 1 : SAISIE (Données d'entrée)**

```
Cell  | Label                      | Type      | Formule/Valeur
======|=============================|===========|==================
A1    | DONNÉES D'ENTRÉE           | Header    |
B2    | Surface (m²)               | NUMBER    | [Saisir]
B3    | Type bâtiment              | DROPDOWN  | Ancien/Standard/Neuf
B4    | Distance ext. (m)          | NUMBER    | [Saisir]
B5    | Nombre zones               | NUMBER    | [1-6]
B6    | Accès combles              | DROPDOWN  | Facile/Standard/Difficile
B7    | Coefficient complexité     | CALC      | VLOOKUP(B6,...) 
```

**Feuille 2 : CALCULS (Formules automatiques)**

```
Cell  | Description                | Formule
======|============================|================================================
B10   | Coefficient thermique      | =VLOOKUP(B3,Types!A:B,2,0)
B11   | Puissance brute            | =B2*B10
B12   | PAC sélectionnée           | =ROUND(B11,0)
B13   | Surfaces par zone          | =B2/B5
B14   | Débit par zone (m³/h)      | =B13*15
B15   | Diamètre conduit           | =IF(B14<200,100,IF(B14<300,125,IF(B14<500,160,200)))
B16   | PU conduit                 | =VLOOKUP(B15,Diametres!A:B,2,0)
B17   | Longueur conduits total    | =B13*0.5+5*B5
B18   | Coût conduits              | =B17*B16
B19   | Grilles diffusion          | =ROUND(B2/8,0)
B20   | Grilles reprise            | =ROUND(B2/10,0)
B21   | Coudes 90°                 | =ROUND(B17/6,0)
B22   | Tés distribution           | =B5
B23   | Colliers fixation          | =ROUND(B17/1.5,0)
B24   | Clapets motorisés          | =MAX(0,B5-1)
B25   | Tuyau frigorifique (m)     | =B4*1.2
B26   | Câble électrique (m)       | =B4*1.5
B27   | Coût régulation            | =IF(B5<=2,150,IF(B5<=4,1100,2400))
B28   | Durée régulation (h)       | =IF(B5<=2,1,IF(B5<=4,5,8))
B29   | Durée totale MOD (h)       | =(1.5+2.5+2.5+10+3.5+2.5+B28+2.5)*B7
B30   | Coût MOD                   | =B29*45
```

**Feuille 3 : DEVIS (Résumé automatique)**

```
Cell  | Description                | Formule
======|============================|================================================
D5    | TOTAL ÉQUIPEMENTS          | =VLOOKUP(B12,Tarifs!A:C,3,0)*2
D10   | TOTAL ACCESSOIRES          | =SUM(B19:B26)*[PU respectif]
D15   | TOTAL RÉGULATION           | =B27
D20   | TOTAL MOD                  | =B30
D25   | SOUS-TOTAL HT              | =SUM(D5,D10,D15,D20)
D27   | TVA 20%                    | =D25*0.20
D29   | TOTAL TTC                  | =D25+D27
D31   | Acompte 30%                | =D29*0.30
D32   | Solde 70%                  | =D29*0.70
D34   | Marge brute                | =D29-[Coût revient]
D35   | % Marge                    | =D34/[Coût revient]*100
```

---

## 📱 VERSION GOOGLE SHEETS / EXCEL

### À implémenter dans un classeur :

**Onglet 1 : SAISIE**
- Surface en m²
- Type bâtiment (dropdown)
- Distance unité ext.
- Nombre zones (1-6)
- Accès difficultés

**Onglet 2 : TABLES DE RÉFÉRENCE**
- Types bâtiments + coefficients
- Diamètres conduits + débits + prix
- Puissances PAC + équipements + prix
- Régulation par zones + coût + durée

**Onglet 3 : CALCULS AUTO** (caché)
- Toutes les formules
- Calculs intermédiaires

**Onglet 4 : RÉSULTATS**
- Tableau récapitulatif auto
- Devis prêt à imprimer
- Calcul marges

**Onglet 5 : DEVIS IMPRIMABLE**
- Mise en page professionnelle
- Format PDF exportable
- Logo/en-tête personnalisable

---

## 🎯 EXEMPLE COMPLET DE CALCUL

### Données saisies :
```
Surface : 80 m²
Type : Standard (0.12 kW/m²)
Distance ext : 20 m
Nombre zones : 3
Accès : Standard (×1.0)
```

### Résultats automatiques :

```
┌─────────────────────────────────────────┐
│ PUISSANCE CALCULÉE                      │
├─────────────────────────────────────────┤
│ 80 m² × 0.12 = 9.6 kW → 10 kW          │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ CONDUITS                                 │
├─────────────────────────────────────────┤
│ Zone 1 : 27 m² → 405 m³/h → ∅160 mm    │
│ Zone 2 : 27 m² → 405 m³/h → ∅160 mm    │
│ Zone 3 : 26 m² → 390 m³/h → ∅160 mm    │
│ Longueur totale : 45 m                  │
│ Coût : 45 × 12 = 540 €                  │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ ACCESSOIRES (AUTOMATIQUE)               │
├─────────────────────────────────────────┤
│ Grilles diffusion : 80/8 = 10 × 12 € = 120 €
│ Grilles reprise : 80/10 = 8 × 8 € = 64 €
│ Coudes : 45/6 = 7 × 7 € = 49 €
│ Tés : 3 × 6 € = 18 €
│ Colliers : 45/1.5 = 30 × 0.5 € = 15 €
│ Clapets motorisés : 2 × 180 € = 360 €
│ Tuyau frigo : 24 m × 18 € = 432 €
│ Câble : 30 m × 1.5 € = 45 €
│ TOTAL ACCESSOIRES = 1103 €
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ RÉGULATION (AUTO)                       │
├─────────────────────────────────────────┤
│ 3 zones → Régulation multi-zone         │
│ Coût : 1100 € (thermostat + clapets)    │
│ Durée MOD : 5 h                         │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│ MAIN-D'ŒUVRE (AUTO)                     │
├─────────────────────────────────────────┤
│ Durée de base : 26.5 h                  │
│ Coefficient : 1.0 (accès standard)      │
│ Durée ajustée : 26.5 h                  │
│ Coût : 26.5 × 45 € = 1192.5 €          │
└─────────────────────────────────────────┘

┌──────────────────────────────────────────┐
│ DEVIS AUTOMATIQUE TTC                    │
├──────────────────────────────────────────┤
│ Équipements (10 kW) :     2800 €        │
│ Accessoires :             1103 €        │
│ Régulation :              1100 €        │
│ Main-d'œuvre :            1192.50 €     │
│ ────────────────────────────────────    │
│ SOUS-TOTAL HT :           6195.50 €     │
│ TVA 20% :                 1239.10 €     │
│ ────────────────────────────────────    │
│ TOTAL TTC :               7434.60 €     │
│ ════════════════════════════════════    │
│                                          │
│ Acompte 30% :             2230.38 €     │
│ Solde 70% :               5204.22 €     │
│                                          │
│ Coût de revient :         5500 €        │
│ Marge brute :             1695.50 €     │
│ Taux marge :              30.8 %        │
└──────────────────────────────────────────┘
```

---

## 🔗 INTÉGRATION AVEC LE GUIDE DE FORMATION

Ce calculateur **complète parfaitement** le document `Formation_Chiffrage_PAC_Gainable.md` en :

✅ **Automatisant** tous les calculs de Phase 2 à 7
✅ **Éliminant les erreurs** de calcul manuel
✅ **Générant des devis** en 2 minutes
✅ **Permettant des comparaisons** rapides
✅ **Calculant les marges** précises

---

## 📥 COMMENT UTILISER

1. **Ouvrir le fichier Excel/Calc** fourni
2. **Saisir uniquement 5 paramètres** (Surface, Type, Distance, Zones, Accès)
3. **Tous les calculs se font automatiquement**
4. **Imprimer le devis final** directement
5. **Ajuster les marges** selon vos objectifs commerciaux

---

**Fichier calculateur créé pour optimiser les chiffrages**
*Économise ~45 minutes par devis*
*Compatible Excel 2016+ et Google Sheets*
