# Regional RAG Pilot

Pilotprojekt for systemadministratorer på billeddiagnostiske afdelinger i Region Hovedstaden.

## Formål

Formålet er at bygge en Retrieval-Augmented Generation (RAG) løsning i Databricks, der gør det muligt for systemadministratorer hurtigt at finde svar i Quick Guides, SOP'er og teknisk dokumentation.

Piloten fokuserer på at evaluere, om AI-assisteret videnssøgning kan reducere tidsforbruget ved fejlfinding og support.

---

# Pilot Scope

Første pilot omfatter:

- 8 Quick Guides
- Golden Set til evaluering
- Databricks AI Search
- Genie Agent
- Dokumentbaseret søgning

Piloten indeholder ikke:

- Patientdata
- Kliniske journaldata
- CPR-numre
- Passwords eller hemmeligheder

---

# GitHub Struktur

```text
regional-rag-pilot/

├── README.md
│
├── docs/
│   ├── notes.md
│   └── databricks-notes.md
│
├── golden_set/
│   ├── README.md
│   └── Golden_Set.xlsx
│
└── prompts/
    └── system_prompt.txt
```

---

# Databricks Struktur

```text
Catalog
└── dap_project_rag938_upload
    └── Volumes
        └── dap_project_rag938_upload
            └── pilot
                ├── quick_guides
                │   ├── QuickGuide_01.pdf
                │   ├── QuickGuide_02.pdf
                │   ├── QuickGuide_03.pdf
                │   ├── QuickGuide_04.pdf
                │   ├── QuickGuide_05.pdf
                │   ├── QuickGuide_06.pdf
                │   ├── QuickGuide_07.pdf
                │   └── QuickGuide_08.pdf
                │
                ├── outputs
                │
                └── evaluation
```

---

# Sikkerhed og Governance

## Dataklassifikation

Tilladt:

- Quick Guides
- SOP'er
- Teknisk dokumentation
- Driftsvejledninger

Ikke tilladt:

- Patientdata
- CPR-numre
- Følsomme personoplysninger
- Passwords
- API-nøgler
- Certifikater

## Adgangsstyring

Der anvendes princippet:

- Least Privilege
- Need To Know
- Rollebaseret adgang

Brugere må kun se dokumenter, som de er autoriseret til at tilgå.

## Kildehenvisninger

Alle svar skal indeholde referencer til de dokumenter, som svaret er baseret på.

Eksempel:

```text
Kilde:
QuickGuide_03.pdf
Afsnit 4.2
```

## Hallucinationskontrol

Hvis dokumentationen ikke indeholder svaret, skal agenten svare:

```text
Jeg kan ikke finde svaret i den tilgængelige dokumentation.
```

---

# Succeskriterier

Piloten vurderes på:

- Retrieval Accuracy
- Correctness
- Groundedness
- Brugerfeedback

Målsætninger:

- 90 % korrekt dokumentgenfinding
- Kildereferencer i alle svar
- Positiv feedback fra pilotbrugere

---

# Næste Skridt

- [ ] Upload 8 Quick Guides til Databricks Volume
- [ ] Opret AI Search indeks
- [ ] Opret Genie Agent
- [ ] Tilknyt dokumenter
- [ ] Test Golden Set
- [ ] Evaluer resultater
