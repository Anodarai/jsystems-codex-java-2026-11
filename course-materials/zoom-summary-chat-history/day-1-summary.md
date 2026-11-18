# Podsumowanie — dzień 1, 18 listopada 2026

Pierwszy dzień szkolenia „OpenAI Codex w codziennej pracy programistycznej przy projektach Java” poświęcono narzędziom agentowym, konfiguracji środowiska pracy, kontekstowi i modelom oraz umiejętnościom (skills). Ważnym wątkiem było bezpieczne rozpoczęcie pracy z nieznanym repozytorium jFTP. Prowadzący: Łukasz Matuszewski.

## Agenci, kontekst i praca programistyczna

Agent programistyczny łączy model językowy z kontekstem, instrukcjami i narzędziami, które pozwalają mu wykonywać wieloetapowe zadania. Rozmawiano o ewolucji takich narzędzi — od autouzupełniania kodu do agentów wspierających większe zadania — oraz o koncepcji Dark Factory, czyli daleko idącej automatyzacji wytwarzania oprogramowania. Taki sposób pracy wymaga określenia zakresu nadzoru nad agentem.

Kontekst modelu obejmuje informacje dostępne agentowi podczas zadania. W aplikacji Codex udostępniono ustawienie pokazujące wykorzystanie okna kontekstu; w CLI wskazano też `/statusline` i `/experimental` jako miejsca związane ze statusem i funkcjami eksperymentalnymi. Polecenie `!` pozwala uruchomić polecenie powłoki z poziomu CLI. Do diagnostyki środowiska pokazano `codex doctor`, również w wariancie `! codex doctor` wewnątrz CLI.

## Codex i środowisko pracy

Omawiano zarówno aplikację desktopową Codex, jak i Codex CLI — to różne sposoby pracy z agentem. Wspomniano także Codex AppServer, który może hostować sesje agentów; jego wersja nie musi być taka sama jak wersja CLI. Przy pracy z projektem warto jasno wskazać agentowi właściwe katalogi repozytoriów. Dla kilku repozytoriów można udostępnić osobne foldery jako część projektu.

