# Länkar till plug-ins

## IEM plugin suite

<https://plugins.iem.at/>

Gratis och open source, finns till både MacOS, Windows och Linux. Har
stöd för upp till 7:e ordningens ambisonics.

## Ambisonics Toolkit

<https://www.ambisonictoolkit.net/>

Gratis och open source, med stöd för REAPER (MacOS, Windows och Linux)
och SuperCollider (MacOS, Windows och Linux). Versionen för REAPER har
stöd för 1:a ordningens ambisonics, men versionen för SuperCollider har
stöd för högre ordningens ambisonics.

## Soundfield by RØDE

<https://rode.com/en/software/soundfield-by-rode>

Gratis plug-in, utvecklad av RØDE som tillverkar mikrofonen Soundfield.
Används för att konvertera signalen från en Soundfield-mikrofon
(A-format) till flertalet olika format såsom B-format, stereo, 7.1, etc.

# Andra typer av panorering

## Stereo

Sedan mitten på 1900-talet har flertalet system för panorering
utvecklats. Det lättaste av dessa är stereo, vilket ni alla är bekanta
med via pan-kontrollen på en mixer eller i en DAW. När vi vill att
ljudet ska upplevas att komma från vänster vrider vi pan-kontrollen så
att mer av ljudet kommer från vänster högtalare/hörlur, och vice versa
om vi vill att ljudet ska upplevas att komma från höger.

## Surround: Quad, 5.1 med mera

Vill vi utöka detta system till fyra högtalare, d.v.s *Quad*, gör vi på
samma sätt -- vill vi att ljudet ska upplevas komma bakom oss skickar vi
helt enkelt mer signal till de bakre högtalarna än de främre.

Det är på detta sätt de vanliga formaten för bio fungerar. Dessa brukar
finnas i de flesta DAW. Du har kanske sett 5.1, 7.1, 13.1 osv.

## Problem med denna metod

Om vi t.ex har en Pro Tools-session där vi använder 7.1, och sedan
renderar (även kallat \"bounce\") mixen kommer vi att få antingen
`.wav`{.verbatim}-fil med 8 kanaler (7 högtalare + 1 sub) eller 8
individuella `.wav`{.verbatim}-filer. Vi kan då spela upp mixen i ett
ljudsystem som har stöd för 7.1. Vi kan däremot inte enkelt spela upp
mixen i ett system som har t.ex fyra högtalare, eller ett system såsom
Klangkupolen på KMH som har 29 högtalare. Mixen kommer att vara låst
till 7.1, och ifall vi vill översätta den till andra format måste vi
antingen gå in i vår Pro Tools-session igen och ändra panoreringen
alternativt panorera varje kanal i 7.1-mixen manuellt i det nya
ljudsystemets format.

Detta gör denna typ av format, där vi panorerar enligt en viss
högtalaruppställning, oflexibla.

# Ambisonics {#ambisonics-1}

Ambisonics är ett system för 3D-panorering och inspelning som började
utvecklas under sent 1970-tal. Ambisonics är alltså inte ett företag som
utvecklar en viss plug-in, utan ett system som har implementerats i
flertalet plug-ins av flertalet företag.

Det som skiljer ambisonics från flera andra system är att vi separerar
panoreringen från den givna högtalaruppställningen. I ambsisonics
föreställer vi oss en sfär (s.k *soundfield*) som omger lyssnaren, och
placerar ljud på punkter av sfärens yta. Detta betyder att vi i
ambisonics anger från vilken punkt vi vill att ljudet ska upplevas låta
från, oberoende av högtalaruppställningen som kommer att spela upp
ljuden.

Ambisonics uppnår detta med att ha ett intermediärt format som består av
ett antal ljudkanaler vars fas- och amplitudförhållande innehåller
information om från vilken punkt på den imaginära sfären ljuden ska
komma ifrån. Detta intermediära format kallas för *B-format*.[^1]

För att nå detta intermeidära format måste vi använda en s.k *ambisonics
encoder*. Dessa kallas i vissa plug-ins för *ambisonics panner*, och
betyder alltså att vi tar en ljudkälla och placerar den i ett virtuellt
rum. Ljudkällan kan vara mono, stereo eller egentligen vad som helst --
de olika kanalerna i ljudkällan får varsin position på den imaginära
sfären.

När vi sedan har panorerat våra ljud -- enkodat dem i B-format -- kan vi
dekoda ljuden till en given högtalaruppställning. Denna
högtalaruppställning kan vara i stort sett vilken som helst. Detta
innebär att vi kan rendera vår mix i B-format, och sedan dekoda ljudet
till den högtalaruppställning i vilken vi vill spela upp mixen.

## Ambisonic order

Det som är viktigt att förstå är att signalen i B-format har flertalet
kanaler. Dessa kanaler överenstämmer *inte* med antalet ljudkällor, och
*inte* med antalet högtalare. Antalet kanaler i B-format-signalen har
istället att vilken s.k *ordning* av ambisonics man arbetar i -- på
engelska *ambisonic order*. Detta kan ses som vilken upplösning vi
arbetar i -- ju högre ordning, desto högre upplösning, och ju fler
kanaler i B-format-signalen. Enkelt förklarat för vi plats med mer
spatiell information ju fler kanaler B-format-signalen har.

Den mest lågupplösta formen av ambisonics är 1:a ordningens ambisonics.
Då har B-format-signalen 4 ljudkanaler.

[^1]: *B-format* kan också användas för att hänvisa till kanalordningen
    *FuMa*, vilket äldre plug-ins använder. Vissa kallar det äldre
    formatet för B-format och det nyare för ambix. I detta kompendium
    använder jag B-format för att referera till det intermediära
    formatet i ambisonics, oavsett om det är äldre eller nyare plug-ins.
