# Enums

**Applies to:** `app/Enums/**`, `app/Models/**`

Use native enums in `app/Enums/`, named in PascalCase without an `Enum` suffix, with PascalCase cases. Use backed string enums with explicit values for persisted state and cast them on the model.

```php
enum UserRole: string
{
    case Admin = 'admin';
    case Partner = 'partner';
}

protected function casts(): array
{
    return ['role' => UserRole::class];
}
```
