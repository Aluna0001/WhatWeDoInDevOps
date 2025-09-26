# Git Hooks og Linting

## Git Hooks

**GitHub hooks** (eller mere præcist **Git hooks**) er scripts der automatisk køres på bestemte tidspunkter i din Git workflow. De fungerer som "event listeners" for Git operationer.

### Hvad er Git hooks?

Git hooks er executable scripts der triggers når specifikke Git events sker, såsom:
* Før du committer (pre-commit)
* Efter du committer (post-commit)
* Før du pusher (pre-push)
* Når du modtager en push (post-receive)

### Hvor findes de?

```
.git/hooks/
```

I denne mappe finder du eksempel-filer som:
* `pre-commit.sample`
* `pre-push.sample`
* `post-merge.sample`

### Praktisk eksempel med linting:

Du kan sætte en **pre-commit hook** op til at køre `npx standard` automatisk:

Dette vil:
1. Køre standard linting før hver commit
2. Stoppe committet hvis der er linting errors
3. Tvinge dig til at fixe koden først

### GitHub vs Git hooks:

* **Git hooks** = lokale scripts på din maskine
* **GitHub hooks/webhooks** = server-side events når du pusher til GitHub

### Hvorfor bruge dem?

* Automatisk code quality checks
* Prevent "broken" commits
* Køre tests automatisk
* Formatere kode konsistent i teams

## Linting Tools

### Hadolint

**"hadolint"** - Docker linter

Når vi starter med at arbejde med Docker kan vi bruge hadolint til vores Docker compose.

### Linting Philosophy

* **Man kan linte på alt**
* **Gå mere op i Linter**
* **Du må gerne fejle. Fejl. Og så skal Linteren fange det**
* **Vi forsøger at undgå teknisk gæld**

## Automation

### Cron Jobs

* **Cron / Cron job / Crontab** - planlagte tasks i Unix/Linux systemer
* Automatisering af gentagne opgaver
* Kan bruges til at køre linting checks, backups, monitoring osv.