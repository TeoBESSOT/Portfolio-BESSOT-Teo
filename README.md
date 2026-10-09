# Portfolio QLIO — GitHub Pages + Supabase

Version simple : un seul fichier `index.html`, hébergé gratuitement sur GitHub Pages. Supabase gère la connexion et stocke les fiches.

## 1. Créer le projet Supabase
1. Crée un projet sur https://supabase.com/
2. Ouvre **SQL Editor**.
3. Copie-colle tout le contenu de `supabase/schema.sql`, puis clique sur **Run**.

## 2. Créer ton compte administrateur
1. Dans Supabase, va dans **Authentication → Users → Add user**.
2. Crée ton compte avec ton e-mail et un mot de passe.
3. Copie l'UUID de ce compte.
4. Dans **SQL Editor**, exécute cette requête en remplaçant l'UUID :

```sql
insert into public.admin_users (user_id)
values ('COLLE-ICI-LE-UUID-DE-TON-COMPTE');
```

Ne crée pas de bouton d'inscription public : ton compte doit être créé depuis le tableau de bord Supabase.

## 3. Relier le site à Supabase
Dans Supabase, ouvre **Project Settings → API** (ou **Data API** selon l'interface) et copie :
- l'URL du projet ;
- la clé **publishable** (ou l'ancienne clé `anon`).

Dans `index.html`, trouve ces deux lignes près de la fin du fichier et remplace les valeurs :

```js
const SUPABASE_URL = 'COLLE_ICI_URL_SUPABASE';
const SUPABASE_PUBLISHABLE_KEY = 'COLLE_ICI_CLE_PUBLISHABLE_SUPABASE';
```

La clé publishable/anon est prévue pour être utilisée dans un site public, à condition que les politiques RLS soient en place. **Ne mets jamais la clé `service_role` ou une clé secrète dans `index.html`.**

## 4. Publier sur GitHub Pages
1. Sur GitHub, crée un dépôt public, par exemple `portfolio-qlio`.
2. Ajoute `index.html`, le dossier `supabase` et `README.md` au dépôt.
3. Dans le dépôt, ouvre **Settings → Pages**.
4. Sous **Build and deployment**, choisis **Deploy from a branch**.
5. Choisis la branche `main` et le dossier `/(root)`, puis **Save**.
6. Attends la publication : GitHub affichera l'adresse publique du site dans cette page.

Tu peux modifier `index.html` directement sur GitHub : le site se mettra à jour après quelques instants.

## 5. Tester
- Ouvre le lien GitHub Pages dans une fenêtre privée : les fiches doivent être visibles sans connexion.
- Clique sur **Connexion admin** et connecte-toi avec ton compte Supabase : les champs deviennent modifiables.
- Enregistre une fiche et recharge la page pour vérifier que le changement est conservé.

## À savoir
- Les titres sont des exemples : remplace-les par tes 28 véritables apprentissages critiques.
- Les visiteurs peuvent lire tout le contenu : ne publie pas d'informations confidentielles.
- L'accès à l'édition est contrôlé par Supabase, pas par le fait de masquer les boutons du site. Les règles RLS de `schema.sql` protègent aussi la base de données.
- Le dépôt GitHub est public : son code source sera visible. N'y mets aucun mot de passe ni clé secrète.
