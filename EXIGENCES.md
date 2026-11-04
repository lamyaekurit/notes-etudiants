# Exigences de sécurité de l'application des notes
| # | Exigence : « Le système doit… » | Vérification | Étape du SDLC | Test |
# Exigences de sécurité de l'application des notes

| # | Exigence : « Le système doit… » | Vérification | Étape du SDLC | Test |
# Exigences de sécurité de l'application des notes

| # | Exigence : « Le système doit… » | Vérification | Étape du SDLC | Test |
|---|---|---|---|---|
| 1 | Le système doit empêcher l'injection SQL : une recherche par nom ne doit jamais être interprétée comme du code SQL (requêtes paramétrées). | pytest + `bandit -r . -x ./.venv,./test_app.py,./test_securite.py` | Développement (codage sécurisé), vérifié en Tests (SAST) | S1 : `test_recherche_resiste_a_l_injection` |
| 2 | Le système doit identifier l'utilisateur (jeton valide) avant toute modification de note, sinon répondre 401. | pytest | Exigences / Conception (authentification) | S2 : `test_modification_refusee_sans_identification` |
| 3 | Le système doit interdire à un étudiant de modifier une note, sinon répondre 403. | pytest | Conception (autorisation par rôle, STRIDE : E) | S3 : `test_modification_refusee_a_un_etudiant` |
| 4 | Le système doit autoriser un enseignant à modifier uniquement les notes de son propre module. | pytest | Conception (autorisation par rôle, STRIDE : E) | S4 : `test_modification_refusee_a_un_autre_module`<br>S6 : `test_modification_par_l_enseignant_du_module` |
| 5 | Le système doit valider la note reçue : un nombre entre 0 et 20, sinon répondre 400. | pytest | Développement (codage sécurisé) | S5 : `test_note_invalide_refusee` |
| 6 | Le système ne doit révéler aucun détail technique en cas de problème (erreur 500 générique). | pytest + revue de code | Développement (codage sécurisé, revue de code) | S7 : `test_erreur_sans_detail_technique` |