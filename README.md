# 🏥 Regional RAG Pilot

### AI-baseret vidensassistent for billeddiagnostisk IT i Region Hovedstaden

---

## Formål

Regional RAG Pilot har til formål at etablere en fælles AI-baseret vidensassistent for systemadministratorer på de billeddiagnostiske afdelinger i Region Hovedstaden.

Løsningen skal gøre det nemmere at finde, forstå og genanvende teknisk viden på tværs af hospitaler, teams og systemer. Ved hjælp af Retrieval-Augmented Generation (RAG) kombineres regionale dokumenter, driftsprocedurer, leverandørmanualer og historiske hændelser i én samlet og styret vidensplatform.

### Mål

- Reducere tiden brugt på fejlsøgning
- Mindske afhængigheden af nøglepersoner
- Forbedre vidensdeling mellem hospitaler
- Understøtte onboarding af nye medarbejdere
- Sikre sporbare og dokumenterede AI-svar
- Etablere et fælles regionalt vidensgrundlag

---

# Baggrund

Teknisk viden er i dag spredt på tværs af mange forskellige systemer og lagringssteder.

## Typiske kilder

- SharePoint
- Microsoft Teams
- ServiceNow
- Leverandørportaler
- SOP'er
- Driftsvejledninger
- Netværksdokumentation
- Incidenthistorik
- Change Records
- Lokale wikier

Konsekvensen er, at systemadministratorer ofte bruger betydelig tid på at finde relevant information, og at værdifuld viden risikerer at forsvinde, når nøglepersoner skifter rolle eller arbejdsplads.

---

# Vision

At skabe en regional AI-assistent, som kan besvare spørgsmål som:

> Hvorfor afviser Sectra PACS undersøgelser fra Siemens CT?

> Hvordan er DICOM-routing konfigureret mellem RIS og PACS?

> Hvilken SOP beskriver failover-proceduren for PACS?

> Har vi tidligere oplevet lignende incidents?

> Hvilke ændringer blev gennemført ved den seneste opgradering?

## Krav til alle svar

- Kildebaserede
- Sporbare
- Dokumenterede
- Reproducerbare
- Underlagt governance

Assistenten skal fungere som en erfaren kollega, ikke som en generisk chatbot.

---

# Målgruppe

## Primære brugere

- PACS-administratorer
- RIS-administratorer
- Infrastrukturadministratorer
- Integrationsspecialister
- Driftsteams
- Applikationsspecialister

## Sekundære brugere

- Teamledere
- Serviceejere
- IT-arkitekter
- Projektledere
- Leverandøransvarlige

---

# Scope

## Inkluderet i pilotprojektet

### Dokumentation

- PACS-dokumentation
- RIS-dokumentation
- SOP'er
- Runbooks
- Leverandørmanualer
- Driftsprocedurer
- Fejlfindingsvejledninger

### Datakilder

- SharePoint Online
- Microsoft Teams
- ServiceNow
- PDF-dokumenter
- Word-dokumenter
- Excel-dokumentation

### Domæner

- Radiologi
- Nuklearmedicin
- Billeddiagnostisk IT
- Understøttende infrastruktur

## Uden for scope

- Patientdata
- EPJ-data
- DICOM-billedindhold
- Kliniske beslutningssystemer
- Automatiske ændringer i produktionsmiljøer

---

# Succeskriterier

## Drift

- Reduceret MTTR (Mean Time To Resolution)
- Hurtigere fejlsøgning
- Genbrug af tidligere løsninger

## Brugere

- Kortere søgetid
- Høj brugeradoption
- Hurtigere onboarding

## Governance

- Fuld sporbarhed
- Adgangsstyring via eksisterende rettigheder
- Auditérbare svar og opslag

## Kvalitet

- Høj relevans i søgeresultater
- Kildehenvisning i alle svar
- Lav hallucinationsrate

---

# Løsningsarkitektur

```text
                +----------------------+
                | SharePoint           |
                +----------+-----------+
                           |
                +----------v-----------+
                | ServiceNow           |
                +----------+-----------+
                           |
                +----------v-----------+
                | SOP'er & Runbooks    |
                +----------+-----------+
                           |
                +----------v-----------+
                | Leverandørmanualer   |
                +----------+-----------+
                           |
                           v

        +---------------------------------------+
        | Dokumentindlæsning                    |
        +---------------------------------------+
                           |
                           v

        +---------------------------------------+
        | Parsing & Normalisering               |
        +---------------------------------------+
                           |
                           v

        +---------------------------------------+
        | Chunking & Metadata                   |
        +---------------------------------------+
                           |
                           v

        +---------------------------------------+
        | Embeddings                            |
        +---------------------------------------+
                           |
                           v

        +---------------------------------------+
        | Databricks AI Search                  |
        +---------------------------------------+
                           |
                           v

        +---------------------------------------+
        | Mosaic AI Agent                       |
        +---------------------------------------+
                           |
                           v

        +---------------------------------------+
        | Systemadministrator                   |
        +---------------------------------------+
```

