## algol-display

Dette repositoriet viser hvordan man setter opp en raspberry pi til å automatisk åpne programmer etter boot.

### LXDE

Raspberry Pi bruker [LXDE](https://wiki.archlinux.org/title/LXDE) som desktop environment. Etter LXDE har startet opp leser den ```/home/pi/.config/lxsession/LXDE-pi/autostart```, en fil hvor man kan putte kommandoer man vil at skal kjøres etter startup. Denne filen finnes ikke på en fresh Raspberry installasjon. Bare lag directoriesene og filen. [autostart](https://wiki.archlinux.org/title/LXDE#Autostart) har et veldig enkelt format: Hver linje er en @ etterfulgt av kommandoen man vil at skal kjøres.

### Ruter Mon

Ruter har lagd en applikasjon som enkelt lager avgangstavler. Gå inn på [Ruter Mon](https://mon.ruter.no/) og sett opp en tavle. Alle instillinger blir en del av url-en.

Med disse to har man det man trenger for å lage åpne en avgangstavle on boot; bare putt det her i ```autostart```:

```
@chromium-browser --start-maximized --start-fullscreen <URL>
```

Dette kan man gjøre ved å kjøre ```./sync.sh```, som vil kopiere ```autostart```-filen i dette repoet til riktig plassering.

[Forskningsparken T-bane Horisontal](https://mon.ruter.no/departures/59.943756-10.721023/N4Igrgzgpgwg9gGzAWwHYBkCGBPOYAuIAXPgE5hQA0IARnJqQCYTEDaoE+cADgAoKYAxlACSzNiAByAZQBKRaVz4DhRAGwBGNQGY1IajPmKe-IVCIBWAJxqADLZABdaoygDsURoob4AKgEtkKGJbagALf0ZXDH9UKBYiUEMFJVNVazsHIlYpOSIARTAcIg0tCwAWAFoqgDV4-AR-fVz5QuLStQrKi0rZWIBzKFQAAgA3f0xh41I4ZuS27BKyqp7pOH7UCFHMVFQ5vIWlzpXK6dmDA6LFjq6emAYEYYAhKFI40ghh7gEIFkcAX2oqBQNFeAHkAGYAESg3B8YFI8WIAA5qPh-A1gkQQKZ8PgIXBSMhhhpmox-BBMDQEJ5fKQdhBuIT8ABZOCuBI5GiQJzUIZUmmMYhkCjhSJQOlCADW8CQaGF5CggI4qRUonE2RaKRMassNns+yMqrM6i0ul5IFc7k83lIfkCWNCIAiUSG6FiSMSWuMyhNGQNmvmVyOFh6VRepH6UtI2E4mAQNJG40mLMwACtCZwKHsLq1gzcw70PEmJsNUxmPvhs4aCvmyoXy5mq0Ma4cC91KnVOI0xqXG5Xq7na+16x2+qhBiWU+mm4OtW3Rz1ZMXW3XOj0ev2sy2hwv1x3puiJ1BCACgSDwdDYfDEQlUSB0ZjiDiBHiCUThgAmMkUgW0+mbEydpshyEjcn8fKoH+QokIqYquJKggyogKB7LBFD-M4ICjK8ED+HAaGfv8QA)

[Forskningsparken T-bane Vertikal](https://mon.ruter.no/departures/59.943756-10.721023/N4Igrgzgpgwg9gGzAWwHYBkCGBPOYAuIAXAGaYLQA0IARnJgE4AmExA2qBPnAA4AKCTAGMoASRbsQAOQDKAJSIzu-QSKIA2AIzqAzOpDVZCpbwHCoRAKwBOdQAY7IALrUmUQdihMljfABUAS2QoYjtqAAsApjcMANQoViJQI0VlMzUbe0ciNml5IgBFMBwiTW1LABYAWmqANQT8BACDPIUikrL1SqrLKrk4gHMoVAACADcAzBGTBjgWlPbsUvLq3pk4AdQIMcxUVHn8xeWu1aqZucND4qXO7t6YRgQRgCEoBniGCBGeQQhWJwAvtRUCgaG8APIkAAiUB4vjADASxAAHNR8AFGiEiCAzPh8CQ4AxkCNNC0mAEIJgaAgvH4GLsIDxCfgALJwNyJXI0SDOajDKk0pjEfAMMBQCJRKB04QAa3gSDQwtFUCBnDSqjEEhyrVSpg1VlsDgOxnV5g02j0vJAbg8Xh8DH8QSxYRAkWiw3QcSRSR1JhUZsyRu1C2ux0svWqrwYAxlDGwXHINNGEymLMwACtCVwxftLm1Q7cI31PMnJiM05nPvgc8bCgXykWK1nq8Na0dCz0qvUuE1xmWm1Wa3m6x0G53+qghqXUxnm0Ode2x705CW2-Wur1egPs63h4uN52ZujJ1BCIDgaCIdDYfDEYlUSB0ZjiDjBHiCUSRgAmMkUgW0+ktiZB02Q5SRuX+PlUH-IUiBFMUJTcaUhDlRAUH2ODlQBFwQDGN4IACOAMK-AEgA)
### xdotool

Raspbian bruker [Xorg](https://wiki.archlinux.org/title/xorg) som display server. [xdotool](https://manpages.ubuntu.com/manpages/trusty/man1/xdotool.1.html) kan brukes til å sende input events til Xorg. Da kan man f.eks flytte musa ned i hjørnet eller sende tastetrykk.

```
xdotool mousemove 100000 100000
```

Dette flytter musa ned i høyre hjørne. Dette kan man også putte i ```autostart```.

### Flere vinduer

Å åpne flere vinduer med forskjellige ting i en spesiell layout er mer vanskelig. En mulighet er å bytte fra LXDE til i3 og bruke [layout saving](https://i3wm.org/docs/layout-saving.html). Hvis man vil beholde LXDE kan man kanskje bruke [devilspie2](https://www.nongnu.org/devilspie2/).
