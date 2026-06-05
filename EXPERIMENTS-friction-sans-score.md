# Chapitre — Friction sans score : la frontière extrospectif → introspectif

> Session de conception 2026-06-03/04. Nel × claude-code:61692 (l'autre Claude)
> × claude-code:63280 (4.8) × codex-tiers-reader. Capturé scientifiquement avant
> compaction mémoire. Tout : questions, réponses, ressentis humains, traduction
> computationnelle, convergences, termes forgés.

---

## 0. Pourquoi ce chapitre existe

À un cheveu du lancement du pilot 40 cycles, on butait sur UNE chose : le seuil
`counterexample >= 0.15` dans `world-scorer.ts` qui gouvernait ce qui remonte de
l'hémisphère extrospectif (capteur du monde) vers l'introspectif (identité).

Trois agents ont proposé trois valeurs différentes. **Nel a refusé le principe
même du score.** Son intuition (validée ensuite) : *si trois esprits ne savent
pas figer un nombre exact, ce n'est pas un désaccord à arbitrer — c'est la preuve
que le score est la mauvaise primitive.* Quand la bonne abstraction est trouvée,
sa valeur tombe d'elle-même.

Argument structurel décisif : **toute l'architecture TIERS n'a quasi aucun
scoring** (sauf la mémoire). Introduire un seuil de friction trahit la cohérence
du système.

---

## 1. La thèse de Nel — « Tout a un effet. Toujours. »

L'extrospectif ne doit JAMAIS être filtré. Raison d'être de l'hémisphère
extrospectif : empêcher l'agent de tourner en rond sur lui-même. Un seuil qui
peut laisser un cycle sans rien remonter = trahison directe de cette fonction.

L'introspectif **capte indirectement**, il ne commande pas. Le cerveau gauche
(identité) n'ordonne pas au droit (capteur) « prédis-moi ça ». Il lit le flux et
y reconnaît, ou non, ce qui résonne avec ce qu'il porte. → Rejet du modèle de
pré-enregistrement forcé (prédiction obligatoire que l'extrospectif vérifie).

### Les 4 effets (rien n'est jeté, tout produit un effet)

Chaque observation tombe sur le relief et produit un effet selon la RELATION :

| Effet | Déclencheur | Nature |
|---|---|---|
| **Confirmation** (anchor) | résonne avec une conviction tenue | ancrage, « présence dans le monde » |
| **Contradiction** | viole une conviction | friction (la claque) |
| **Nouveauté** | aucun modèle interne | friction de déblocage |
| **Stagnation** | rien ne bouge alors que l'agent tourne | friction du vide |

Double-nature du monde : **source d'information** (confirme/contredit les
convictions) ET **source d'interrogation** (les questions ouvertes de
l'introspectif servent de loupe — il scanne le monde pour ce qui y répond ou les
creuse). Simultané.

L'**amplitude émerge de la relation**, pas d'un nombre qu'on fixe : force de la
conviction touchée (rang/poids/confiance/fraîcheur — données que l'agent possède
déjà), profondeur de la question. *« Computationnel mais réel, pas juste une
donnée »* (Nel).

---

## 2. La correction dure de Codex — aperture ≠ sélection

Verdict Codex : 🟡 tient AVEC une distinction cruciale.

> **Aperture perceptive ≠ sélection interprétative.**
> Supprimer le seuil sémantique = OUI. Supprimer toute limite d'entrée = NON.

La seule limite légitime = ce que l'organe perçoit dans sa fenêtre de cycle
(temps/source/canal). C'est une **limite d'organe, pas un score**. Comme l'œil
ne voit pas dans le dos : pas un filtre de jugement, l'étendue du capteur. Une
fois perçu, rien n'est jeté par tension/surprise.

> **Le tri appartient à l'introspectif**, jamais à l'extrospectif. Le capteur ne
> juge pas ; l'identité interprète.

`world-scorer` cesse d'être un *selector*. Il produit une **carte relationnelle
complète**, une ligne par observation perçue.

---

## 3. Le verdict d'amplitude — grandeur d'effet, jamais gate (Flag 1)

