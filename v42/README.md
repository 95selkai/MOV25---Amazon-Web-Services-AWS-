AWS – Vecka 42 – Novatrix
Namn: Selma Kaidi
Kurs: Amazon Web Services (AWS)
Projekt: Novatrix-Web

Jag har skapat en EC2-instans i AWS med Amazon Linux 2023. Instansen heter Novatrix-Web och är placerad i regionen Europe (Stockholm).

Jag valde en instanstyp med hänsyn till kostnaden.

2. Installera en webbserver
Jag anslöt till min EC2-instans via EC2 Instance Connect och installerade webbservern Nginx.

Jag använde följande kommandon:

sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
Jag kontrollerade att Nginx fungerade.

3. Driftsätta en webbsida
Jag skapade en enkel HTML-webbsida för Novatrix.

Webbsidan innehåller rubriken “Välkommen till Novatrix!” och texten “Min första webbserver på AWS EC2.”

Webbsidan är tillgänglig via instansens publika IP-adress:

http://16.171.10.3

4. Verifiering
Jag öppnade webbsidan i webbläsaren och kontrollerade att den fungerade.

Jag har tagit skärmbilder som visar webbservern och den publicerade webbsidan.

5. Dokumentation
Jag har skapat ett publikt GitHub-repository och dokumenterar arbetet i mappen v42.

Dokumentationen innehåller beskrivningar av installationen, konfigurationen och verifieringen.

6. Kostnadskontroll
Jag ska kontrollera att en månadsbudget med e-postlarm är konfigurerad i AWS Budgets och lägga till en skärmbild som bevis.
