---
title: "Wie ich diskrete Entscheidungen treffe, die nicht wichtig sind"
date: 2023-07-27T14:43:05+02:00
tags: [Mathematik, fun]
---

Wenn die Entscheidung binär ist (wie Links oder Rechts), genügt ein einfacher Münzwurf. Anderenfalls müsste man einen Zufallszahlengenerator benutzen. Normalerweise treffe ich solche unwichtigen Entscheidungen schnell, indem ich die Uhr meines Telefons und [modulare Arithmetik](https://en.wikipedia.org/wiki/Modular_arithmetic) (mein Lieblingsoperator) verwende. Die Idee ist, die Minute ($m$) auf der Uhr deines Telefons als Eingabe für $f(m, n) = m \mod n$ zu nehmen, wobei $n$ die Anzahl der eindeutigen Auswahlmöglichkeiten ist, die du hast.

Nehmen wir an, du bist in Deutschland und bekommst 5 verschiedene Kuchenstücke geschenkt (sehr Deutsch :)), die alle gleich gut aussehen, aber du willst nur eins. Du schaust auf dein Handy und siehst, dass es `15:39` Uhr ist. Daher:

$$39 \mod 5 \equiv 4$$

Also nimmst du den Kuchen ganz rechts, denn wir nummerieren die Kuchenstücke von links nach rechts $0, 1, 2, 3, 4$.

Für einfache Entscheidungen hat man meistens weniger als 60 Optionen, so dass die Minute ausreichen sollte; Sekunden werden nicht verwendet, weil sie sich zu schnell ändern.