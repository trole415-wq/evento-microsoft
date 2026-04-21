---
description: Agent instructions for the Soc Ops social bingo game project built with Blazor and .NET 10.
---

# Soc Ops Agent Instructions

## 📋 Development Checklist

Before making changes, verify:
- [ ] .NET 10 SDK installed: `dotnet --version`
- [ ] Build succeeds: `dotnet build SocOps/SocOps.csproj`
- [ ] Tests pass: `dotnet test` (if applicable)
- [ ] Dev server runs: `dotnet run --project SocOps/SocOps.csproj`

---

## Project Overview

**Soc Ops** is a social bingo game built with **Blazor** and **.NET 10**. Players find people matching questions to get 5 in a row to win.

- **Game**: https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/
- **Lab Guide**: https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/docs/

---

## Architecture

### Components & Services
- **`Home.razor`** → Routes to `StartScreen` or `GameScreen` based on `GameService.CurrentGameState`
- **`BingoGameService`** — State management (Start/Playing/Bingo), board, event notifications
- **`BingoLogicService`** — Pure logic: win detection, board generation

### Key Models
- `GameState` (Start, Playing, Bingo) — `Models/GameState.cs`
- `BingoSquareData` — Cell: `Id`, `Question`, `IsSelected`, `IsWinning`
- `Questions.cs` — ~25 questions, randomly shuffled per game

---

## Blazor Essentials

- **Binding**: `@bind-value`, `@bind` for two-way sync
- **Events**: `@onclick`, `@onchange`; use `[Parameter]` for callbacks
- **Lifecycle**: Subscribe to `GameService.OnStateChanged` in `OnInitializedAsync()`, unsubscribe in `Dispose()`
- **Routing**: `/` route in `Home.razor` via `App.razor` router

---

## Styling

Use CSS utilities from `wwwroot/css/app.css`: `.flex`, `.flex-col`, `.grid`, `.grid-cols-5`, `.p-1`–`.p-6`, `.mb-2`–`.mb-8`, `.gap-1`.

Refer to `.github/instructions/css-utilities.instructions.md` and `frontend-design.instructions.md` for design patterns.

---

## Common Tasks

**Add Bingo Question**: Edit `Data/Questions.cs`, add string to list.

**Change Board Size**: Update dimensions in `BingoGameService.cs`, change `.grid-cols-5` in `BingoBoard.razor`.

**Style Components**: Use CSS utilities or add `.razor.css` files (e.g., `BingoBoard.razor.css`).

**Debug State**: `OnStateChanged` fires on state updates; components re-render via `StateHasChanged`.

---

## File Structure

```
SocOps/
  Components/       → Razor UI components
  Services/         → BingoGameService, BingoLogicService
  Models/           → GameState, BingoSquareData, BingoLine
  Pages/            → Home.razor (main entry)
  Data/             → Questions.cs
  wwwroot/css/      → Utility classes (app.css)
```

---

## Code Principles

- **Separation**: Services = state/logic; Components = UI/events
- **Event-Driven**: State propagates via `OnStateChanged`
- **Reusable**: `BingoSquare`, `BingoModal` are generic
- **No External Deps**: .NET Standard libraries only

---

## Resources

- [Blazor Docs](https://learn.microsoft.com/en-us/aspnet/core/blazor/?view=aspnetcore-10.0)
- [.NET 10 Docs](https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-10)
