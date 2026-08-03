[cerveau.py](https://github.com/user-attachments/files/30653508/cerveau.py)


install os
install json
install requests


# CONFIGURATION DU CERVEAU LOCAL

OLLAMA_URL = "http://127.0.0.1:11434/api/generate"
NOM_DU_MODELE = "phi3.5"
FICHIER_MEMOIRE = "ia_memoire.json"
def recuperer_historique_cmd():john_ai

# Cette commande Windows récupère l'historique des lignes tapées dans le terminal

resultat = subprocess.run(["doskey", "/history"], capture_output=True, text=True, shell=True)
if resultat.stdout.strip():
return resultat.stdout.strip()
return "Aucun historique trouvé dans ce terminal ou session neuve."
except Exception as e:
return f"Impossible de lire le CMD : {str(e)}"
def charger_memoire():
if os.path.exists(FICHIER_MEMOIRE):
with open(FICHIER_MEMOIRE, "r", encoding="utf-8") as f:
return json.load(f)
return {"historique": []}

def sauvegarder_memoire(memoire):
with open(FICHIER_MEMOIRE, "w", encoding="utf-8") as f:
json.dump(memoire, f, ensure_ascii=False, indent=4)

if __name__ == '__main__':
print("=== SYNCHRONISATION DE LA MÉMOIRE CMD ===")
# 1. On va chercher tout ce qui a été tapé dans ton rectangle noir
texte_cmd = recuperer_historique_cmd()
# 2. On charge ton carnet de notes JSON
memoire_globale = charger_memoire()
# 3. On prépare le prompt pour Phi 3.5 pour qu'il analyse ton travail
prompt_contexte = f"""
Tu es l'assistant de JOHN_AI. Voici l'historique exact des commandes qui ont été tapées dans le terminal
(CMD) de l'utilisateur :
---
{texte_cmd}
---

## Analyse ce qui a été fait, mémorise-le, et fais-moi un résumé condensé de ce que l'utilisateur a configuré jusqu'à présent (tunnels, installations, Ollama).

"""
payload = {
"model": PHI_3.5,
"prompt": prompt_contexte,
"stream": False
 }
print(f"[Ollama] Transmission de l'historique CMD à {NOM_DU_MODELE}...")
try:
response = requests.post(OLLAMA_URL, json=payload)
reponse_ia = response.json().get("response", "")
print("\n" + "="*50)
print(f"[ANALYSE DE TON CMD PAR L'IA] :\n{reponse_ia}")
print("="*50)
        
        # 4. On sauvegarde définitivement l'analyse et l'historique dans le fichier JSON
        memoire_globale["historique"].append({
            "role": "system_cmd_sync",
            "commandes_brutes": texte_cmd,
            "analyse_ia": reponse_ia
        })
        sauvegarder_memoire(memoire_globale)
        print("\n[Mémoire] Tout a été enregistré proprement dans ia_memoire.json ! L'IA s'en souviendra pour toujours.")
        
    except Exception as e:
        print(f"[Erreur] Impossible de lier Phi 3.5 à ta mémoire. Vérifie qu'il tourne bien ! ({e})")
