# AWS – Vecka 44 | Novatrix

**Nätverksarkitektur och säkerhet i Amazon Web Services (AWS)**
Utbildning: Moln- och virtualiseringsspecialist

## Projektbeskrivning

Under vecka 44 har jag byggt och dokumenterat en nätverksmiljö i AWS. Arbetet omfattar VPC, publika och privata subnät, routing, Security Groups, Network ACL och en EC2-webbserver med Nginx.

## 1. Översikt

| Resurs | Konfiguration |
|---|---|
| Region | `eu-north-1` (Stockholm) |
| VPC | `novatrix-vpc` |
| VPC CIDR | `10.0.0.0/16` |
| Publikt subnät | `novatrix-public` (`10.0.1.0/24`) |
| Privata subnät | `novatrix-private-a`, `novatrix-private-b` |
| Publik route table | `novatrix-rt` |
| EC2 | `novatrix-web` |
| Operativsystem | Amazon Linux 2023 |
| Webbserver | Nginx |
| Security Group | `novatrix-web-sg` |
| Network ACL | `novatrix-web-nacl` |

## 2. VPC och nätverksdesign

Jag skapade `novatrix-vpc` och separerade nätverket i ett publikt subnät för webbservern och två privata subnät för framtida interna tjänster.

```text
Internet
|
Internet Gateway
|
novatrix-vpc
10.0.0.0/16
|
+------------+------------+
| |
novatrix-public Privata subnät
10.0.1.0/24 novatrix-private-a
| novatrix-private-b
novatrix-web (framtida DB)
EC2 + Nginx
```

Den publika routetabellen har bland annat följande routes:

```text
10.0.0.0/16 -> local
0.0.0.0/0 -> Internet Gateway
```

## 3. Säkerhet – Security Groups och Network ACL

Jag har arbetat med flera säkerhetslager (*defense in depth*).

### Security Group

För `novatrix-web-sg` har jag tidigare kontrollerat dessa inkommande regler:

| Typ | Port | Källa |
|---|---:|---|
| HTTP | 80 | `0.0.0.0/0` |
| HTTPS | 443 | `0.0.0.0/0` |
| SSH | 22 | `188.150.43.119/32` (IP vid konfigurationstillfället) |

> **Obs:** En öppen HTTPS-port betyder inte automatiskt att TLS-certifikat och HTTPS är konfigurerade i Nginx.

### Network ACL

Jag har skapat en NACL med namnet `novatrix-web-nacl`. Den fungerar som ett ytterligare skydd på subnätsnivå. De exakta in- och utgående reglerna samt subnätskopplingen behöver dokumenteras separat för att säkerhetskonfigurationen ska vara fullständigt verifierad.

## 4. EC2 och webbserver

Jag skapade EC2-instansen `novatrix-web` i det publika subnätet och installerade Nginx på Amazon Linux 2023.

För att kontrollera tjänsten använde jag:

```bash
sudo systemctl status nginx
```

Resultatet visade:

```text
Active: active (running)
```

Jag öppnade webbserverns publika IP-adress i webbläsaren och såg texten:

> Välkommen till Novatrix! Min första webbserver på AWS EC2.

Det verifierar att webbservern kunde nås via **HTTP** vid testtillfället.

## 5. Tester och verifiering

| Kontroll | Resultat |
|---|---|
| VPC skapad i Stockholm-regionen | Kontrollerat |
| Publikt och privata subnät | Kontrollerat |
| Route till Internet Gateway | Kontrollerat |
| EC2 och Nginx | Kontrollerat |
| Webbplats tillgänglig via HTTP | Kontrollerat |
| HTTPS med TLS-certifikat | Inte verifierat |
| Blockerad trafik och NACL-regler | Behöver dokumenteras |

## 6. Dokumentation och skärmbilder

Skärmbilder från AWS används som underlag för VPC, subnät, routing, Security Groups, NACL, EC2 och webbservern. Lägg dem i mappen `bilder/` och länka till dem här när de är uppladdade.

## Slutsats

Arbetet gav mig praktisk erfarenhet av nätverkssegmentering, routing, EC2 och flera säkerhetslager i AWS. Jag har även installerat och testat en fungerande Nginx-webbserver.

