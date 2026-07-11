# Verhaltenskodex für Mitwirkende

Willkommen bei **Cersia**! Cersia ist die persönliche Kaufakte für Schweizer Konsumentinnen und Konsumenten und befindet sich aktuell in der Pilotphase. Das Projekt umfasst mehrere Repositories in der Organisation `Cersia-ch` (z. B. `docs`, `.github`, weitere produktspezifische Repos) sowie privat verwaltete Template- und Infrastruktur-Repos unter `HeiligerG`.

Wenn du einen Beitrag leisten möchtest – sei es durch Dokumentation, Übersetzungen, Händlerdaten, Tests, Bug-Reports oder Code – bitten wir dich, die folgenden Regeln und Abläufe zu beachten. Sie sorgen dafür, dass das Projekt übersichtlich, nachvollziehbar und für alle Beteiligten sicher bleibt.

---

## 1. Respektvoller Umgang

- **Sei freundlich und geduldig.** Viele Mitwirkende arbeiten sich zum ersten Mal in ein Schweizer Consumer-Produkt mit Fokus auf Datenschutz ein. Konstruktives Feedback ist willkommen, herablassende Kommentare sind es nicht.
- **Hilf anderen.** Wenn du eine Frage beantworten oder ein Problem erklären kannst, tu es gerne.
- **Akzeptiere unterschiedliche Erfahrungsstufen.** Es gibt keine „dummen" Fragen oder Beiträge.
- **Respektiere den Datenschutz.** Cersia verarbeitet sensible Konsumdaten (Belege, Finanzen, ggf. ableitbare Gesundheits- oder Wohninformationen). Diskutiere niemals reale personenbezogene Daten aus Produktion, Tests oder Interviews öffentlich. Verwende für Beispiele ausschliesslich anonymisierte oder fiktive Daten.

---

## 2. Git-Workflow (verpflichtend)

Unser Projekt lebt von einem **sauberen, nachvollziehbaren Git-Verlauf** über mehrere Repositories hinweg. Jede Änderung muss diesem Workflow folgen:

### 2.1 Nie direkt auf `main` oder `master` committen

Der Branch `main` (bzw. `master` in historisch gewachsenen Repos) ist unser produktionsreifer Hauptbranch. **Es ist strikt verboten**, direkt darauf zu committen oder zu pushen. Auch Dokumentations- oder Konfigurationsänderungen benötigen einen Feature-Branch.

### 2.2 Feature-Branches verwenden

Für jede Änderung – egal ob Bugfix, neues Feature, Doku-Anpassung oder Konfig-Update – erstellst du einen eigenen Branch.

```bash
# Naming-Konventionen
feat/kurze-beschreibung          # Neue Features
fix/kurze-beschreibung           # Bugfixes
docs/kurze-beschreibung          # Dokumentation
refactor/kurze-beschreibung      # Code- oder Doku-Refactoring
chore/kurze-beschreibung         # Wartung, Tooling, Dependencies
data/kurze-beschreibung          # Händlerdatenbank, Inhalte, Übersetzungen
```

**Beispiele:**

```bash
git checkout -b docs/adapt-code-of-conduct-for-cersia
git checkout -b feat/onboarding-checklist
git checkout -b data/haendler-digitec-galaxus-update
```

### 2.3 Commits sinnvoll gestalten

- Schreibe aussagekräftige Commit-Nachrichten auf **Deutsch** (Englisch nur, wenn der betroffene Issue/PR englischsprachig ist).
- Ein Commit sollte eine in sich geschlossene Einheit sein.
- Vermeide riesige Commits, die mehrere unterschiedliche Themen mischen.

**Gutes Beispiel:**

```
docs(coc): adapt code of conduct from webtasks to cersia
```

### 2.4 Merge mit `--no-ff`

Wenn dein Feature-Branch fertig ist und reviewed wurde, wird er über einen **non-fast-forward Merge** integriert:

```bash
git checkout main
git merge --no-ff docs/adapt-code-of-conduct-for-cersia \
  -m "Merge branch 'docs/adapt-code-of-conduct-for-cersia' into main"
```

Dadurch bleibt der Verlauf des Branches im Git-Graph sichtbar, was die Nachvollziehbarkeit erheblich verbessert.

### 2.5 Branch nach dem Merge löschen

