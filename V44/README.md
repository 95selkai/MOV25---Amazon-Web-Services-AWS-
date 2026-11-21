Vecka 44 – AWS Nätverk och säkerhet
Del 2 – VPC och nätverk
Jag har skapat en VPC i AWS med namnet novatrix-vpc i regionen Stockholm (eu-north-1).

Jag har konfigurerat:

Publikt subnät: novatrix-public
Privata subnät: novatrix-private-a och novatrix-private-b
Route tables för nätverkstrafiken
Internet Gateway för internetanslutning
Del 3 – Säkerhet
Jag har arbetat med Security Groups och Network ACLs för att skydda nätverket.

Security Group novatrix-web-sg har konfigurerats med regler för HTTP (port 80), HTTPS (port 443) och begränsad SSH-åtkomst (port 22).

Jag har även skapat en Network ACL med namnet novatrix-web-nacl.

Del 4 – Webbserver
Jag har skapat en EC2-instans med namnet novatrix-web i det publika subnätet.

På servern har jag installerat och startat Nginx.

Webbservern har testats och visar sidan:

Välkommen till Novatrix! Min första webbserver på AWS EC2.

De privata subnäten är förberedda för framtida resurser, exempelvis en databas.

Del 5 – Verifiering och dokumentation
Jag har kontrollerat att Nginx är aktiv och att webbservern går att öppna via HTTP.

Jag har dokumenterat nätverksmiljön med skärmbilder från AWS.

Ytterligare verifiering av NACL-regler och blockerad trafik behöver dokumenteras för att bekräfta säkerhetskraven.

Defense in depth
Jag har arbetat med flera säkerhetsnivåer i AWS, bland annat Security Groups och Network ACLs, för att begränsa åtkomsten till nätverket.
