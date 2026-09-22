**Namn** Jan Haddad
**Datum** 15-09 2026
**Kurs** Introduktion till yrkesrollen och grunderna i IT-infrastruktur



## Git - Versionshantering och skapa Projektmapp

För att verionshantera mitt arbete använde jag Git bash och Github.


cd ~\dokuments          "för att navigera till dokuments mappen"
mkdir Systementor-Labb  "för att skapa mappen som heter Systementor-Labb"
cd Systementor-Labb     "för att navigera till mappen systementor-Labb"
pwd                     "för att kontrollera att jag är i rätt map (/c/Users/janha/documents/systementor-labb)"  

### initiera Git repository samt skapa dokumentationsfilen

git init                 "För att göra den aktuella mappen till ett git repository"
git branch -M main       "för att döpa den nuvarande branhen till main"

touch Labbdokumentation.md "här skapade vi en markdown fil som heter Labbdokumentation för att kunna dokumetnera senare i uppgiften med hjälp av Visual Studio Code"

git status                    "Som visade att labbdokumentet är ospårade av git "

git add Labbdokumentation.md  ""

### Commits

git commit -m "grundstruktur" 

git log --oneline  "för att kontrollera commit historiken som visade resultat (5368645 (HEAD -> main) grundstruktur)"


### Github

Jag skapade en repositroy på Github för att kunna lagra projektet externt.

git remote add origin https://github.com/Jan0321/Uppgift_Labbmilj-Git-CLI-och-AI.git "för att koppla mitt lokala git repository till github"

git remote -v        "för att kontrollera att koppligen var ok"

git push -u orgin main  "då skickade jag mitt lokala main branch till github"

git status              "då visade det att koppligen lyckades och är synkroiserat med repositoryt på github(On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
)"

git log --oneline   "5368645 (HEAD -> main) grundstruktur"
















## Introdution
I denna uppgift bygger jag en virtuell labbmilijö i VirtualBox med Linux och Windows 11. Jag ska konfigurera ett gemensamt närverk, arbeta med kommandon och behörigheter samt dokumentera resultat.




Jag använder Virtualbox och har installerat två virtuella maskiner:

- Windows 11
- Linux Server