Sobald ein Branch erfolgreich gemerged wurde, wird er lokal und remote gelöscht:

```bash
git branch -d docs/adapt-code-of-conduct-for-cersia
git push origin --delete docs/adapt-code-of-conduct-for-cersia
```

### 2.6 Kurz zusammengefasst

1. `git checkout -b <branch-name>`
2. Änderungen vornehmen und **repo-spezifisch** validieren (siehe Abschnitt 3)
3. `git add <dateien>`
4. `git commit -m "aussagekräftige nachricht"`
5. PR öffnen → Review → Approval
6. `git checkout main`
7. `git merge --no-ff <branch-name>`
8. `git branch -d <branch-name>`
9. `git push origin --delete <branch-name>`

---

## 3. Qualitätsanspruch

### 3.1 Vor dem Commit validieren

Validiere **repo-spezifisch**, nicht pauschal:

| Repo-Typ | Validierung |
|----------|-------------|
| `Cersia-ch/docs` (Markdown) | Markdown-Lint, interne Links prüfen, Rechtschreibung (DE/CH) |
| `Cersia-ch/.github` (Org-Profile, Templates) | YAML/JSON-Lint, Vorschau der GitHub-UI |
| Anwendungs-Repos (z. B. `app`, `api`) | `npm run build`, `npm test`, Lint, Type-Check |
| Händlerdaten-Repos | Schema-Validierung gegen `haendler.schema.json` |

**Lieber eine kleine, saubere Änderung als ein grosser, halbfertiger Patch.**

### 3.2 Patterns beibehalten

- Halte dich an bestehende Strukturen (z. B. Hermes-Phasen-Templates in `docs/`).
- Verwende etablierte Bibliotheken und Konventionen des jeweiligen Repos.
- Keine ungefragten Framework-Wechsel oder Massen-Refactorings in einem PR.

---

## 4. Reagieren auf Änderungswünsche

- Wenn ein Maintainer Feedback oder Änderungswünsche äussert, nimm es konstruktiv auf.
- Pushe Korrekturen auf denselben Branch (sofern noch nicht gemerged) oder erstelle bei grösseren Änderungen einen neuen, sauberen Branch.
- Frage nach, wenn etwas unklar ist – lieber einmal mehr fragen als eine Annahme treffen, die gegen Datenschutz oder Schweizer Recht verstösst.

---

## 5. Inhaltliche Beiträge

Cersia lebt von vielfältigen Beiträgen. Neue Inhalte benötigen eine klare Struktur:

### 5.1 Dokumentation (Hermes-Phasen)

- Neue Doku-Dateien folgen der Struktur der Hermes-Project-Templates (`phase-0-initiation`, `phase-1-analyse`, …).
- Jede Datei enthält: Zweck, Verantwortlichkeiten, Akzeptanzkriterien und Reviewer.
- Halte dich an bestehende Gliederungspunkte, statt eigene Unterstrukturen einzuführen.

### 5.2 Händlerdatenbank

- Neue Händler werden über `data/<haendler-name>-update`-Branches eingereicht.
- Pflichtfelder: Rückgabelink, Kundendienstlink, übliche Rückgabefrist, Rückgabeadresse, erforderliche Schritte, bekannte Einschränkungen, Datum der letzten Überprüfung.
- Keine Annahmen über gesetzliche Ansprüche – nur dokumentierte Händlerangaben.

### 5.3 Übersetzungen (DE / FR / IT / EN)

- Übersetzungen sind **keine 1:1-Übertragungen**, sondern sprachlich und kulturell angepasst.
- Händlerbegriffe, Rechtsinformationen und Kommunikationsvorlagen müssen lokalisiert werden.
- Änderungen an einer Sprache lösen einen Hinweis an die anderen Sprachen aus (Folge-PRs).

### 5.4 Tests & Bug-Reports

- Reproduzierbare Steps sind Pflicht (Umgebung, Browser, Konto, Händler).
- Sicherheitslücken bitte **nicht** öffentlich melden, sondern direkt an `security@cersia.ch`.

---

## 6. Lizenz

Durch deinen Beitrag stimmst du zu, dass er unter der Lizenz des jeweiligen Repos veröffentlicht wird. Repo-spezifische Lizenzdetails siehe `LICENSE` im entsprechenden Repository.

---

Vielen Dank, dass du Cersia besser machst!