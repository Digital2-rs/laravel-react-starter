# Actions

**Applies to:** `app/Actions/**`, `app/Http/Controllers/**`

Implement business operations as Actions in `app/Actions/<Domain>/`, named with a PascalCase verb and noun. Controllers delegate application logic to Actions.

An Action has exactly one public method, `handle()`. Inject dependencies through its constructor, accept typed models, DTOs, or primitives, return a result rather than an HTTP response, and wrap data mutations in `DB::transaction()`.

```php
final class CreateAddress
{
    public function handle(Partner $partner, AddressData $data): Address
    {
        return DB::transaction(fn (): Address => $partner->addresses()->create($data->toArray()));
    }
}
```

```php
final class AddressController
{
    public function store(AddressRequest $request, CreateAddress $createAddress): RedirectResponse
    {
        $address = $createAddress->handle(
            $request->user()->partner,
            AddressData::from($request->validated()),
        );

        return to_route('addresses.show', $address);
    }
}
```
