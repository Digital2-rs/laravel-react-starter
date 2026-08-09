# Query Objects

**Applies to:** `app/Queries/**`

Encapsulate reusable, non-trivial Eloquent queries in `app/Queries/`. Expose a `builder(array $filters = []): Builder` method that returns an unexecuted builder for the caller to compose and execute.

```php
public function builder(array $filters = []): Builder
{
    return Partner::query()
        ->where('is_active', true)
        ->when($filters['search'] ?? null, fn (Builder $query, string $search) =>
            $query->where('name', 'like', "%{$search}%")
        );
}
```
