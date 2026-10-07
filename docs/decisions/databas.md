# Beslutsdokument: databasval

*Ett av teamets sex beslutsdokument. Skrivs i M3, hålls levande. Samma mall som `docs/testing.md`. Fyll i varje rubrik – en sida räcker, men varje påstående ska gå att försvara muntligt på onsdag.*

**Datum:** 2026-10-
**Beslut:** *(en eller två meningar: vad ligger i Postgres, vad ligger i MongoDB, och varför just den gränsen)*

## Bakgrund
*(Vad ärvde ni? Vilken skuld betalar det här av? Vad kostar `/api/tours` i dag – mät: storlek på svaret, antal databasfrågor, antal rader i `tour_logs`.)*

## Dokumentmodellen för turer
*(Skissa dokumentet som JSON med de fält ni bestämt. Inbäddat eller refererat – och varför? Hur många mätpunkter är en tur i dag, hur stort blir ett dokument, och var går gränsen (16 MB per dokument) för er? Vilka index behövs för de frågor klienten ställer?)*

```json
{
}
```

## Vad som stannar i Postgres
*(Guider, användare, foton? Motivera per tabell: relationer, transaktioner, sökning.)*

## Så här ska migreringen gå till (genomförs i M5)
*(Steg för steg: skript som läser ur Postgres och skriver till Mongo · hur `/api/tours` byter källa · hur ni verifierar att inget tappats (antal turer, antal punkter, stickprov) · vad som händer med `tour_logs`-tabellen efteråt.)*

## Alternativ vi jämförde
*(Minst två: t.ex. behålla allt i Postgres men med `jsonb`-kolumn för loggarna · allt till MongoDB · MongoDB för loggarna, Postgres för resten. För varje: vad talar för, vad talar emot.)*

## Konsekvenser
*(Två databaser att drifta och backa upp. Två anslutningssträngar i miljön. Vad kräver det av compose, av pipelinen, av molnet i M6?)*

**Skrivet av:** *(namn – den som signerar ska kunna försvara det)*
