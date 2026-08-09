# Data Objects

**Applies to:** `app/DataObjects/**`, `app/Actions/**`, `app/Http/Controllers/**`

Pass application data with Spatie Data DTOs in `app/DataObjects/`. Name them with the `Data` suffix and use typed, promoted `public readonly` properties.

Build DTOs from validated Form Request data with `::from()` before passing them to an Action; Actions do not accept raw arrays.

```php
final class AddressData extends Data
{
    public function __construct(
        public readonly string $street,
        public readonly bool $isDefault = false,
    ) {}
}

$address = $createAddress->handle($partner, AddressData::from($request->validated()));
```