W materiałach i na czacie udostępniono repozytorium szkoleniowe: [jsystems-codex-java-2026-11](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11). Pokazano pracę z `git`, `glab` (GitLab CLI) i forkiem repozytorium. Na Windows wskazano [Dev Drive](https://learn.microsoft.com/en-us/windows/dev-drive/) jako opcję przeznaczoną do pracy deweloperskiej i szybszych operacji na plikach. W poleceniach pojawiły się `cd D:` oraz docelowy katalog klonowania `D:\jsystems-codex-java-2026-11`.

Przykładowe polecenia diagnostyczne i nawigacyjne

```text
glab version
cd D:
codex doctor
! codex doctor
```

Do otwierania bieżącego katalogu w edytorze pokazano `code .`. Udostępniono też [Fresh](https://getfresh.dev/) jako alternatywny edytor TUI; polecenie `fresh .` otwiera bieżący folder.

## Modele i ich porównywanie

Zamiast opierać wybór modelu na pojedynczej etykiecie lub rankingu, warto porównywać jakość, czas wykonania i koszt w kontekście konkretnego zadania. Narzędzia i strony udostępnione podczas szkolenia:

- [Artificial Analysis](https://artificialanalysis.ai/) — agregator benchmarków; [Decision Index](https://artificialanalysis.ai/evaluations/artificial-analysis-decision-index) dotyczy modeli decyzyjnych, a [widok czasu względem jakości](https://artificialanalysis.ai/?intelligence-efficiency=time-per-task) ułatwia porównanie czasu wykonania.
- [Arena](https://arena.ai/) — platforma porównywania modeli. Udostępnione dema opisano etykietami [Opus 5.5](https://01a1a099-865e-7a7b-810d-0a8ec35a61b6.arena.site/), [Claude Sonnet 5.5](https://01a1ee55-7d68-7332-af6b-4d7dc60f10b4.arena.site/), [Mistral Large 4](https://01a1ee55-7d68-7239-b98d-fb6069409ccd.arena.site/), [Astra 6.2](https://01a1ee53-77fa-7884-a924-e0d4e2c8c2dc.arena.site/), [Fable 5.1 Max](https://01a1ee53-77fa-7365-9612-39e7fcda16fe.arena.site/).
- [Jev by TypeSafe](https://typesafe.ai/) — przykład modelu decyzyjnego, przeznaczonego do ustrukturyzowanych ocen i klasyfikacji.
- [Thinking Machines](https://thinkingmachines.ai/) oraz [Inkling 2 Small](https://thinkingmachines.ai/news/inkling-2-small/).
- [Qwen3.8-27B](https://huggingface.co/Qwen/Qwen3.8-27B) — przykład modelu udostępnionego na Hugging Face.

W krótkim ćwiczeniu można było zaproponować grę inspirowaną grą z dzieciństwa lub postacią z filmu albo książki, albo wybrać dowolną aplikację webową.

Omówiono także modele open source i rozwój modeli z różnych regionów. Wspomniano o buforowaniu jako elemencie pracy z modelami; szczegóły i warunki działania należy sprawdzać w aktualnych materiałach dostawcy, zamiast zakładać, że pozostają niezmienne.

## Uprawnienia i bezpieczna praca z repozytoriami

Porównano ograniczenia sandboxa, tryby wymagające zatwierdzania działań i tryb pełnego dostępu. Wybór powinien uwzględniać zaufanie do repozytorium, zakres zadania i poziom izolacji środowiska. Samo zatwierdzanie kolejnych poleceń nie zastępuje ich rozumienia ani sprawdzenia kodu. Nieznane repozytorium warto najpierw analizować w odizolowanym środowisku i nie uruchamiać pochopnie jego skryptów.

Udostępnione materiały:

- [Dokumentacja Codex: sandboxing](https://learn.chatgpt.com/docs/sandboxing?surface=app#how-you-control-it).
- [Sandboxing i mechanizmy ochronne w Codex oraz Claude Code](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/Research/Sandboxing-and-harness-in-Codex-vs-ClaudeCode.md).
- [Rozwiązywanie problemów z sandboxem Codex w Windows](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/Research/codex-windows-sandbox-troubleshooting-2026-10-15.md).
- [Konfiguracje Codex dla kursu](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/tree/main/course-materials/agent-configs/codex).

### Pierwsze zadanie analityczne: jFTP

Repozytorium [jFTP](https://github.com/sai-pullabhotla/jftp) posłużyło jako przykład projektu, który trzeba sprawdzić przed uruchomieniem. Brief zadania obejmował sklonowanie go do środowiska chmurowego Codex, użycie Code Mode i podejścia algorytmicznego do przygotowania skanowania plików pod kątem typowych oznak prompt injection i innych ryzyk, ręczne sprawdzenie wybranych plików i zależności oraz wyszukanie informacji o repozytorium i jego twórcy.

Materiały powiązane z zadaniem: [Code Mode i programowanie algorytmiczne](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/Research/code-mode-and-algorithmic-code-migration-2026-10-13.md). Polecenie klonowania jFTP

```text
git clone https://github.com/sai-pullabhotla/jftp.git
```

## Skills: struktura, instalacja i kontrola

Skill to instrukcja — często w Markdown — opisująca, kiedy i jak agent ma wykonać określony rodzaj zadania. Może zawierać dodatkowe materiały lub skrypty. Skills mogą być dostępne globalnie albo w zakresie projektu; umieszczenie ich przy projekcie ułatwia powiązanie instrukcji z repozytorium i pracą zespołu. Przed instalacją należy przejrzeć źródło i zawartość, zwłaszcza gdy skill pochodzi z nieznanego miejsca lub ma możliwość uruchamiania kodu.

Pokazane zasoby:

- [skills.sh](https://www.skills.sh/) — wyszukiwarka i menedżer skills.
- [Agent Toolbox EdukeyTeam](https://github.com/EdukeyTeam/agent-toolbox/tree/main) — repozytorium skills udostępnione do szkolenia.
- Przykładowe strony skills z oznaczeniem `security/snyk`: [create-design-system](https://www.skills.sh/edukeyteam/agent-toolbox/create-design-system/security/snyk) i [respond-to-code-review](https://www.skills.sh/edukeyteam/agent-toolbox/respond-to-code-review/security/snyk).

Polecenie podane do instalacji skills z repozytorium Agent Toolbox:

```text
npx --yes skills@latest add EdukeyTeam/agent-toolbox
```

W trakcie pracy z jFTP pojawiło się również przejście do katalogu `D:\jftp\`.

## Inne udostępnione narzędzia

- [CrewAI](https://crewai.com/) — framework do tworzenia zespołów agentów.
- [Cursor](https://cursor.com/) — edytor kodu z agentem AI. [Tabnine](https://docs.tabnine.com/main) należał do wczesnych narzędzi AI do autouzupełniania kodu. Deep TabNine pojawił się w 2019 r., a techniczna wersja zapoznawcza GitHub Copilota w 2021 r.
- [Atuin](https://atuin.sh/) — wyszukiwanie i synchronizacja historii poleceń.
- [tmux — wiki](https://github.com/tmux/tmux/wiki) i [tmux.app](https://tmux.app/) — multiplekser sesji terminalowych.
- [Omarchy](https://omarchy.org/) — środowisko Linux dla programistów; wspomniano też o Termux na Androidzie.
- [Herdr](https://herdr.dev/) — narzędzie do zarządzania wieloma agentami; udostępniono również [materiał o menedżerach agentów i zdalnych sesjach](https://github.com/LucasMatuszewski/jsystems-codex-java-2026-11/blob/main/course-materials/Research/agent-managers-and-remote-agents.md).
- [Codex CLI — dokumentacja](https://learn.chatgpt.com/docs/codex/cli) i [oficjalna instrukcja instalacji](https://learn.chatgpt.com/docs/codex/cli#getting-started) z opcją dla Windows.
- [Prezentacja wprowadzająca](https://devpowers.com/szkolenia/jsystems/codex-java-2026-11/Prezentacja_01_Start_kursu.html) i [strona szkolenia z materiałami](https://devpowers.com/szkolenia/jsystems/codex-java-2026-11/).
