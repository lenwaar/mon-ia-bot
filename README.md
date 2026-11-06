# 🤖 Mon IA bot

Assistant IA déployé sur **Cloudflare Workers** : recherche web, DeepSearch, vérification des faits, génération d'images et bot Telegram. Un seul fichier JavaScript, sans serveur à gérer.

## Fonctionnalités

- 💬 **Discussion avec recherche web automatique** dès que la question touche à l'actualité
- 🔎 **/deepsearch** : plusieurs requêtes, pages lues, synthèse avec sources numérotées
- 🧠 **/think** : mode réflexion avec un modèle de raisonnement
- ✅ **/verifie** : vérification des faits avec verdict (vrai, faux, partiel, invérifiable) et sources
- 📄 **/explique** et **/resume** : pour un lien, un article, une vidéo YouTube ou un message cité
- 🎨 **/imagine** : génération d'images ; analyse des images envoyées
- 🌍 **/traduis**, **/meteo**, **/devise**, **/calcul**, **/heure**, **/wiki**
- 😄 Modes **/fun** et **/serieux**, niveaux de puissance **/niveau 1-5**, mémoire de conversation
- 🎤 Messages vocaux transcrits (Telegram)

## Où l'utiliser

- **Interface web** : `/bot`
- **API JSON** : `POST /api/bot`
- **Telegram** : bot relié par webhook (groupes : mention ou réponse au bot)

## Architecture

```
Utilisateur (web / Telegram / API)
            |
   Cloudflare Worker (worker_ia.js)
            |
   +--------+----------+-----------+
   |        |          |           |
Workers AI  Recherche  Services    KV
(modèles)   web        de secours  (quotas, mémoire)
```

## Choix techniques

- **Serverless** : aucun serveur à maintenir, gratuit pour démarrer
- **Quotas par utilisateur** : protègent les limites des offres gratuites
- **Modération** des demandes avant traitement
- **Services de secours** : si le modèle principal échoue, une autre IA prend le relais
- **Choix automatique de l'outil** : le bot décide seul s'il doit chercher sur le web
- **Sécurité** : secret du webhook vérifié, contrôle de l'origine, protection contre les adresses internes lors de la lecture de pages

## Déploiement

1. Créer un Worker dans le tableau de bord Cloudflare (Workers & Pages)
2. Coller le contenu de `worker_ia.js` dans l'éditeur, puis **Deploy**
3. Ajouter le binding **AI** (Workers AI) dans Settings
4. Ouvrir `https://<ton-worker>/bot`

### Telegram (facultatif)

1. Créer un bot avec @BotFather et récupérer le token
2. Ajouter les secrets `TELEGRAM_BOT_TOKEN` et `TELEGRAM_SECRET`
3. Ouvrir une fois `https://<ton-worker>/api/bot/telegram/setup?cle=<TELEGRAM_SECRET>`

Variables facultatives : `TELEGRAM_OWNER_ID`, `TELEGRAM_AUTORISES`, `BOT_KV`.

## Limites

- Les modèles gratuits de Cloudflare sont moins puissants que les plus grands modèles du marché
- Pas d'accès en direct aux publications de X (API payante)

## Transparence

Projet développé avec l'aide d'un assistant IA (Claude), que j'ai relu, testé, déployé et que je maintiens.

## Licence

MIT
<img width="1131" height="963" alt="image" src="https://github.com/user-attachments/assets/d6bdff09-46de-4116-8982-c95ec7c8c141" />
<img width="1917" height="941" alt="image" src="https://github.com/user-attachments/assets/a8fd5064-8d46-4ea3-9688-a2f15524aa55" />

