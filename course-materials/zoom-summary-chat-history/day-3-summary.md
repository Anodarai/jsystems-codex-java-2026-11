# Podsumowanie — dzień 3, 20 listopada 2026

## Praca z agentami w trybie headless

W trybie headless agent wykonuje zadanie przekazane z CLI i zwraca wynik, który można wykorzystać w skrypcie. Pokazano przykłady użycia Codex przez `codex exec` oraz Claude przez `claude -p "prompt"`. Opcja `--json` pozwala odczytać zdarzenia i statystyki użycia w formie strumienia JSON. Wśród omawianych narzędzi znalazły się [OpenCode](https://opencode.ai/) i [Pi](https://pi.dev/). OpenCode zaproponowano jako zewnętrznego agenta do eksploracji repozytorium.

Przy zadaniu delegowanym agentowi warto określić cel, zakres i oczekiwany wynik. Zespołem agentów może kierować orkiestrator, który rozdziela pracę według kompetencji, koordynuje wykonanie i sprawdza jakość. W omawianym przykładzie Sol był proponowany do generowania kodu, Luna do eksploracji, czytania plików i researchu, a Astra do wyjątkowo trudnych zadań.

## Dokumentacja i Context7

Przy pytaniu o lokalne narzędzie CLI najpierw sprawdź jego wbudowaną pomoc. W przypadku dokumentacji bibliotek i zależności użyj Context7, a zwykłe wyszukiwanie w internecie pozostaw jako dalszy krok, gdy wcześniejsze źródła nie wystarczą. [Context7](https://context7.com/) zwraca fragmenty dokumentacji dobrane do zapytania, co pomaga ograniczyć ilość tekstu trafiającego do kontekstu.

Pokazano konfigurację MCP dla Codex, w tym `npx ctx7 setup --codex`, `codex mcp login context7` oraz przykładową konfigurację z adresem `https://mcp.context7.com/mcp`. Udostępniono też przykład lokalnego serwera MCP uruchamianego przez `npx`. W przykładzie adres serwera i odwołanie do zmiennej środowiskowej zapisano w konfiguracji MCP. Osobno pokazano materiały do [indeksowania własnego kodu lub dokumentacji](https://github.com/EdukeyTeam/agent-toolbox/tree/main/skills/legacy-codebase-workflows/assets/context7).

## Planowanie implementacji i delegowanie

Plan implementacji powinien opisywać zakres, kolejność prac, kryteria akceptacji i sposób koordynacji. Szczegóły zakresu i decyzji pozostają w PRD, ADR i pozostałej dokumentacji. Plan odsyła do tych źródeł. Przed rozpoczęciem prac należy porównać plan z instrukcjami `AGENTS.md`, dokumentacją projektu i opisem architektury oraz rozstrzygnąć sprzeczności.

Przykład planowania pokazano na [gałęzi `docs/modernization-plan` w repozytorium jFTP](https://github.com/LucasMatuszewski/jftp-2026-11-06/tree/docs/modernization-plan). Zakładany przebieg obejmował najpierw minimalne zmiany potrzebne do uruchomienia aplikacji i sprawdzenie testów, a następnie właściwą modernizację, aktualizację zależności i standardów Java oraz granularne commity. Gdy po zmianie test przestaje przechodzić, diagnozę zacznij od zmienionego kodu.

Prowadzący rozpoczął nową sesję poleceniem `/new` i przekazał plik planu do `/goal`. Pokazał też monitor komentarzy do przeglądu kodu, który sprawdzał je co pięć minut do ustalonego limitu czasu. [Skill do obsługi uwag z przeglądu kodu](https://github.com/EdukeyTeam/agent-toolbox/tree/main/skills/respond-to-code-review)

[Skill `write-implementation-plan`](https://github.com/LucasMatuszewski/jftp-2026-11-06/tree/docs/modernization-plan/.agents/skills/write-implementation-plan) umieszczono w repozytorium projektu, pod `.agents/skills/`. Domyślnym miejscem na plany jest `docs/plans/`. Omawiana konwencja zakłada briefy dla delegowanych zadań, również dla agentów CLI. Brief powinien zawierać instrukcje wystarczające do wykonania przydzielonej pracy bez podejmowania przez podagenta kluczowych decyzji. Briefy powiązane z planem trafiają do `docs/.briefs/<plan-name>`. Commituj je w trakcie realizacji, a po zakończeniu usuń wraz z planem. Najpierw rozdziel zakresy pracy między agentów. Rozważ `git worktree`, gdy muszą równolegle zmieniać te same pliki. [Dokumentacja Git worktree](https://git-scm.com/docs/git-worktree)

## Integracje z GitHub i GitLab

Omówiono trzy sposoby łączenia agentów z usługami repozytoriów: wbudowane konektory, dostęp przez CLI i serwery MCP. [GitHub MCP Server](https://github.com/github/github-mcp-server) · [GitLab MCP](https://docs.gitlab.com/user/model_context_protocol/mcp_server/) · [GitLab CLI](https://docs.gitlab.com/cli/)

Przy tokenach PAT obowiązuje zasada najmniejszych uprawnień: przyznawaj tylko dostęp potrzebny do konkretnego zadania, ograniczaj zakres repozytoriów i unikaj zbędnych uprawnień zapisu. Integrację można wykorzystać m.in. w pracy z kodem i pull requestami, a GitLab MCP lub CLI skonfigurować dla własnego środowiska.

## Środowiska, testowanie i automatyzacja

Środowiska chmurowe pozwalają uruchamiać pracę agenta poza lokalnym komputerem. Materiał o środowiskach Codex: https://learn.chatgpt.com/docs/environments/cloud-environments. Tailscale (https://tailscale.com/) przedstawiono jako sposób łączenia urządzeń, takich jak komputer, telefon czy VPS, we wspólną prywatną sieć.

Do testowania aplikacji webowych pokazano Playwright CLI lub MCP, a do aplikacji desktopowych computer use. Automatyzacja istniejącej, zalogowanej karty przeglądarki może wymagać rozszerzenia i dodatkowych uprawnień. Chrome DevTools MCP: https://github.com/ChromeDevTools/chrome-devtools-mcp. Podłączenie do działającej instancji Chrome może dać narzędziu dostęp do otwartych kart i ich danych, dlatego należy ograniczyć użycie do zaufanego środowiska i nie podłączać go bez potrzeby.

Przykłady konfiguracji Codex, reguł, uprawnień, hooków i CI/CD udostępniono w materiałach kursowych: https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/tree/main/course-materials. Przykłady CI/CD dla headless Codex i innych narzędzi: https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/tree/main/course-materials/cicd-headless. Pokazano też PR-Agent: https://github.com/The-PR-Agent/pr-agent.

## Konfiguracja bezpieczeństwa Codex

Sandbox ogranicza środowisko wykonania. Profile uprawnień i reguły poleceń pozwalają doprecyzować dostęp agenta. Profile uprawnień można definiować w `config.toml` lub osobnym `.codex/permissions.toml`; przykład i opis są w [materiałach o profilach uprawnień](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/agent-configs/codex/PERMISSIONS.md). Reguły można umieszczać w `.codex/rules/<name>.rules`. Zademonstrowana reguła blokowała jawne prefiksy poleceń `git push` dla wybranych nazw zdalnych i gałęzi. Przykład działa na jawnych prefiksach poleceń. Ochronę gałęzi ustawia się również po stronie serwera repozytorium. [Przykładowa reguła kursowa](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/agent-configs/codex/rules/course.rules) Hooki Codex SDK pozwalają uruchamiać działania przy zdarzeniach cyklu życia, takich jak rozpoczęcie sesji lub użycie Bash; przykłady: https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/tree/main/course-materials/hooks-example.
