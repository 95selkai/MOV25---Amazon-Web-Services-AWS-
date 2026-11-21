AWS – Vecka 43: IAM, EC2 och S3

## Syfte
I denna uppgift har jag arbetat med identiteter, grupper, behörigheter och roller i AWS. Målet är att förstå hur IAM används för att styra åtkomst enligt principen om minsta möjliga behörighet (least privilege), och hur en EC2-instans kan få åtkomst till S3 genom en IAM-roll.

## Resurser som skapats eller kontrollerats
- S3-bucket: `novatrix-s3-demo-bucket`.
- IAM-användare: `demo-erik`.
- IAM-grupp: `utveckling`, med användaren `demo-erik` som medlem.
- Gruppolicy: `AmazonS3ReadOnlyAccess`.
- Direkt policy för användaren: `IAMUserChangePassword` (synlig i IAM-konsolen).
- IAM-roll: `novatrix-ec2-read`, med `AmazonS3ReadOnlyAccess`.
- EC2-instans: `Novatrix-Web`.

## 1. IAM-användare och grupp
Jag skapade IAM-användaren `demo-erik` och gruppen `utveckling`. Användaren lades till i gruppen. I IAM-konsolen kontrollerade jag att gruppen hade policyn `AmazonS3ReadOnlyAccess`, som ger läsbehörigheter till S3. Jag kontrollerade också användarens tilldelade policies.

Exempel på AWS CLI-kommandon för att återskapa och kontrollera upplägget (skapa inte dubbletter om resurserna redan finns):

```bash
aws iam get-user --user-name demo-erik
aws iam get-group --group-name utveckling
aws iam list-attached-group-policies --group-name utveckling
aws iam list-attached-user-policies --user-name demo-erik
```

## 2. IAM-roll för EC2
Jag skapade/kontrollerade rollen `novatrix-ec2-read`. Den har policyn `AmazonS3ReadOnlyAccess`. I fliken Trust relationships verifierade jag att tjänsten `ec2.amazonaws.com` får anta rollen med åtgärden `sts:AssumeRole`. Detta gör att EC2 kan använda tillfälliga rolluppgifter i stället för att lagra permanenta åtkomstnycklar på servern.

## 3. Koppla rollen till EC2
Jag öppnade EC2 > Instances, markerade `Novatrix-Web` och valde Actions > Security > Modify IAM role. Jag valde `novatrix-ec2-read` och sparade. AWS visade ett grönt meddelande om att IAM-rollen hade ersatts/kopplats. Instansen var Running och hade 3/3 godkända statuskontroller.

## 4. Verifiering via EC2-terminal
I terminalen på EC2 körde jag:

```bash
aws sts get-caller-identity
```

Resultatet innehöll en ARN i formatet `arn:aws:sts::...:assumed-role/novatrix-ec2-read/i-...`. Det visar att terminalen använde den avsedda EC2-rollen.

Jag körde också:

```bash
aws s3 ls
```

Kommandot listade `novatrix-s3-demo-bucket` utan fel. Detta visar att den aktuella identiteten kunde lista bucketnamn. Ett separat test av att lista objekt i just bucketen har inte visats som slutfört:

```bash
aws s3 ls s3://novatrix-s3-demo-bucket/
```

## 5. Least privilege – varför dessa behörigheter?
`AmazonS3ReadOnlyAccess` ger läsbehörigheter till S3 men inte skrivbehörighet. Det är mer begränsat än administratörsåtkomst, men policyn gäller S3-resurser brett och är därför inte strikt begränsad till en enda bucket. I en produktionsmiljö skulle jag skapa en anpassad IAM-policy som enbart ger nödvändiga läsrättigheter till den aktuella bucketen. Användaren får sina S3-behörigheter genom gruppen och EC2 får dem genom rollen.

## 6. Resultat och återstående kontroll
Genomfört och dokumenterat: S3-bucket, IAM-användare, gruppmedlemskap, policies, EC2-roll, trust relationship, rollkoppling till EC2, STS-identitet och lyckad bucketlistning. Återstår att dokumentera: test av objektlistning i bucketen samt eventuellt ett negativt skrivtest, om det krävs av läraren. Spara relevanta skärmbilder i GitHub-repot utan att visa lösenord eller access keys.
