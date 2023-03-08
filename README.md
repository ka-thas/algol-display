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

### xdotool

Raspbian bruker [Xorg](https://wiki.archlinux.org/title/xorg) som display server. [xdotool](https://manpages.ubuntu.com/manpages/trusty/man1/xdotool.1.html) kan brukes til å sende input events til Xorg. Da kan man f.eks flytte musa ned i hjørnet eller sende tastetrykk.

```
xdotool mousemove 100000 100000
```

Dette flytter musa ned i høyre hjørne. Dette kan man også putte i ```autostart```.

### Flere vinduer

Å åpne flere vinduer med forskjellige ting i en spesiell layout er mer vanskelig. En mulighet er å bytte fra LXDE til i3 og bruke [layout saving](https://i3wm.org/docs/layout-saving.html). Hvis man vil beholde LXDE kan man kanskje bruke [devilspie2](https://www.nongnu.org/devilspie2/).
