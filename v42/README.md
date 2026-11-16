# AWS – Vecka 42 | Novatrix-Web

**Namn:** Selma Kaidi
**Kurs:** Amazon Web Services (AWS)
**Projekt:** Novatrix-Web

## 1. EC2-instans
Jag skapade en EC2-instans med Amazon Linux 2023 i regionen Europe (Stockholm).

**Instansnamn:** Novatrix-Web

## 2. Installation av Nginx
Jag anslöt via EC2 Instance Connect och installerade Nginx.

```bash
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

## 3. Webbsida
Jag skapade en enkel HTML-webbsida med rubriken Välkommen till Novatrix!

**Publik IP vid test:** http://16.171.10.3

## 4. Verifiering
Jag öppnade webbsidan i webbläsaren och kontrollerade att den fungerade.

## 5. Dokumentation
Skärmbilder och ytterligare dokumentation läggs till i denna mapp.

## 6. Kostnadskontroll
6. Kostnadskontroll – AWS Budgets
Jag har skapat en månadsbudget på 5 USD i AWS Budgets för att övervaka kostnaderna för mitt Novatrix-projekt.

Jag har konfigurerat tre kostnadslarm:

Actual cost > 85 %
Actual cost > 100 %
Forecasted cost > 100 %
Min e-postadress är verifierad för att kunna ta emot budgetlarm.

Jag har kontrollerat att budgeten är aktiv och har status Healthy.

Resultat: Kostnadskontrollen är konfigurerad och verifierad.


