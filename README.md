# fabric-git-poc

Testrepository voor Git-integratie en CI/CD met Microsoft Fabric en Power BI.

## Branchstrategie

```
feature/<omschrijving>  ──PR──▶  dev  ──PR──▶  main
        │                          │               │
  (eigen workspace)          WS_Git_Dev     GitHub Actions
                          (Git-koppeling)        │
                                          ┌──────┴──────┐
                                     WS_Git_Test    WS_Git_Prod
                                     (automatisch)  (na goedkeuring)
```

| Branch | Doel | Gekoppeld aan |
|---|---|---|
| `feature/*` | Grotere wijzigingen apart ontwikkelen | Eigen feature-workspace (tijdelijk) |
| `dev` | Dagelijks werk | `WS_Git_Dev` via Fabric Git-integratie |
| `main` | Goedgekeurde versie | Deploy naar `WS_Git_Test` en `WS_Git_Prod` via GitHub Actions |

## Werkwijze

1. Werk in `WS_Git_Dev` of lokaal op de branch `dev`.
2. Grotere wijziging? Maak een branch `feature/...` en een pull request naar `dev`.
3. Klaar voor Test? Maak een pull request van `dev` naar `main`.
4. Na de merge deployt GitHub Actions automatisch naar Test, en na goedkeuring naar Prod.

## Afspraken

### Naamgeving van items
Elk item krijgt een voorvoegsel. De itemnaam wordt ook de mapnaam in de repo.

| Voorvoegsel | Type |
|---|---|
| `SM_` | Semantic model |
| `RPT_` | Rapport |
| `NB_` | Notebook |
| `LH_` | Lakehouse |

### Branches
`feature/korte-omschrijving`, bijvoorbeeld `feature/omzet-ytd`.

### Commitberichten
Soort plus korte omschrijving:

- `feat:` iets nieuws, bijvoorbeeld `feat: measure Omzet YTD`
- `fix:` een correctie, bijvoorbeeld `fix: format Totale omzet`
- `docs:` documentatie, bijvoorbeeld `docs: README bijgewerkt`
- `chore:` onderhoud of configuratie, bijvoorbeeld `chore: parameter.yml bijgewerkt`

### Werken met Tabular Editor
Wijzig een model in een aan Git gekoppelde workspace nooit rechtstreeks via het XMLA-endpoint. Werk via de repo.