---

# Teknologistak

## Platform

- Databricks Lakehouse
- Unity Catalog
- Databricks AI Search
- Mosaic AI Agent Framework

## Datakilder

- SharePoint Online
- Microsoft Teams
- ServiceNow
- PDF-filer
- Office-dokumenter
- Leverandørdokumentation

## AI-komponenter

- Embedding-modeller
- Retrieval-Augmented Generation (RAG)
- Hybrid Search
- Semantic Search
- Reranking
- Kildehenvisninger

---

# Dataarkitektur

## Bronze

Rå data og originale dokumenter.

Eksempler:

- PDF-filer
- Word-dokumenter
- SharePoint-indhold
- ServiceNow-data

## Silver

Strukturerede og rensede data.

Eksempler:

- Ekstraheret tekst
- Metadata
- Dokumentversioner
- Kildereferencer

## Gold

AI-optimerede datasæt.

Eksempler:

- Chunks
- Embeddings
- Søgeindekser
- Retrieval-tabeller

---

# Metadata-strategi

Alle dokumenter beriges med metadata.

```json
{
  "hospital": "Herlev",
  "afdeling": "Radiologi",
  "system": "Sectra PACS",
  "leverandør": "Sectra",
  "dokumenttype": "SOP",
  "kritikalitet": "Høj",
  "senest_opdateret": "2026-10-01"
}
```

### Mulige metadatafelter

- Hospital
- Afdeling
- System
- Leverandør
- Dokumenttype
- Miljø
- Ansvarlig enhed
- Sikkerhedsniveau
- Version
- Sidst opdateret

---

# Governance

## Adgangsstyring

Brugere må kun kunne se information, som de allerede har adgang til gennem eksisterende rettighedsmodeller.

## Sporbarhed

Alle svar skal kunne spores tilbage til:

- Kildedokument
- Dokumentversion
- Brugerforespørgsel
- Tidspunkt

## Revision

Alle opslag og svar skal kunne logges og auditeres.

## Transparens

Systemet skal vise de kilder, som svaret bygger på.

---

# Eksempel på brugerrejse

### Spørgsmål

> Hvorfor modtager Sectra PACS ikke undersøgelser fra Siemens CT?

### Systemet udfører

1. Søgning i AI Search
2. Gennemgang af SOP'er
3. Analyse af tidligere incidents
4. Opslag i change-historik
5. Opslag i leverandørdokumentation
6. Generering af svar med kildehenvisninger

### Eksempel på svar

> Den mest sandsynlige årsag er en AET-konfigurationsfejl introduceret efter netværksændringen den 12. oktober 2026. Se SOP PACS-NET-014 samt incident INC45612.

---

# Roadmap

## Fase 1 - Fundament

- Arkitekturdesign
- Datakildeanalyse
- Governance-model
- Proof of Concept

## Fase 2 - Dokumentindlæsning

- SharePoint-integration
- SOP-indlæsning
- Leverandørdokumentation

## Fase 3 - RAG-platform

- Embeddings
- AI Search
- Vidensassistent

## Fase 4 - ITSM-integration

- ServiceNow Incidents
- ServiceNow Problems
- ServiceNow Changes

## Fase 5 - Regional skalering

- Flere hospitaler
- Flere tekniske domæner
- Operations-dashboard
- AI-assisteret drift

---

# Risici

## Datakvalitet

Forældet dokumentation giver forældede svar.

## Governance

Fejlkonfigurerede rettigheder kan eksponere følsom information.

## Adoption

Løsningen skaber først værdi, når den anvendes konsekvent.

## Tavs viden

Ikke-dokumenteret viden kan ikke genfindes af systemet.

---

# Forventede gevinster

- Hurtigere fejlsøgning
- Bedre vidensdeling
- Mindre personafhængighed
- Højere dokumentationskvalitet
- Kortere oplæringstid
- Regional genbrug af erfaringer
- Stærkere AI-governance

---

# Projektstatus

**Status:** Design og afklaring

### Nuværende fokus

- Datakilder
- Governance
- Databricks-arkitektur
- AI Search-strategi
- Pilotimplementering

---

# Bidragydere

**Region Hovedstaden**  
Center for IT og Medicoteknologi  
Billeddiagnostisk IT

---

# Licens

Internt pilotprojekt for Region Hovedstaden.

Fortroligt materiale til intern anvendelse.
``
