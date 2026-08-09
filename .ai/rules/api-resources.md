# API Resources

**Applies to:** `app/Providers/**`, `app/Http/Resources/**`

Disable the JSON resource `data` wrapper once in a service provider with `JsonResource::withoutWrapping()`. API resources return flat response payloads.

```php
public function boot(): void
{
    JsonResource::withoutWrapping();
}
```
