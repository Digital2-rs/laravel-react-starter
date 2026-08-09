# Services And Jobs

**Applies to:** `app/Services/**`, `app/Jobs/**`

Place external-system wrappers in `app/Services/` and name them after the system without a `Service` suffix. Name jobs as the verb-and-object work they perform without a `Job` suffix.

```php
final class Erp
{
    // External ERP integration.
}

final class SyncErpPrices implements ShouldQueue
{
    // Synchronizes ERP prices.
}
```
