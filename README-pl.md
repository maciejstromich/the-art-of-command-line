[ Dostępne tłumaczenia:
[English](README.md), [Español](README-es.md), [Italiano](README-it.md), [日本語](README-ja.md), [한국어](README-ko.md), [Polski](README-pl.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [Українська](README-uk.md), [中文](README-zh.md)
]


# Sztuka posługiwania się linią komend

[![Przyłącz się do rozmowy na https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Podstawy](#podstawy)
- [Codzienne użytkowanie](#codzienne-użytkowanie)
- [Przetwarzanie plików i danych](#przetwarzanie-plików-i-danych)
- [Degubowanie systemu](#debugowanie-systemu)
- [Jednolinijkowce](#jednolinijkowce)
- [Niejasne ale przydatne](#niejasne-ale-przydatne)
- [Tylko dla OS X](#tylko-dla-osx)
- [Więcej zasobów](#więcej-zasobów)
- [Oświadczenie](#oświadczenie)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

Płynność w posługiwaniu się linią komend jest umiejętnością często zaniedbywaną albo uznawaną za wiedzę tajemną, która poprawia twoją zwinność i produktywność jako inżyniera. Dokument ten jest zbiorem notatek i wskazówek na temat korzystania z linii poleceń, które uznałem za użyteczne podczas pracy z systemem Linuks. Znajdziesz tutaj wskazówki o różnym stopniu zaawansowania. Ta strona nie jest zbyt długa, ale jeśli potrafisz z pamięci użyć zawarte tutaj komendy, wiesz naprawdę sporo.

Praca jest wynikiem współpracy [wielu autorów i tłumaczy](AUTHORS.md).
Wiele z zawartych tutaj informacji 
[oryginalnie](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[pojawiło się](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
na [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
i widząc zaintereowanie tam, wydało mi się, iż użycie Githuba ma większy sens, gdzie ludzie z większym talentem niż autor oryginalnego postu mogliby proponować ulepszenia. Jeśli widzisz błąd albo coś co może być przedstawione lepiej, zgłość go albo dostarcz rozwiązanie w postaci PR! (Oczywiście należy najpierw zapoznać się z sekcją Meta tego dokumentu jak i istniejącymi PR/błędami)

## Meta

Cel dokumentu:

- Ten przewodnik jest zarówno dla początkujących jak i zaawansowanych. Celem jest *zakres* (wszystko jest ważne), *specyficzność* (daj konkretne przykłady najpopularniejszych przypadków użycia) oraz *treściwość* (unikaj rzeczy które nie są istotne albo dygresji które można wyszukać gdzieś indziej). Każda wskazówka jest ważna: w jakimś konkretnym przypadku lub gdy znacząco skraca czas nad alternatywami.
- Jest przeznaczony dla osób pracujących w systemie Linux, z wyjątkiem sekcji "[Tylko dla OS X](#tylko-dla-osx)". Wiele z opisanych przykładów tyczy się także innych Unixów lub MacOS (albo nawet Cygwin).
- Skupiamy się głównie na interaktywnym Bashu, mimo iż wiele wskazówek może zostać użyta w innych powłokach oraz w skryptach bashowych.
- Zawiera zarówno "standardowe" komendy Unixa, jak również te które wymagają specjalnych doinstalowanych paczek -- o ile są wystarczająco ważne aby zasłużyć na włączenie ich do dokumentu.

Notatki:

- Aby utrzymać dokument jako jedną stronę, zawartość jest domyślnie zawarta w formie odniesień. Jesteś wystarczająco mądry aby poszukać detali gdzieś indziej (np. w wyszukiwarce Google) kiedy rozumiesz już ideę albo komendę. Używaj `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` (w zależności od systemu z którego korzystasz) aby zainstalować nowe programy.
- Używaj [Explainshell](http://explainshell.com/) aby otrzymać pomocne informacje na temat komendy, opcji, potoku, itd. 


## Podstawy

- Naucz się podstaw Basha. , Wpisz `man bash` i przynajmniej przejrzyj całość; jest prosto napisana i niezbyt długia. Alternatywne powłoki mogą być fajne, ale Bash jest potężny i zawsze dostępny. (nauka *tylko* zsh, fish, itd., mimo, że kuszące na swoim laptopie, ogranicza Cię w wielu sytuacjach, na przykład w interakcji z istniejącymi już serwerami).

- Naucz się chociaż jednego tekstowego edytora. Idealnie było by nauczyć się Vim (`vi), ponieważ nie ma sobie równych przy przypadkowym edytowaniu plików e terminalu (nawet jeśli używasz Emacsa, złożonego IDE albo nowego hipsterskiego edytora większość czasu).

- Umiej czytać dokumentację używając `man` (dla ciekawych, `man man` listuje numery sekcji, np. 1 to "zwyczajne" komendy, 5 to pliki/konwencje, a 8 są przeznaczone dla administracji). Wyszukiwanie stron manuali odbywa się z pomocą komendy `apropos`. Wiedz, że część komend nie plikami wykonywalnymi, ale są wbudowane w Basha i możesz otrzymać pomoc na temat ich użycia przez wywołanie komendy `help` oraz `help -d`.

- Naucz się przekierowań wyjścia i wejścia przy pomocy `>` oraz `<` i potoków `|`. Wiedz, że `>` nadpisuje plik wynikowy, a `>>` dołącza do pliku wynikowego. Naucz się o standardowym strumieniu wyjścia oraz standardowym strumieniu błędów (stdout i stderr).

- Naucz się obsłudze symboli wieloznacznych (globbing) `*` (i może `?` oraz `[`...`]`). Zrozum różnice pomiędzy pomiędzy pojedyńczym `'` oraz podwójnym `"` cudzysłowem. (Więcej na temat rozwijania zmiennych znajdziesz poniżej.)

- Umiej zarządzać zadaniami w Bashu: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, itd.

- Poznaj `ssh` oraz podstawy uwierzytelniania bez użycia haseł poprzez `ssh-agent`, `ssh-add`, itd.

- Podstawoe zarządzanie plikami: `ls` oraz `ls -l` ( w szczególności, naucz się co oznacza każda kolumna), `less`, `head`, `tail` and `tail -f` (albo lepiej `less +F`), `ln` oraz `ln -s` (naucz się różnic pomiędzy twardymi i miękkimi linkami), `chown`, `chmod`, `du` (dla szybkiego podsumowania użycia dysku: `du -hs *`). Zarządznie systemem pliku, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`. Naucz się co to jest i-węzeł (`ls -i` or `df -i`).

- Podstawowe zarządzanie siecią: `ip` oraz `ifconfig`, `dig`.

- Umiej używać wyrażeń regularnych oraz różnych argumentów w `grep`/`egrep`. Warte poznania są: `-i`, `-o`, `-v`, `-A`, `-B` oraz `-C`.

- Naucz się używać `apt-get`, `yum`, `dnf` or `pacman` (w zależności od dystrybucji) aby wyszukiwać i instalować paczki oprogramowania. Upewnij się że masz zainstalowanego `pip` aby zarządzać zależnościami pythonowymi (używane poniżej zależności najłatwiej zainstalować używając `pip`).


## Codzienne użytkowanie

- W Bash, używaj **Tab** aby uzupełnić argumenty lub wylistować wszystkie dostępne komendy oraz **ctrl-r** aby przeszukiwać historię komend (po naciśnięciu kombinacji zacznij wpisywać wyszukiwaną komendę, naciskaj **ctrl-r** aby przeskakiwać pomiędzy wynikami, naciśnięcie **Enter** wykona znalezioną komendę, a naciśnięcie strzałki w prawo pozwoli Ci edytować aktualną linijkę).

- W Bash, użycie **ctrl-w** usunie ostatnie słowo, a **ctrl-u** usunie wszystko do początku linii. Użyj **alt-b** oraz **alt-f** aby przemieszczać się co wyraz, **ctrl-a** aby ustawić kursor na początek linii, **ctrl-e** aby ustawić kursor na końcu linii, **ctrl-k** aby usunąć wszystko do końca linii, **ctrl-l** aby wyczyścić ekran. Sprawdź `man readline` w poszukiwaniu wszystkich podstawowych skrótów klawiaturowych w Bashu. Jest ich całkiem sporo. Na przykład: **alt-.** przeskakuje po poprzednich argumentach, a **alt-*** rozwija symbol wieloznaczny.

- Alternatywnie, jeśli wolisz skróty klawiaturowe używane w vi, wpisz `set -o vi` (`set -o emacs` przywróci poprzedni tryb).

- Aby edytować długie komendy, po ustawieniu edytora (na przykład `export EDITOR=vim`), należy przycisnąć **ctrl-x** **ctrl-e**. Jeśli preferujesz styl vi, użyj **escape-v**

- `history` pokazuje ostatnio używane komendy. Jest też wiele skrótów, takich jak `!$` (ostatni argument) oraz `!!` (ostatnia komenda), ale te są często łatwozastępowalne przez **ctrl-r** i **alt-.**.

- Aby powrócić do poprzedniego katalogu domowego użyj `cd -`

- Jeśli jesteś w połowie wprowadzania komendy i się rozmyślisz, naciśnij **alt-#** aby dodać `#` na początku linii (komentarz) albo użyj **ctrl-a**, **#**, **Enter**. Będziesz mógł wrócić do niej później poprzez historię komend.

- Używaj `xargs` (albo `parallel`). Zauważ że możesz kontrolować ilość obiektów wykonywanych per linia (`-L`) jak również równolegle wykonanie komend (`-P`). Jeśli nie jesteś pewny jak dana komenda zadziała możesz najpierw użyć `xargs echo`. `-I{}` jest także przydatne. Przykłady:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` jest pomocne do wyświetlenia drzewa procesów.

- Użyj `pgrep` oraz `pkill` aby wyszukac lub wysłać sygnał do procesów używając nazwy procesu (`-f` jest pomocne)

- Znaj sygnały które możesz wysłać do procesu. Na przykład, aby zwiesić process, użyj `kill -STOP [numer procesu]`. Aby zobaczyć pełną listę, sprawdź `man 7 signal`.

- Użyj `nohup` oraz `disown` jesli checsz aby process w tle działał cały czas.

- Aby sprawdzić jakie procesy nasłuchją w sieci użyj `netstat -lntp` lub `ss -plat` (dla TCP; aby wylistować procesy nasłuchujące na UDP dodaj `-u`).

- `lsof` listuje aktualnie otwarte pliki i gniazda.

- `uptime` lub `w` podaje informacje jak długo system działa.

- `alias` tworzy skróty dla często używanych komend. Na przykład `alias ll='ls -latr'` tworzy nowy alias ``ll`.

- W skryptach bashowych, `set -x` (lub inny wariant `set -v`, który loguje nieprzetworzone informacje, włączając to nierozwinięte zmienne oraz komentarze) używany jest do debugowania. Używaj tryby rygorystycznego `set -e` aby przerywać działanie w przypadku wystąpienia błędu (program skończy działanie z niezerowym kodem wyjścia). Użyj `set -u` aby wykrywać niestworzone nazwy zmiennych. Rozważ także użycie `set -o pipefail` jeśli używasz potoków (poczytaj na temat potoków jako iż temat ten jest bardzo subtelny. Dla bardziej zawiłych skryptów użyj `trap` podczas EXIT albo ERR. Wyłapiesz w ten sposób pospolite błędy, przerwiesz działanie oraz wypiszesz komunikat.
```bash
      set -euo pipefail
      trap "echo 'error: Script failed: see failed command above'" ERR
```

- W skryptach bashowych, podpowłoki (zapisane w nawiasach) są wygodnym sposobem aby grupować wykonywane komendy. Często używanym przykładem jest tymczasowe przeniesienie się do innego katalogu roboczego, np.:
```bash
      # zrób coś w katalogu roboczym
      (cd /jakis/inny/katalog && inna-komenda)
      # zrób coś w oryginalnym katalogu roboczym
```

- W Bashu jest wiele sposobów pracy ze zmiennymi. Sprawdzanie czy zmienna istnieje: `${nazwa:?komunikat błędu}`. Na przykład, jeśli skrypt wymaga jednego argumentu użyj: `input_file=${1:?użycie: $0 input_file}`. Rozwinięcie arytmetyczne: `i=$(( (i + 1) % 5 ))`. Sekwencje: {1..10}`. Przycinanie ciągów: `${var%suffix}` and `${var#prefix}`. Na przykład jeśli var=foo.pdf, to `echo ${var%.pdf}.txt` wypisze `foo.txt`.

- Rozwinięcie nawiasowe przy użyciu `{`..`}` może zmniejszyć ilość podobnego tekstu i zautomatyzować kombinację obiektów. Na przykład `mv foo.{txt,pdf} katalog/` przeniesie dwa pliki do katalog, `cp somefile{,.bak}` (jest skrótem: `cp somefile somefile.bak`) albo `mkdir -p test-{a,b,c}/subtest-{1,2,3}` (która zostanie zinterpretowana jako stworzenie wszystkich możliwych kombinacji katalogów).

- Wyjście może zostać potraktowane jako plik przez użycie `<(jakaś komenda)`. Na przykład, aby porównać lokalny i zdalny plik `/etc/hosts`:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Poznaj "here documents" w Bashu: `cat <<EOF ...`.

_ W Bashu przekierowanie standardowego strumienia wyjścia i standardowego strumienia błędu przy pomocy: `komenda >plik_loga 2>&1` lub `komenda &> plik_loga`. Aby upewnić się, że komenda nie zostawi otwartego uchwytu do standardowego strumieniu wejścia, przywiązującego ją do terminala w którym się znajdujesz, często używa się `</dev/null`.

- Użyj `man ascii` aby zobaczyć tablicę ASCII z wartościami decymalnymi i hexadecymalnymi. Aby zajrzeć do ogólnej informacji o enkodowaniu użyj `mn unicode`, `man utf-8` oraz `man latic1`.

- `screen` lub [`tmux`](https://tmux.github.io/) zmultipleksuje terminal. Jest to szczególnie przydatne podczas zdalnych sesji ssh kiedy potrzeba się odłączyć i podłączyć od sesji. `byobu` jest rozszerzeniem `screen` i `tmux`, które dostarcza więcej informacji oraz łatwiejsze zarządzanie. `dtach` jest minimalistyczną alternatywą dla trwałości sesji.

- Użyj `-L` lub `-D` (oraz okazjonalnie `-R`) aby przetunelować port przy pomocy ssh. Jest to przydatne, np. aby otworzyć stronę używając zdalny serwer.

- Kilka optymalizacji lokalnej konfiguracji ssh. Przykład `~/.ssh/config` zamieszczony poniżej zawiera ustawienia które unikają zamykania połączenia w niektórych środowiskach sieciowych, używa kompresji (która jest przydatna podczas używania `scp` w wolnych śieciach),  i multipleksuje kanały do tego samego serwera używając lokalnych plików kontrolnych:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Kilka innych opcji dotyczących ssh są mogą mieć wpływ na bezpieczeństwo i powinny być włączane z pełną świadomością, np. tylko dla podsieci, jednego serwera, albo tylko dla zaufanych sieci:  `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Rozważ użycie [`mosh`](https://mosh.mit.edu/) który jest alternatywą dla ssh używającą UDP, unijącą zgubionych połączeń i dodającą kilka ułatwień (wymaga konfiguracji po stronie serwera).

- Aby wyświetlić prawa do pliku w formie ósemkowej, która jest użyteczna w konfiguracji systemu ale nie jest dostępna w `ls`, użyj:
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Dla interaktywnego wyboru wartości z informacji zwracanych przez inną komendę użyj [`percol`](https://github.com/mooz/percol) albo [`fzf`](https://github.com/junegunn/fzf).

- Aby oddziaływać na pliki na podstawie informacji zwracanych przez inną komendę (np jak `git`), użyj `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Aby uruchomić prosty serwer www ze wszystkimi plikami w aktualnym katalogu i dostępem do wszystkich podkatalogów, dostępny dla wszystkich w twojej sieci, użyj:
`python -m SimpleHTTPServer 7777` (Python2.X. Serwer będzie nasłuchiwał na porcie 7777) lub `python -m http.server 7777` (Python3.X. Serwer będzie nasłuchiwał na porcie 7777).

- Aby uruchomić komendę z przywilejami użyj `sudo` (dla przywilejów root) lub `sudo -u` (dla innego użytkownika`. Użyj `su` lub `sudo bash` aby uruchomić powłokę jak ten użytkownik. Użyj `su -` aby zasymulować świeże logowanie się jako root lub jako inny użytkownik.


## Przetwarzanie plików i danych

- To locate a file by name in the current directory, `find . -iname '*something*'` (or similar). To find a file anywhere by name, use `locate something` (but bear in mind `updatedb` may not have indexed recently created files).

- For general searching through source or data files (more advanced than `grep -r`), use [`ag`](https://github.com/ggreer/the_silver_searcher).

- To convert HTML to text: `lynx -dump -stdin`

- For Markdown, HTML, and all kinds of document conversion, try [`pandoc`](http://pandoc.org/).

- If you must handle XML, `xmlstarlet` is old but good.

- For JSON, use [`jq`](http://stedolan.github.io/jq/).

- For YAML, use [`shyaml`](https://github.com/0k/shyaml).

- For Excel or CSV files, [csvkit](https://github.com/onyxfish/csvkit) provides `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- For Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) is convenient and [`s4cmd`](https://github.com/bloomreach/s4cmd) is faster. Amazon's [`aws`](https://github.com/aws/aws-cli) and the improved [`saws`](https://github.com/donnemartin/saws) are essential for other AWS-related tasks.

- Know about `sort` and `uniq`, including uniq's `-u` and `-d` options -- see one-liners below. See also `comm`.

- Know about `cut`, `paste`, and `join` to manipulate text files. Many people use `cut` but forget about `join`.

- Know about `wc` to count newlines (`-l`), characters (`-m`), words (`-w`) and bytes (`-c`).

- Know about `tee` to copy from stdin to a file and also to stdout, as in `ls -al | tee file.txt`.

- Know that locale affects a lot of command line tools in subtle ways, including sorting order (collation) and performance. Most Linux installations will set `LANG` or other locale variables to a local setting like US English. But be aware sorting will change if you change locale. And know i18n routines can make sort or other commands run *many times* slower. In some situations (such as the set operations or uniqueness operations below) you can safely ignore slow i18n routines entirely and use traditional byte-based sort order, using `export LC_ALL=C`.

- Know basic `awk` and `sed` for simple data munging. For example, summing all numbers in the third column of a text file: `awk '{ x += $3 } END { print x }'`. This is probably 3X faster and 3X shorter than equivalent Python.

- To replace all occurrences of a string in place, in one or more files:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- To rename multiple files and/or search and replace within files, try [`repren`](https://github.com/jlevy/repren). (In some cases the `rename` command also allows multiple renames, but be careful as its functionality is not the same on all Linux distributions.)
```sh
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
      # Recover backup files whatever.bak -> whatever:
      repren --renames --from '(.*)\.bak' --to '\1' *.bak
      # Same as above, using rename, if available:
      rename 's/\.bak$//' *.bak
```

- As the man page says, `rsync` really is a fast and extraordinarily versatile file copying tool. It's known for synchronizing between machines but is equally useful locally. It also is among the [fastest ways](https://web.archive.org/web/20130929001850/http://linuxnote.net/jianingy/en/linux/a-fast-way-to-remove-huge-number-of-files.html) to delete large numbers of files:
```sh
mkdir empty && rsync -r --delete empty/ some-dir && rmdir some-dir
```

- Use `shuf` to shuffle or select random lines from a file.

- Know `sort`'s options. For numbers, use `-n`, or `-h` for handling human-readable numbers (e.g. from `du -h`). Know how keys work (`-t` and `-k`). In particular, watch out that you need to write `-k1,1` to sort by only the first field; `-k1` means sort according to the whole line. Stable sort (`sort -s`) can be useful. For example, to sort first by field 2, then secondarily by field 1, you can use `sort -k1,1 | sort -s -k2,2`.

- If you ever need to write a tab literal in a command line in Bash (e.g. for the -t argument to sort), press **ctrl-v** **[Tab]** or write `$'\t'` (the latter is better as you can copy/paste it).

- The standard tools for patching source code are `diff` and `patch`. See also `diffstat` for summary statistics of a diff and `sdiff` for a side-by-side diff. Note `diff -r` works for entire directories. Use `diff -r tree1 tree2 | diffstat` for a summary of changes. Use `vimdiff` to compare and edit files.

- For binary files, use `hd`, `hexdump` or `xxd` for simple hex dumps and `bvi` or `biew` for binary editing.

- Also for binary files, `strings` (plus `grep`, etc.) lets you find bits of text.

- For binary diffs (delta compression), use `xdelta3`.

- To convert text encodings, try `iconv`. Or `uconv` for more advanced use; it supports some advanced Unicode things. For example, this command lowercases and removes all accents (by expanding and dropping them):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- To split files into pieces, see `split` (to split by size) and `csplit` (to split by a pattern).

- To manipulate date and time expressions, use `dateadd`, `datediff`, `strptime` etc. from [`dateutils`](http://www.fresse.org/dateutils/).

- Use `zless`, `zmore`, `zcat`, and `zgrep` to operate on compressed files.


## Debugowanie systemu

- For web debugging, `curl` and `curl -I` are handy, or their `wget` equivalents, or the more modern [`httpie`](https://github.com/jkbrzt/httpie).

- To know current cpu/disk status, the classic tools are `top` (or the better `htop`), `iostat`, and `iotop`. Use `iostat -mxz 15` for basic CPU and detailed per-partition disk stats and performance insight.

- For network connection details, use `netstat` and `ss`.

- For a quick overview of what's happening on a system, `dstat` is especially useful. For broadest overview with details, use [`glances`](https://github.com/nicolargo/glances).

- To know memory status, run and understand the output of `free` and `vmstat`. In particular, be aware the "cached" value is memory held by the Linux kernel as file cache, so effectively counts toward the "free" value.

- Java system debugging is a different kettle of fish, but a simple trick on Oracle's and some other JVMs is that you can run `kill -3 <pid>` and a full stack trace and heap summary (including generational garbage collection details, which can be highly informative) will be dumped to stderr/logs. The JDK's `jps`, `jstat`, `jstack`, `jmap` are useful. [SJK tools](https://github.com/aragozin/jvm-tools) are more advanced.

- Use `mtr` as a better traceroute, to identify network issues.

- For looking at why a disk is full, `ncdu` saves time over the usual commands like `du -sh *`.

- To find which socket or process is using bandwidth, try `iftop` or `nethogs`.

- The `ab` tool (comes with Apache) is helpful for quick-and-dirty checking of web server performance. For more complex load testing, try `siege`.

- For more serious network debugging, `wireshark`, `tshark`, or `ngrep`.

- Know about `strace` and `ltrace`. These can be helpful if a program is failing, hanging, or crashing, and you don't know why, or if you want to get a general idea of performance. Note the profiling option (`-c`), and the ability to attach to a running process (`-p`).

- Know about `ldd` to check shared libraries etc.

- Know how to connect to a running process with `gdb` and get its stack traces.

- Use `/proc`. It's amazingly helpful sometimes when debugging live problems. Examples: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (where `xxx` is the process id or pid).

- When debugging why something went wrong in the past, `sar` can be very helpful. It shows historic statistics on CPU, memory, network, etc.

- For deeper systems and performance analyses, look at `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](https://en.wikipedia.org/wiki/Perf_(Linux)), and [`sysdig`](https://github.com/draios/sysdig).

- Check what OS you're on with `uname` or `uname -a` (general Unix/kernel info) or `lsb_release -a` (Linux distro info).

- Use `dmesg` whenever something's acting really funny (it could be hardware or driver issues).


## Jednolinijkowce

A few examples of piecing together commands:

- It is remarkably helpful sometimes that you can do set intersection, union, and difference of text files via `sort`/`uniq`. Suppose `a` and `b` are text files that are already uniqued. This is fast, and works on files of arbitrary size, up to many gigabytes. (Sort is not limited by memory, though you may need to use the `-T` option if `/tmp` is on a small root partition.) See also the note about `LC_ALL` above and `sort`'s `-u` option (left out for clarity below).
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Use `grep . *` to quickly examine the contents of all files in a directory (so each line is paired with the filename), or `head -100 *` (so each file has a heading). This can be useful for directories filled with config settings like those in `/sys`, `/proc`, `/etc`.


- Summing all numbers in the third column of a text file (this is probably 3X faster and 3X less code than equivalent Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- If want to see sizes/dates on a tree of files, this is like a recursive `ls -l` but is easier to read than `ls -lR`:
```sh
      find . -type f -ls
```

- Say you have a text file, like a web server log, and a certain value that appears on some lines, such as an `acct_id` parameter that is present in the URL. If you want a tally of how many requests for each `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- To continuously monitor changes, use `watch`, e.g. check changes to files in a directory with `watch -d -n 2 'ls -rtlh | tail'` or to network settings while troubleshooting your wifi settings with `watch -d -n 2 ifconfig`.

- Run this function to get a random tip from this document (parses Markdown and extracts an item):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Niejasne ale przydatne

- `expr`: perform arithmetic or boolean operations or evaluate regular expressions

- `m4`: simple macro processor

- `yes`: print a string a lot

- `cal`: nice calendar

- `env`: run a command (useful in scripts)

- `printenv`: print out environment variables (useful in debugging and scripts)

- `look`: find English words (or lines in a file) beginning with a string

- `cut`, `paste` and `join`: data manipulation

- `fmt`: format text paragraphs

- `pr`: format text into pages/columns

- `fold`: wrap lines of text

- `column`: format text fields into aligned, fixed-width columns or tables

- `expand` and `unexpand`: convert between tabs and spaces

- `nl`: add line numbers

- `seq`: print numbers

- `bc`: calculator

- `factor`: factor integers

- [`gpg`](https://gnupg.org/): encrypt and sign files

- `toe`: table of terminfo entries

- `nc`: network debugging and data transfer

- `socat`: socket relay and tcp port forwarder (similar to `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): network traffic visualization

- `dd`: moving data between files or devices

- `file`: identify type of a file

- `tree`: display directories and subdirectories as a nesting tree; like `ls` but recursive

- `stat`: file info

- `time`: execute and time a command

- `timeout`: execute a command for specified amount of time and stop the process when the specified amount of time completes.

- `lockfile`: create semaphore file that can only be removed by `rm -f`

- `logrotate`: rotate, compress and mail logs.

- `watch`: run a command repeatedly, showing results and/or highlighting changes

- `tac`: print files in reverse

- `shuf`: random selection of lines from a file

- `comm`: compare sorted files line by line

- `pv`: monitor the progress of data through a pipe

- `hd`, `hexdump`, `xxd`, `biew` and `bvi`: dump or edit binary files

- `strings`: extract text from binary files

- `tr`: character translation or manipulation

- `iconv` or `uconv`: conversion for text encodings

- `split` and `csplit`: splitting files

- `sponge`: read all input before writing it, useful for reading from then writing to the same file, e.g., `grep -v something some-file | sponge some-file`

- `units`: unit conversions and calculations; converts furlongs per fortnight to twips per blink (see also `/usr/share/units/definitions.units`)

- `apg`: generates random passwords

- `7z`: high-ratio file compression

- `ldd`: dynamic library info

- `nm`: symbols from object files

- `ab`: benchmarking web servers

- `strace`: system call debugging

- `mtr`: better traceroute for network debugging

- `cssh`: visual concurrent shell

- `rsync`: sync files and folders over SSH or in local file system

- `wireshark` and `tshark`: packet capture and network debugging

- `ngrep`: grep for the network layer

- `host` and `dig`: DNS lookups

- `lsof`: process file descriptor and socket info

- `dstat`: useful system stats

- [`glances`](https://github.com/nicolargo/glances): high level, multi-subsystem overview

- `iostat`: Disk usage stats

- `mpstat`: CPU usage stats

- `vmstat`: Memory usage stats

- `htop`: improved version of top

- `last`: login history

- `w`: who's logged on

- `id`: user/group identity info

- `sar`: historic system stats

- `iftop` or `nethogs`: network utilization by socket or process

- `ss`: socket statistics

- `dmesg`: boot and system error messages

- `sysctl`: view and configure Linux kernel parameters at run time

- `hdparm`: SATA/ATA disk manipulation/performance

- `lsb_release`: Linux distribution info

- `lsblk`: list block devices: a tree view of your disks and disk paritions

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: hardware information, including CPU, BIOS, RAID, graphics, devices, etc.

- `lsmod` and `modinfo`: List and show details of kernel modules.

- `fortune`, `ddate`, and `sl`: um, well, it depends on whether you consider steam locomotives and Zippy quotations "useful"


## OS X only

These are items relevant *only* on MacOS.

- Package management with `brew` (Homebrew) and/or `port` (MacPorts). These can be used to install on MacOS many of the above commands.

- Copy output of any command to a desktop app with `pbcopy` and paste input from one with `pbpaste`.

- To enable the Option key in Mac OS Terminal as an alt key (such as used in the commands above like **alt-b**, **alt-f**, etc.), open Preferences -> Profiles -> Keyboard and select "Use Option as Meta key".

- To open a file with a desktop app, use `open` or `open -a /Applications/Whatever.app`.

- Spotlight: Search files with `mdfind` and list metadata (such as photo EXIF info) with `mdls`.

- Be aware MacOS is based on BSD Unix, and many commands (for example `ps`, `ls`, `tail`, `awk`, `sed`) have many subtle variations from Linux, which is largely influenced by System V-style Unix and GNU tools. You can often tell the difference by noting a man page has the heading "BSD General Commands Manual." In some cases GNU versions can be installed, too (such as `gawk` and `gsed` for GNU awk and sed). If writing cross-platform Bash scripts, avoid such commands (for example, consider Python or `perl`) or test carefully.

- To get MacOS release information, use `sw_vers`.


## More resources

- [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.
- [awesome-osx-command-line](https://github.com/herrbischoff/awesome-osx-command-line): A more in-depth guide for the Mac OS command line.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) for writing better shell scripts.
- [shellcheck](https://github.com/koalaman/shellcheck): A shell script static analysis tool. Essentially, lint for bash/sh/zsh.
- [Filenames and Pathnames in Shell](http://www.dwheeler.com/essays/filenames-in-shell.html): The sadly complex minutiae on how to handle filenames correctly in shell scripts.


## Disclaimer

With the exception of very small tasks, code is written so others can read it. With power comes responsibility. The fact you *can* do something in Bash doesn't necessarily mean you should! ;)


## License

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
