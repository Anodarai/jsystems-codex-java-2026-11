# Podsumowanie — dzień 2, 19 listopada 2026

## Zakres dnia

Dzień 2 szkolenia JSystems dla grupy 2 dotyczył pracy z dużym, starszym kodem na przykładzie jFTP oraz sposobów, które pomagają agentowi poznać repozytorium bez ładowania całego kodu do kontekstu. Omawiano mapowanie kodu, kompresję, dokumentowanie architektury, instrukcje i skille, zarządzanie sesją oraz przygotowanie bezpiecznej ścieżki do późniejszej modernizacji.

## Analiza repozytorium i artefakty

W ćwiczeniu z jFTP polecano przygotować RepoMap, następnie Repomix, jego skompresowaną wersję bez komentarzy oraz graf kodu z wizualizacją. RepoMap pokazuje symbole i strukturę repozytorium w zwięzłej postaci; Repomix pakuje wybrany kod do analizy, a graf pomaga zobaczyć zależności między elementami. Prowadzący wskazał `docs/` jako miejsce na mapę i osobny podkatalog na jej artefakty. Porównanie wersji Repomix z komentarzami i bez nich pokazuje, jak kompresja może zmniejszyć liczbę tokenów.

Materiały do ćwiczenia obejmują [Repomix](https://repomix.com/), [Aider RepoMap](https://aider.chat/docs/repomap.html) i [Graphify](https://github.com/Graphify-Labs/graphify).

## Instrukcje, skille i dokumentacja

Rozmowa objęła `AGENTS.md`, skille i własnych subagentów. Praktyczny przykład ustawień rozdzielał polski język rozmowy od angielskiego języka dokumentacji, komentarzy i kodu, z preferencją zwięzłych odpowiedzi. Do Spec-Driven Development wskazano [Spec Kit](https://github.com/github/spec-kit), [specs.md](https://specs.md/) oraz skille wyszukiwane według haseł [spec](https://www.skills.sh/?q=spec), [prd](https://www.skills.sh/?q=prd), [adr](https://www.skills.sh/?q=adr), [plan](https://www.skills.sh/?q=plan). Pokazano też [własnych subagentów Codex](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/tree/main/course-materials/agent-configs/codex/agents), [slajd o AGENTS.md](https://devpowers.com/szkolenia/jsystems/codex-java-2026-11/Prezentacja_04_Workflow.html#4) oraz przykłady użycia skilli do diagramów Mermaid i dokumentacji ADR. Do diagramów udostępniono [design-doc-mermaid](https://github.com/SpillwaveSolutions/design-doc-mermaid) oraz [instrukcję diagramów architektury](https://github.com/EdukeyTeam/agent-toolbox/blob/main/skills/legacy-codebase-workflows/references/architecture-diagrams.md).

W materiałach znalazły się również [Caveman](https://github.com/juliusbrussee/caveman) i [Ponytail](https://github.com/dietrichgebert/ponytail) jako podejścia do ograniczania nadmiarowego tekstu i inżynierii. W czacie podano konkretną komendę instalacji Ponytail: `npx skills add https://github.com/dietrichgebert/ponytail --skill ponytail`. Wspomniano także o Beads jako narzędziu pracy z zadaniami i pamięcią agentów oraz o Dolt jako bazie łączącej podejście bazodanowe z historią zmian: [Beads](https://github.com/gastownhall/beads), [Dolt](https://github.com/dolthub/dolt).

## Kontekst i narzędzia pracy

Wskazano [Tokenizer OpenAI](https://platform.openai.com/tokenizer) do oglądania podziału tekstu na tokeny. `/compact` służy do skrócenia historii sesji, ale powstałe podsumowanie może pominąć szczegóły; nowa sesja jest alternatywą, gdy potrzebny jest odświeżony kontekst. Jako narzędzia dyktowania omówiono [Handy](https://handy.computer/) i model Canary 1B v2 dla polskiego rozpoznawania mowy. W CLI pokazano `/resume`, `/voice`, podwójne `Esc` do widoku transkrypcji, nawigację strzałkami po historii promptów i `Enter` do cofnięcia promptu. `Ctrl+G` otwierał skonfigurowany edytor Micro; wskazano skróty `Ctrl+S` do zapisu i `Ctrl+Q` do wyjścia ([Micro](https://micro-editor.github.io/)).

MCP przedstawiono jako standard udostępniania narzędzi agentom, w tym przez własne serwery: [wprowadzenie do MCP](https://modelcontextprotocol.io/docs/2026-07-28/getting-started/intro), [budowa serwera](https://modelcontextprotocol.io/docs/2026-07-28/develop/build-server). Pobieranie dokumentacji przez Context7 zaplanowano na kolejny dzień.

## Testy i planowanie modernizacji jFTP

W rozmowie pokazano polecenia tworzenia testów charakteryzacyjnych i regresyjnych na podstawie istniejącego kodu. Warto ręcznie sprawdzić, jakie zachowania pokrywają testy wygenerowane przez agenta. Najpierw wprowadzić minimalne zmiany potrzebne do uruchomienia aplikacji i uruchomić testy. Jeśli regresja pojawi się po zmianie, zacząć diagnozę od kodu, który ją wprowadził. Dopiero po uzyskaniu działającej, przetestowanej bazy przechodzić do większej refaktoryzacji i wykonywać zmiany w małych, czytelnych commitach.

Planowanie odbyło się w Plan Mode (`Shift+Tab` lub `/plan`). Zaobserwowano, że plan nie został zapisany do pliku w tym trybie; prowadzący wyszedł z niego i osobno poprosił o zapis. Następnie rozpoczął nową sesję przez `/new` i uruchomił cel poleceniem `/goal implement this plan fully docs\modernization-plan.md`. Odpowiedzi zapisane w czacie wybrały Java 25 LTS jako cel, zachowanie kompatybilności FTP, weryfikację najpierw na Windows oraz wycofanie osobnego appletu. Podczas uruchamiania planu instalacja Maven wymagała dodatkowej zgody mimo „Approve for me”. Warto obserwować początek pracy agenta, żeby zauważyć takie blokady. [Przykładowy prompt modernizacji jFTP](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/Prompt%20examples/Legacy-Code-JFTP-modernization.md)

## Dalszy ciąg

Na 20 listopada zaplanowano dalszą pracę nad jFTP, przegląd i wykonanie planu, demonstrację Context7 oraz weryfikację zmian. [Lista zadań na jutro](./day-2-chat-history.md#lista-zada%C5%84-na-jutro)
