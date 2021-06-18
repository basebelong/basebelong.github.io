# Upptäckter i Fedora

## En helt ny värld

Som en del i min strävan efter att certifiera mig som systemadministratör för RHEL 8 har jag installerat Fedora 34 på min laptop. Det är **länge** sedan jag körde något Red Hat system. Första jag installerade var Red Hat Linux 5.2 någon gång kring 1998. Minns att jag använde åtminstone version 6 och några av de tidiga Fedora releaserna.

För någon som i modern tid mestadels kört Ubuntu är Fedora något av en udda fågel. Säkert helt självklar för den som är van, men mycket nytt för åtminstone mig att upptäcka.

Fedora har på senare tid hoppat väldigt mycket mellan vilket filsystem som skall vara default. Nu senast är det btrfs. Innan det var det xfs. Lustigt nog har Red Hat deprikerat btrfs för RHEL 8. Fedoras val av filsystem tycks vara någon form av inre strid bland rödhattarna.

## swap på zram

När jag undersökte möjligheterna till hybernation i Fedora 34 på min Lenovo Yoga laptop upptäckte jag att swap körs i zram. Lite googlande ledde mig till Fedoras [wiki](https://fedoraproject.org/wiki/Changes/SwapOnZRAM). Där diskuteras ämnet utförligt.

Min laptop har **bara** 16GB RAM så det är besvärligt att bygga upp lab-miljöer med flertalet virtuella maskiner utan att minnestrycket blir för högt och Fedoras oomd börjar döda processer hej vilt. Som den fullständiga galning jag är tänker jag att det kan man komma undan genom swap på zram och ett mycket högt swappiness värde. Ett bra sätt att testa hur stabilt någonting är - är att testa extremfall.

swap på zram är konfigurerat genom systemd. Default inställningarna finns under /usr/lib/systemd/zram-generator.conf och behöver flyttas till /etc/systemd för att konfigureras där. Filen har en manualsida som finns att läsa under man(5) zram-generator.conf.

Mitt första naiva test var att lägga till
	max-zram-size = 32768
	swap-priority = 10000
för att verkligen kunna testa extremfallet. Minns att jag bara har 16GB fysiskt minne. Du har jag altså en dubbelt så stor swap i nämnda minne. zram är komprimerat, men kräver ju att kompressionen har ett förhållande bättre än 2:1 för att swap inte skall äta upp allt minne!

Det gick faktiskt att krascha systemet, eller åtminstone göra det obrukbart - genom att starta ett gäng överprovitionerade virtuella maskiner. 

En mer rimlig (men smått förbluffande) inställning är på mitt system att avsätta lika mycket till swap på zram som det finns fysiskt minne. Jag har ännu inte efter att ha använt min dator normalt under en tid stött på allvarliga problem.

Använder följande inställningar på min 16GB maskin:
	[zram0]
	zram-fraction = 1.0
	max-zram-size = 16384
	swap-priority = 200

zramctl visar användningssiffror. Under experimenterandet var det lämpligt att lämna ett terminalfönster igång med 'sudo watch -n 3 zramctl'

[Back](../../../index.html)
