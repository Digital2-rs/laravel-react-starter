# PHP Style

**Applies to:** `app/**`

Inject dependencies through constructor property promotion, placing each constructor argument on its own line with a trailing comma. Use `?Type` for nullable types and declare `void` for methods that return nothing.

Use guard clauses: put unhappy paths first, avoid `else`, and prefer separate condition checks over compound conditions when practical.

```php
public function handle(?User $user): void
{
    if (! $user) {
        return;
    }

    $this->notify($user);
}
```
