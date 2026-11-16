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
AWS Budgets och e-postlarm behöver kontrolleras och dokumenteras.
