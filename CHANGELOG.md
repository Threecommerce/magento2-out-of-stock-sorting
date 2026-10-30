# Changelog

## [1.0.4] - 2026-10-28

### Fixed
- Con il motore di ricerca standard (OpenSearch/Elasticsearch/MySQL) l'ordinamento veniva comunque perso: il
  `SearchResultApplier` del core azzera l'`ORDER BY` e imposta `FIELD(id, ...)`. Nuovo plugin
  `SortAfterSearchApplierPlugin` che dopo l'applier riporta in testa l'ordinamento per stato stock (solo liste
  categoria). Verificato su Magento standard (demo Hyvä) e sul sito con applier personalizzato.
- La logica è in `Model\StockOrder` (idempotente: join una sola volta, ordinamento per stock sempre per primo).

## [1.0.3] - 2026-10-28

### Fixed
- Il modulo non produceva alcun effetto: `CollectionFilter::filter()` restituisce `void`, quindi `afterFilter`
  riceveva sempre `null` e usciva subito. Ora il plugin lavora sulla collection passata come argomento.
- Il ramo "senza MSI" faceva il join con `website_id = 1`, mentre `cataloginventory_stock_status` usa lo scope
  di default (`website_id = 0`): ora si usa `StockConfigurationInterface::getDefaultScopeId()`.
- Rimosso il riferimento a una classe MSI inesistente (`GetStockStatusSelect`).
- Il join viene fatto solo con "Display Out of Stock Products" = Sì.
- `composer.json`: tolto il campo `version` (la versione deriva dal tag), descrizione corretta, dipendenze dai
  moduli Catalog e CatalogInventory.