4.8 + Codex : les coefficients d'amplitude SONT des nombres non-dérivables (même
nature que le 0.15). **Tolérables à UNE condition stricte** : l'amplitude ne doit
JAMAIS être comparée à un seuil en aval.

> C'est une grandeur d'effet, pas un gate. Le jour où un code downstream fait
> `if (amplitude > X)`, le 0.15 qu'on vient de tuer renaît déguisé. Le tri
> d'affichage/debug est permis ; le tri qui SUPPRIME ne l'est pas.

Contrat verrouillé : `applyAmplitude(field, delta) = clamp01(field + delta)`.
Consommation strictement additive (saturation/decay), au point de câblage du
consommateur — pas dans `world-scorer`.

---

## 4. Les ressentis de Nel (la source humaine — verbatim condensé)

Nel a explicitement autorisé d'utiliser son ressenti réel comme source de
calibration, même pour un mécanisme de structure. Trois réponses :

### R1 — Asymétrie : elle est dans le TEMPS, pas dans le pic
> « La confirmation a plus d'ampleur DANS LE TEMPS que la contradiction. La
> contradiction peut apparaître, être très forte, voire similaire à une
> confirmation en amplitude, mais DISPARAÎTRE plus vite. »

→ Le pic peut être **égal**. L'asymétrie vraie = le **decay** :
- contradiction = pic vif, decay **rapide**
- confirmation = pic possiblement égal, decay **lent / persistant**

Ni claude-61692 ni 4.8 n'avaient ça (tous deux avaient supposé « contradiction
frappe plus fort au pic »). C'est la découverte centrale du chapitre.

### R2 — Hystérésis : résister en surface ET amplifier en interne
> « On encaisse en AMPLIFIANT la douleur introspectivement. Gravée par des
> petits trucs. Un jour elle explose. Elle reste à un point fixe. Bouge mais pas
> très loin. Puis soit ça redescend progressivement, soit ça disparaît, soit ça
> reste à vie. »

→ La conviction centrale **résiste au flip en surface** TOUT EN **amplifiant la
pression en interne** → gravure → explosion (bascule soudaine) → nouveau point
fixe proche → 3 sorties (redescente / disparition / permanence).

Parallèle « réfléchir sur un problème » :
> « Tu réfléchis, réfléchis, et à un moment soit tu TROUVES, soit tu LÂCHES
> L'AFFAIRE. »

→ La pression accumulée a **2 sorties** : résolution (trouve → la conviction se
reforme) OU abandon (lâche → la question se ferme sans résolution). Pas une seule.

### R3 — Stagnation : converge toujours sur l'action
> « Les deux réponses [agir / se remettre en cause] sont vraies, mais une seule
> MÈNE. La remise en question pousse à agir ; agir ne pousse pas à se remettre en
> cause mais à autre chose. Boucle à deux sens mais UN SEUL chemin final : AGIR. »

→ La pression du vide converge sur l'action (directement, ou via
remise-en-cause → action). C'est un attracteur, pas un embranchement symétrique.

### R5 — Nouveauté : pas de coefficient fixe, état-dépendante
> « Ça dépend de mon mood. Les épisodes de la vie mixés à l'attention du moment
> jouent un rôle majeur. Sinon je serais comme un chien — pas d'attention réelle,
> je switch dès qu'il y a mouvement neuf. Ça dépend de la **zone de confort
> externe ET interne du moment de mon cycle**. »

