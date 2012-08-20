# ps-sl

PowerShell script f�r att interagera med AB Storstockholms Lokaltrafik WebServices - [API Realtid][api-realtid-link].

Dessa funktioner l�ter dig s�ka realtidsinformation om avg�ngar fr�n h�llplatser i hela Stockholmsomr�det via SLs realtids API. Mer information om API:et finns h�r

http://www.trafiklab.se/api/sl-realtidsinfo

F�r att kunna anv�nda dessa API:er m�ste du ange en API-nyckel, du kan l�sa mer om hur d� skaffar en s�dan p� [Trafiklab.se][trafiklab-link].


http://www.trafiklab.se/kom-igang

[api-realtid-link]: http://www.trafiklab.se/api/sl-realtidsinfo
[trafiklab-link]: http://www.trafiklab.se/kom-igang 

# F�ruts�ttningar

F�r att anv�nda dessa script m�ste man ha [PowerShell 3.0][powershell-wiki] eller senare installerad. PowerShell 3.0 �r standard i Windows 8 men g�r utm�rkt att [ladda ner][powershell3-link] till tidigare versioner av Windows.

[powershell-wiki]: http://en.wikipedia.org/wiki/Windows_PowerShell
[powershell3-link]: http://www.microsoft.com/en-us/download/details.aspx?id=29939

# Hur g�r man?

Om du vill testa detta, ladda ner filerna och skaffa en API nyckel. SMidigast �r att sedan spara denna API nyckel i din PowerShell profil. Fr�n enkommandorad, skriv:

	PS C:\> notepad $PROFILE

Sedan kan du l�gga till f�ljande rad i profilen:

  $apiKey = 'xyz123xyz123xyz123xyz123xyz123zy'

G�r man det �r denna nyckel alltid tillg�nlig men beh�ver inte sparas i scriptfilen. Gl�m inte att ladda om profilen n�r du gjort detta! 

	PS C:\> . $PROFILE


Nu kan du pr�va att s�ka efter id f�r en h�llplats;

	PS C:\> Get-SLRealtidSite -query Slussen -apiKey $apiKey


	Number                                                      Name
	------                                                      ----
	9192                                                        Slussen (Stockholm)
	

F�r att se aktuella avg�ngar fr�n Slussen, anropa DspDepartures metoden:


	PS C:\> Get-SLRealtidDpsDepartures -siteId 9192 -apiKey $apiKey

	xsi           : http://www.w3.org/2001/XMLSchema-instance
	xsd           : http://www.w3.org/2001/XMLSchema
	xmlns         : http://www1.sl.se/realtidws/
	LatestUpdate  : 2012-08-20T09:07:07.5045861+02:00
	ExecutionTime : 00:00:00.3749928
	Buses         : Buses
	Metros        :
	Trains        :
	Trams         : Trams


Ett XML dokument som visar att det finns bussavg�ngar (Buses) och lokalt�g (Trams) Vill du direkt se filka bussar som snart �ker fr�n Slussen, skriv:

	PS C:\> (Get-SLRealtidDpsDepartures -siteId 9192 -apiKey $apiKey).Buses.DpsBus


	SiteId             : 9192
	StopAreaNumber     : 10149
	TransportMode      : BLUEBUS
	StopAreaName       : Slussen
	LineNumber         : 2
	Destination        : Sofia
	TimeTabledDateTime : 2012-08-20T09:08:00
	ExpectedDateTime   : 2012-08-20T09:08:49
	DisplayTime        : 0 min

	SiteId             : 9192
	StopAreaNumber     : 10149
	TransportMode      : BUS
	StopAreaName       : Slussen
	LineNumber         : 76
	Destination        : Frihamnen
	TimeTabledDateTime : 2012-08-20T09:09:00
	ExpectedDateTime   : 2012-08-20T09:09:00
	DisplayTime        : 0 min

	SiteId             : 9192
	StopAreaNumber     : 10149
	TransportMode      : BUS
	StopAreaName       : Slussen
	LineNumber         : 53
	Destination        : Roslagstull
	TimeTabledDateTime : 2012-08-20T09:06:00
	ExpectedDateTime   : 2012-08-20T09:09:12
	DisplayTime        : 0 min

	..
	..
	..



# Kontakt 

Om du har fr�gor om detta script, skapa helst ett [issue][issue-link] i det h�r projektet.

[issue-link]: https://github.com/yooakim/ps-sl/issues


# Historik

	Datum		Version		Kommentar
	==========	=======		============================================================
	2012-08-20	0.1		Skapade koden




