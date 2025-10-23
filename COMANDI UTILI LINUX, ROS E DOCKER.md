
├── bin/        → comandi base del sistema (es. ls, cp, mv)
├── etc/        → file di configurazione
├── home/       → directory degli utenti (es. /home/mario)
├── opt/        → programmi opzionali installati manualmente
├── usr/        → programmi e librerie standard del sistema
├── var/        → file variabili (log, cache)
├── tmp/        → file temporanei

⚙️ 2️⃣ Comandi di base per muoversi
Comando	Significato	Esempio

pwd	Mostra dove sei (Print Working Directory)	pwd → /home/mario

ls	Lista file/cartelle	ls -l (dettagli), ls -a (anche file nascosti)

cd	Cambia directory	cd /home/mario/ros_ws

mkdir	Crea una nuova cartella	mkdir new_folder

rm	Elimina file o cartelle	rm file.txt o rm -r folder/

cp	Copia file/cartelle	cp a.txt b.txt

mv	Sposta o rinomina	mv 
vecchio.txt nuovo.txt

cat	Visualizza il contenuto di un file	cat README.md

clear	Pulisce il terminale	—
📦 3️⃣ Gestione pacchetti: apt e apt-get
🔹 apt = Advanced Package Tool

È il gestore di pacchetti di Ubuntu/Debian.
Serve per installare, aggiornare o rimuovere software.
Comando	Descrizione

sudo apt update	Aggiorna la lista dei pacchetti disponibili

sudo apt upgrade	Installa gli aggiornamenti disponibili

sudo apt install <pacchetto>	Installa un pacchetto (es. sudo apt install git)

sudo apt remove <pacchetto>	Disinstalla un pacchetto

sudo apt purge <pacchetto>	Disinstalla e rimuove anche i file di configurazione

apt search <nome>	Cerca un pacchetto

apt show <nome>	Mostra informazioni su un pacchetto

👉 Differenza tra apt e apt-get:

    apt è una versione più “user-friendly” (per terminale interattivo)

    apt-get è più adatto per script o Dockerfile (non mostra barre di progresso, ecc.)

📂 4️⃣ Directory importanti per ROS e programmi
Directory	Descrizione

/opt	Programmi opzionali installati globalmente (es. /opt/ros/humble)

/usr/bin	Comandi principali del sistema (es. ls, python3, colcon)

/etc	File di configurazione del sistema

/home/<utente>	Dati dell’utente, es. workspace ROS, documenti, ecc.

/var/log	Log del sistema e applicazioni

/tmp	File temporanei (svuotata a ogni riavvio)

👉 Esempio pratico con ROS:
Quando installi ROS Humble:

/opt/ros/humble/
├── bin/        → comandi ROS (es. ros2)
├── lib/        → librerie
├── share/      → pacchetti installati
└── setup.sh    → script per attivare ROS

Quindi, per “attivare” ROS nel terminale:

source /opt/ros/humble/setup.bash

🔧 5️⃣ Gestione file e permessi
Comando	Descrizione
sudo	Esegui come amministratore (superuser)

chmod	Cambia permessi di un file (chmod +x script.sh)

chown	Cambia il proprietario di un file

ls -l	Mostra i permessi (rwx) e i proprietari

whoami	Mostra l’utente corrente

ps aux	Mostra tutti i processi attivi

kill <pid>	Termina un processo

🧰 6️⃣ Utili per ROS e sviluppo
Comando	Serve a...

colcon build	Compila i pacchetti ROS nel tuo workspace

source install/setup.bash	Attiva l’ambiente del tuo workspace

ros2 run <pkg> <exe>	Lancia un nodo ROS

ros2 topic list	Elenca i topic attivi

ros2 node list	Elenca i nodi ROS 
attivi

ros2 launch <pkg><file.launch.py>	Esegue un launch file

🐋 7️⃣ Comandi Docker fondamentali
Comando	Descrizione

docker build -t nome_immagine .	Crea un’immagine dal Dockerfile
docker images	Mostra le immagini disponibili

docker run -it nome_immagine 

bash	Avvia un container interattivo

docker ps	Mostra i container in esecuzione

docker exec -it nome_container bash	Entra in un container già attivo

docker stop nome_container	Ferma un container

docker rm nome_container	Elimina un container

docker rmi nome_immagine	Elimina un’immagine



# comandi accesso

da home/studenti01/isaaclab 
python3 docker/container.py start ros2

python3 docker/container.py enter ros2

./isaaclab.sh -s

ctrl+d per uscire dal container

python3 docker/container.py stop ros2



da visual studio ctrl+shift+p > add_host > nome del server > metti password "studenti01"