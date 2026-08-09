# Models

**Applies to:** `app/Models/**`

Define casts in a `protected casts(): array` method. Define local scopes as protected methods marked with `#[Scope]`, without a `scope` method-name prefix.

Do not declare `$fillable` or `$guarded`; only persist explicit, validated DTO data. Put every trait declaration on its own `use` line.

```php
#[Scope]
protected function active(Builder $query): void
{
    $query->where('is_active', true);
}

protected function casts(): array
{
    return ['is_active' => 'boolean'];
}
```
