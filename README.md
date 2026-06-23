# DG2 Starter Kit

An opinionated Laravel + Inertia (React) starter kit with strong conventions, typed routing, and AI agent tooling baked in. Built for shipping features fast without sacrificing structure.

## Stack

| Layer       | Tech                                                        |
| ----------- | ---------------------------------------------------------- |
| Backend     | PHP 8.4 · Laravel 13 · Inertia v3                           |
| Frontend    | React 19 · TypeScript · Tailwind CSS v4 · Vite             |
| Data / DTOs | Spatie Laravel Data                                        |
| Routing     | Laravel Wayfinder (typed route functions for the frontend) |
| Models      | Unguarded via `nunomaduro/essentials`                      |
| Testing     | Pest v4 · PHPUnit v12                                       |
| Quality     | Pint · Larastan (PHPStan) · ESLint · Prettier              |
| DX          | Laravel Boost (MCP) · Pail · Sail                          |

## Architecture

The app layer is organized by responsibility, not by Laravel defaults alone:

```
app/
├── Actions/       Single-purpose use cases (handle()), grouped by domain
├── DataObjects/   Spatie Data DTOs (typed, readonly)
├── Queries/       Query objects returning Builders
├── Models/        Unguarded, casts() method, #[Scope] attributes
├── Policies/      Authorization
├── Services/      System integrations (no Service suffix)
├── Http/          Controllers, Requests, Middleware
├── Jobs/ Events/ Listeners/ Notifications/ Support/ Enums/
```

Frontend lives in `resources/js`:

```
resources/js/
├── pages/      Inertia pages (kebab-case .tsx)
├── actions/    Wayfinder-generated controller calls
├── routes/     Wayfinder-generated named routes
├── lib/ types/ wayfinder/
```

## Conventions

This kit ships with enforced conventions (see `.claude/skills/laravel-conventions`). Highlights:

- **Actions** — `Verb + Noun + Action`, one public `handle()`, DI via constructor, mutations wrapped in `DB::transaction()`.
- **DTOs** — Spatie Data with `Data` suffix; no raw arrays into Actions.
- **Query objects** — expose `builder(array $filters = []): Builder`.
- **Models** — no `$fillable`/`$guarded`; safety at the input boundary. Casts via `casts()`, scopes via `#[Scope]`.
- **Migrations** — forward-only (no `down()`); `foreignId()->index()` without `->constrained()`.
- **Frontend** — kebab-case `.tsx`, page-scoped components colocated, shadcn/ui components.
- **Routing** — use Wayfinder route functions, not hardcoded URLs.

## AI Agent Tooling

Pre-configured for multiple agent runtimes: `CLAUDE.md` / `.claude`, `AGENTS.md`, `.codex`, `.agents`, `.ai`, and `opencode.json`. Laravel Boost runs as an MCP server (`.mcp.json`) giving agents docs search, DB schema, and log access.

## Getting Started

```bash
# Install deps, copy env, generate key, migrate, build assets
composer setup

# Run everything (server, queue, logs, vite) in one command
composer dev
```

The app is served by Laravel Herd at `https://dg2-starter.test`.

## Common Commands

```bash
composer dev          # server + queue + logs + vite (concurrently)
composer test         # lint:check + types:check + Pest
composer lint         # Pint (fix)
composer ci:check     # full CI gate: eslint + prettier + phpstan + tests

php artisan test --compact
vendor/bin/pint --dirty       # format changed PHP
npm run dev / npm run build   # frontend assets
```

## Quality Gates

- **Pint** — PHP code style
- **Larastan** — static analysis (`composer types:check`)
- **ESLint + Prettier** — frontend lint/format
- **Pest** — feature + unit tests

Run `composer ci:check` before pushing.
