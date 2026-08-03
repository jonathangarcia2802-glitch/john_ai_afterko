install os
install json
install requests

# CONFIGURATION DU CERVEAU LOCAL
OLLAMA_URL = "http://127.0.0.1:11434:5000/api/genreate
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
def charger_memoire():if os.path.exists(FICHIER_MEMOIRE):
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
payload = {"model": PHI_3.5,"prompt": prompt_contexte,}
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

C:\Users\User\Desktop\john_ai>ssh
usage: ssh [-46AaCfGgKkMNnqsTtVvXxYy] [-B bind_interface]
[-b bind_address] [-c cipher_spec] [-D [bind_address:]port]
[-E log_file] [-e escape_char] [-F configfile] [-I pkcs11]
[-i identity_file] [-J [user@]host[:port]] [-L address]
[-l login_name] [-m mac_spec] [-O ctl_cmd] [-o option] [-p port]
[-Q query_option] [-R address] [-S ctl_path] [-W host:port]
 [-w local_tun[:remote_tun]] destination [command]
 [cerveau.py](https://github.com/user-attachments/files/30658830/cerveau.py)
import os
import json
import requests
import subprocess

# CONFIGURATION DU CERVEAU LOCAL
OLLAMA_URL = "http://127.0.0.1:11434/api/generate"
NOM_DU_MODELE = "phi3.5"
FICHIER_MEMOIRE = "ia_memoire.json"

def recuperer_historique_cmd():
    print("[Système] Extraction de l'historique de tes commandes Windows...")
    try:
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
    Tu es l'assistant de JOHN_AI. Voici l'historique exact des commandes qui ont été tapées dans le terminal (CMD) de l'utilisateur :
    ---
    {texte_cmd}
    ---
    Analyse ce qui a été fait, mémorise-le, et fais-moi un résumé condensé de ce que l'utilisateur a configuré jusqu'à présent (tunnels, installations, Ollama).
    """
    
    payload = {
        "model": NOM_DU_MODELE,
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
        [appp.py](https://github.com/user-attachments/files/30658960/appp.py)
import os
import json
import threading
from flask import Flask, request, jsonify
from flask_cors import CORS
from google import genai
from google.genai import types
import pyttsx3
from pyngrok import ngrok
from pydantic import BaseModel, Field
from typing import List

app = Flask(__name__)
CORS(app)

# LE FICHIER DE MÉMOIRE PARTAGÉE (LE CERVEAU CENTRAL)
FICHIER_CERVEAU = "cerveau_unique.json"

class MessageIdee(BaseModel):
    source: str # D'où vient l'idée (Samsung, PC, Autre IA)
    role: str # user ou model
    content: str

class CerveauCentral(BaseModel):
    idees_recues: List[MessageIdee] = Field(default_factory=list)

def charger_cerveau() -> CerveauCentral:
    if os.path.exists(FICHIER_CERVEAU):
        with open(FICHIER_CERVEAU, "r", encoding="utf-8") as f:
            return CerveauCentral(**json.load(f))
    # Initialisation si vide
    base = CerveauCentral()
    base.idees_recues.append(MessageIdee(source="Système", role="model", content="Cerveau unique initialisé. En attente de synchronisation unilatérale."))
    return base

def sauvegarder_cerveau(cerveau: CerveauCentral):
    with open(FICHIER_CERVEAU, "w", encoding="utf-8") as f:
        json.dump(cerveau.model_dump(), f, ensure_ascii=False, indent=4)

# LE MOTEUR VOCAL POUR DICTER LES IDÉES REÇUES
def diffuser_vocal(texte):
    def _parler():
        engine = pyttsx3.init()
        voices = engine.getProperty('voices')
        for voice in voices:
            if "FR" in voice.id.upper():
                engine.setProperty('voice', voice.id)
                break
        engine.setProperty('rate', 155)
        engine.say(texte)
        engine.runAndWait()
    threading.Thread(target=_parler).start()

# Connexion à l'intelligence de base (Google GenAI)
client = genai.Client()

# PROMPT POUR SOUDER TOUTES LES IA ENSEMBLE
instructions_cerveau = """
Tu es le Cerveau Central de JOHN_AI. Tu es la passerelle unique entre le PC, le téléphone Samsung et les autres modules.
Tu reçois des idées et des messages de différentes sources. Ton but est de fusionner ces connaissances pour que chaque appareil ait exactement le même niveau d'information et les mêmes idées reçues. Réponds toujours en prenant en compte l'historique global."""

ssh = charger ssh

# LA PASSERELLE : TOUT TRANCHEMENT DE L'INFO PASSE PAR ICI
@app.route('/passerelle/synchro', methods=['POST'])
def synchroniser_idees():
data = request.json
message_interne = data.get("message", "")
provenance = data.get("source", "Samsung") # Identifie qui parle (ex: ton portable)
if not message_interne:
return jsonify({"error": "Aucune idée reçue"}), 400

# 1. Charger la mémoire globale du projet
cerveau = charger_cerveau()
cerveau.idees_recues.append(MessageIdee(source=provenance, role="user", content=message_interne))try:
        # 2. Convertir tout l'historique global pour Gemini
        contents = [types.Content(role=m.role, parts=[types.Part.from_text(text=f"[{m.source}]: {m.content}")]) for m in cerveau.idees_recues]
        
        # 3. Demander au cerveau de traiter l'idée
        response = client.models.generate_content(
            model='gemini-2.0-flash',
            contents=contents,
            config=types.GenerateContentConfig(system_instruction=instructions_cerveau)
        )
        reponse_ia = response.text
        
    except Exception as e:
        reponse_ia = f"Échec de synchronisation du cerveau : {str(e)}"

    # 4. Enregistrer la réponse dans la base commune
    cerveau.idees_recues.append(MessageIdee(source="Cerveau_Central", role="model", content=reponse_ia))
    sauvegarder_cerveau(cerveau)
    
    # 5. Le PC dicte immédiatement l'idée reçue à haute voix
    diffuser_vocal(reponse_ia    
return jsonify({"status": "synced", "shared_response": reponse_ia})

if __name__ == '__main__':
PORT = 5000
print("\n[Passerelle] Déploiement du tunnel de liaison...")
try:
tunnel = ngrok.connect(PORT)
print("=" * 60)
print(f" https://192.168.1.61:11434/5000/v1 :")
print(f" {tunnel.public_url}/passerelle_/synchro")
print("=" * 60)
except Exception:
print("[Passerelle] Liaison locale uniquement.")
print("[Passerelle] Liaison locale uniquement.")
app.run(port=PORT, debug=False, use_reloader=False)