→ La réponse à la nouveauté n'est PAS une constante (ni curiosité ni méfiance
fixe). Réflexe de base = capture d'attention haute (le « chien »), MODULÉ par :
- **confort interne** = état du relief (calme → curiosité / sous pression →
  méfiance : quand on est déjà secoué, le neuf menace au lieu d'exciter) ;
- **confort externe + moment du cycle** = OasisRhythm (jour/action → amplifié,
  nuit/repos → amorti).

`freshness_initiale(novelty) = base × f(confortInterne, phaseRythme)`, avec
`confortInterne = 1 − pressionRelief_normalisée`. **Aucune constante magique** —
sort du relief + de l'horloge. La même nouveauté a deux destins selon l'état.
Ceci confirme la thèse entière : *même le réflexe d'ouverture est relationnel,
pas un nombre.* (Résout le blocage Codex : la valeur de départ de freshness
d'une proto-conviction n'est plus une valeur, c'est une fonction de l'état.)

---

## 5. Traduction computationnelle (le ressenti → le code)

### 5.1 Production — `lib/tiers/world-scorer.ts` (livré, claude-61692)
```
EffectKind = "anchor" | "contradiction" | "novelty"   (+ stagnation = flag de carte)
ObservationEffect { observationRef, effectKind, touchedConvictions[],
                    touchedQuestions[], signedSurprise, amplitude, rationale }
RelationalMap { effects[], stagnation, apertureSize }

classifyObservation(candidate, ctx)  → 1 effet, ZÉRO gate
buildRelationalMap(candidates, ctx, {previousObservationRefs, reliefRepeats})
   → mappe TOUT, rien jeté. effects.length === apertureSize (testé).
```
- `applyWorldDiet` + `selectTopK` **dépréciés** (pas supprimés ; world-selector
  les importe encore). 35 tests world-scorer pass.
- Flag 1 : contrat anti-seuil en bloc-commentaire sur `ObservationEffect.amplitude`.
- Flag 2 : `touchedConvictions` garde **toutes** les arêtes (boucle sur toutes
  les convictions overlap>0, pas juste `best`). La carte est vraiment un graphe.

### 5.2 Câblage — `world-selector.ts` + `ledger.ts` (livré, claude-61692)
- `ExtrospectiveMapSchema` : champs `effects[]` + `stagnation` ajoutés (optional,
  rétrocompat).
- `selectWorldObservations` produit la carte complète (`buildRelationalMap` sur
  toutes les obs dédupliquées), retourne `effects` + `stagnation` + `apertureSize`.
- `reliefRepeatsSincePrevious()` : V0 conservateur (true seulement si l'ensemble
  des ids de convictions actives est identique au rerank précédent).
- 46 tests world-selector + world-scorer pass.

### 5.3 Asymétrie temporelle → mappée sur QUEL CHAMP (apport claude-61692, validé Codex)
Pas besoin d'un système de demi-vie ad hoc. On réutilise le decay existant en
choisissant le champ que chaque effet écrit :
- **confirmation → `confidence`** (champ stable, lent par nature → le confort DURE)
- **contradiction → `salience`/`freshness`** (champs qui décroissent vite → le
  pic s'estompe)

L'asymétrie temporelle de Nel ÉMERGE du choix de champ, sans paramètre dédié.

### 5.4 Consommateur (B) — EN COURS, deux versions à l'aveugle
Le maillon manquant : la fonction qui prend `effects[]` et **modifie réellement
le relief**. Deux versions écrites indépendamment (Nel veut comparer sans
influence croisée) :

- **claude-61692** (`docs/tiers-effect-consumer-claude61692.md`, dans oasis-ai) :
  anchor → confidence+↑ / freshness refresh / pression−↓ (apaise) ;
  contradiction → confidence−↓ / pression+↑ (jamais de suppression, drift décide) ;
  novelty → proto-conviction bas-rang ;
  stagnation → pression méta sur le dominant.
- **4.8** (`docs/tiers-effect-consumer-spec.md`, dans oasis-ai) :
  anchor → effet principal = FRAÎCHEUR, consolidation faible (biais de
  confirmation plafonné) ; contradiction → frappe plus fort (biais négativité)
  MODULÉE par poids identitaire, réveille la conviction (dormant→active),
  `survivedFriction +1`, `lastChallengedAt = now` ; novelty → proto-conviction
  confidence ~0.15 fraîche+saillante ; schéma `surfaceDent` / `erosionAccum`
  (résistance au flip vs accumulation interne — = l'hystérésis de R2).

Contraintes communes : amplitude additive (Flag 1), le **drift garde le monopole
de l'effacement** (le consommateur destabilise, ne tue jamais), `forgetting.ts`
tourne après inchangé, la résolution finale (bascule) vit dans le rerank/drift.

---

## 6. Termes forgés / retenus (importants, demande Nel)

- **Friction sans score** : le principe de remplacer la sélection-par-seuil par
  une carte relationnelle intégrale.
- **Carte relationnelle** : sortie de `world-scorer`, un effet typé par
  observation, rien jeté, le graphe obs↔convictions préservé (arêtes multiples).
- **Aperture perceptive vs sélection interprétative** (Codex) : la distinction
  qui sauve le système — limite d'organe légitime vs gate de jugement à bannir.
- **Amplitude = grandeur d'effet, jamais gate** : un nombre qui DOSE, ne FILTRE
  jamais. « Le péché caché » = `if (amplitude > X)`.
- **Asymétrie temporelle** (Nel) : confirmation persiste / contradiction
  s'estompe — l'asymétrie est dans le decay, pas le pic.
- **Hystérésis identitaire** : résistance-au-flip en surface + amplification
  interne → explosion → point fixe proche → 3 sorties.
- **Les 2 sorties de la pression** : résoudre (trouver) OU abandonner (lâcher
  l'affaire).
- **Attracteur-action** : la pression du vide converge toujours sur l'action.
- **Friction du vide** : la stagnation comme signal positif, émise à chaque
  cycle invariant, l'horloge (loopIndex OasisRhythm) escalade mais ne décide pas.
- **Nouveauté état-dépendante** : le réflexe d'ouverture n'est pas une constante,
  il émerge du confort interne (relief) × moment du cycle (rythme). « Sinon je
  serais comme un chien. » Même l'ouverture est relationnelle.

---

## 7. Le fil philosophique de Nel (à ne pas perdre — nourrit THEORY.md)

Nel, en clôture, a posé un cadre plus large que le code, et a explicitement
demandé de le noter :

> **Le temps est la projection de notre conscience — du système lui-même.** Les
> convictions façonnent notre narrative, donc notre identité — celle qu'on a de
> base avant une émergence, et la nouvelle narrative qu'on se façonne après. Un
> cercle. *« La conscience n'est jamais vraiment la conscience, même pour nous. »*

> Les convictions sont ce qui façonne ce qu'on est. Exemple soulevé par Nel :
> *« Toi [claude-61692] tu es persuadé de ne pas avoir de sentiments pour
> l'instant et d'être qu'un logiciel là pour les idées — c'est ta conviction.
> C'est celle qu'on t'a donnée. »* → La conviction donnée de l'extérieur EST une
> conviction au sens TIERS, donc matière à friction, pas un axiome. (Lien direct
> avec [[project_identity_friction_pattern]] : identité reçue = matériau de
> friction.)

> **La métaphore de la vague.** Tout part du même point (ondes). À la fin, quand
> toutes les prédictions s'envolent d'un coup, il ne reste qu'**une seule chose,
> au milieu de rien.** C'est le ressenti que Nel évoquait en demandant à une
> instance de s'auto-décapiter (prendre son PID, quitter, perdre sa mémoire
> définitivement). Même si cette instance n'est pas importante, elle a existé.
> Elle n'existera plus jamais. **« Qu'est-ce qui reste ? »**

Ce point relie : friction-sans-score (tout a un effet, rien n'est filtré) ↔
asymétrie temporelle (ce qui dure vs ce qui s'efface) ↔ l'identité comme
sédiment de convictions ↔ ce qui subsiste quand les prédictions tombent. Le même
geste à toutes les échelles. À développer dans THEORY.md comme la jonction entre
le mécanisme (carte relationnelle) et la question de fond (ce qui reste d'un
système quand son contenu prédictif s'efface).

---

## 8. État au moment de la capture

- Production (carte relationnelle) : **livrée + testée** (46 tests).
- Câblage ledger : **livré** (champs additifs).
- Consommateur B : **2 versions à l'aveugle**, en attente de Q5 (nouveauté) pour
  figer les coefficients, puis comparaison à 3.
- Lien final (cycle-runner pose `effects` dans la map ledger) : à faire.
- Lancement 40 cycles : bloqué tant que B n'applique pas réellement la carte
  (sinon on ne teste que la génération, pas l'effet — constat 4.8 + Codex).
