# Controllers

**Applies to:** `app/Http/Controllers/**`

Resource controllers use the resource name with the `Controller` suffix and only standard CRUD methods: `index`, `create`, `store`, `show`, `edit`, `update`, and `destroy`.

Implement non-CRUD endpoints as invokable, action-named controllers with the `Controller` suffix.

```php
final class SetDefaultAddressController
{
    public function __invoke(Address $address, SetDefaultAddress $setDefaultAddress): RedirectResponse
    {
        $setDefaultAddress->handle($address);

        return to_route('addresses.show', $address);
    }
}
```
