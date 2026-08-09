# Form Requests

**Applies to:** `app/Http/Requests/**`

Validate request input with Form Requests. Write each field's validation rules in array notation, never pipe-delimited strings.

```php
public function rules(): array
{
    return [
        'email' => ['required', 'email'],
        'name' => ['required', 'string', 'max:255'],
    ];
}
```
