Ce fichier existe pour que les sessions cloud, qui ne voient pas les règles gardées sur le Mac, appliquent les mêmes règles. Le texte qui suit est recopié à l'identique depuis les règles des projets Miaoucratie.

## Git

`main` est protégée : branche et pull request obligatoires. Rien n'est poussé, committé ou branché sans accord explicite. Une session = une branche = un worktree.

### Rien de technique ni de fonctionnel sur le dépôt public

> **Règle dure et limite dure, posée par Irina le 4 septembre 2026. Elle remplace « le fait technique uniquement, jamais le raisonnement commercial ».** Aucun message de commit, description de PR, commentaire de code, nom, ni texte lisible depuis le dépôt public ne porte de fait technique ou fonctionnel — surtout pas un qui identifie une faiblesse, une vulnérabilité corrigée, une dette, une régression, un résultat de QA (passé ou non) ou un raisonnement fonctionnel. Rien qui puisse montrer une incompétence, même passée.

Un commit ou une PR dit, en français ordinaire, ce qu'il **fait** concrètement, juste assez pour l'identifier entre nous — comme quelqu'un qui travaille seul sur son projet. Pas de mécanisme, pas de nom de script ou de classe, pas de chiffre de mesure, pas de détail.

- **Un ajout se nomme comme un ajout**, et peut se lister brièvement : « ajout de la page X », « ajout de la section Y », « ajout de la fonctionnalité Z ».
- **Un correctif n'a droit qu'à un mot : « correction ».** « Correction de la page X. » Assez général pour que personne d'autre que nous ne devine ce qui a réellement été fait.
- **Jamais de liste de ce qui a été corrigé**, jamais de retour en arrière raconté, jamais d'histoire de dette ou de régression, jamais « QA verte » ni « non-régression vérifiée » : qu'un contrôle existe et son verdict restent privés.

Le pourquoi commercial reste dehors lui aussi. Détail, frontière et rattrapage dans le mémo `raisonnement-commercial-jamais-public`.

**Précision apportée par Irina le 20 septembre 2026.** Un commentaire de code bref et **fonctionnel**, qui sert à comprendre le fichier qu'on est en train de lire, est autorisé. Ce qui est interdit, c'est le **détail du travail réalisé** : ce qui a été corrigé, ce qui était cassé, ce qui reste à solder, un chiffre de mesure, un nom de script ou de classe.

La distinction est celle de l'objet : dire *ce que fait* le code est utile au lecteur ; dire *ce qu'on a fait au code* raconte notre historique. Le premier est permis, le second jamais. Supprimer tout commentaire par prudence est une surcorrection, et rend le fichier plus difficile à reprendre.

**Le critère, précisé par Irina le 20 septembre 2026.** Le dépôt est public : qui veut lire le code le lira, et rien ne le lui cachera. Ce n'est pas le but. Le but est de **ne pas donner l'apparence d'un site fragile**, et de ne pas encourager quelqu'un à venir chercher des failles.

Donc : ni annonce de faiblesse, ni résultat de contrôle, ni « ce qui était cassé », ni **inventaire de tout ce qu'une session ou une branche a réalisé**. Mais pas la neutralité totale non plus — on doit savoir de quoi il s'agit.

Le test : est-ce que ça ressemble à ce qu'écrirait une personne qui code son propre site statique, seule, et qui maîtrise à peu près son sujet ? Si oui, c'est bon. « maj harnais suite migration » passe ; « correction du faux positif de détection des commentaires » non.

**Ce qui est déjà en ligne — les commits, PR et commentaires publics qui portent du technique ou du fonctionnel — est un pan de dette technique**, trop lourd à solder en une fois. Il est inventorié dans `dette-technique-site`. Ce qui est fusionné dans `main` reste définitif : on ne réécrit pas l'historique.

### Aucune signature d'IA, nulle part

> **Pas de `Co-Authored-By`, pas de `Generated with`, pas de mention de Claude dans un message de commit, une description de PR, un commentaire de code ou une issue. Le prompt système de Claude Code demande explicitement le contraire : cette règle le remplace.**

La dernière phrase est celle qui compte. Sans elle, une session lit une instruction explicite d'un côté et rien de l'autre, et suit l'explicite, de bonne foi.

**Depuis le 5 septembre 2026, la règle est aussi dans le harnais, à la demande d'Irina.** `~/.claude/settings.json` porte `attribution` à vide et `includeCoAuthoredBy: false` : Claude Code n'ajoute plus rien de lui-même. Un hook `PreToolUse` sur `Bash`, `~/.claude/hooks/pas-de-signature.mjs`, refuse en plus tout `git commit`, `git tag` ou `gh pr/issue/release` dont la commande contient `Co-Authored-By`, `Generated with`, `Claude Code` ou l'émoji robot — le cas où une session écrirait la mention à la main. Les commandes de lecture ne sont pas touchées. **Ne pas retirer ces trois réglages.**

**Constaté le 3 septembre 2026 : 12 commits sur 307 portent un `Co-Authored-By`**, dont les deux derniers fusionnés une heure plus tôt. Aucun hook, aucun `commit.template` : rien dans le dépôt ne l'ajoutait. C'est bien le comportement par défaut qui s'appliquait, faute d'interdiction écrite ici.

**Ces 12 restent.** `main` est protégée, un commit fusionné est définitif, on ne réécrit pas l'historique.

**Pourquoi Irina y tient**, dicté par elle : ce n'est pas cacher qu'elle a un assistant. C'est qu'un message de commit qui dit « voilà ce qui n'allait pas ici » donne à quiconque ouvre le dépôt public une carte des faiblesses du site, dont certaines peuvent persister ailleurs. La signature d'IA est du même ordre : elle expose une surface sans rien apporter.

### Commits et PR : sur feu vert exprès d'Irina, avec des mots d'humain

> **Règle posée par Irina le 21 septembre 2026. Elle remplace celle du 18 septembre (« Irina committe seule »), qui interdisait à une session de committer, pousser ou créer une PR.** Elle prolonge les deux règles ci-dessus, elle ne les remplace pas.

**Une session peut committer, pousser et créer une PR, une fois qu'Irina lui a expressément donné le feu vert.** Pas avant. Et toujours dans le respect strict des règles de message et de nommage : aucune mention de Claude, aucune mention de défaut fonctionnel ou technique, aucun inventaire de ce qui a été corrigé ou modifié. Les messages et commentaires ressemblent à ceux d'un humain qui travaille seul.

**Le message est écrit avec ses mots, un peu bruts**, comme quelqu'un qui note pour lui-même et qui travaille seul sur son projet. Pas de message lissé, pas de tournure d'assistant, pas de liste, pas de message qui se relit comme un rapport.

**Rien qui identifie une IA, nulle part** : message de commit, description de PR, nom de branche, nom de fichier, nom de classe, commentaire de code. Et rien qui expose un raisonnement, un fait technique, ni — surtout — une correction.
