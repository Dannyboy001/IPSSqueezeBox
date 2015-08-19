# IPSSqueezeBox
Erm�glich die Steuerung und Darstellung der Zust�nde
von SqueezeBox Ger�ten in IPS, in Verbindung mit dem
Logitech Media Server.

## Doku:

### Funktionsreferenz LMSSplitter / Logitech Media Server:
F�r alle Befehle gilt: Tritt ein Fehler auf, wird eine Exception geworfen.

#### Datenbank:

`array LMS_GetLibaryInfo (integer $InstanzID)`
Liefert Informationen �ber die Datenbank des LMS.  

| Index   | Typ     | Beschreibung                |
| :-----: | :-----: | :-------------------------: |
| Genres  | integer | Anzahl verschiedener Genres |
| Artists | integer | Anzahl der Interpreten      |
| Albums  | integer | Anzahl der Alben            |
| Songs   | integer | Anzahl aller Titel          |


*mehr fehlt noch...*

### Funktionsreferenz LSQDevice / SqueezeboxDevice:
F�r alle Befehle gilt: Tritt ein Fehler auf, wird eine Exception geworfen.

#### Steuerung:
Alle Befehle liefern einen `boolean` als R�ckgabewert.
`true` wenn der Befehl vom Server best�tigt wurde.
Wird der Befehl nicht best�tigt, so ist die ein Fehler (Exception wird erzeugt).

`boolean LSQ_Power (integer $InstanzID, boolean $Value)`  
Schaltet das Ger�t ein `true` oder aus `false`.  
`boolean LSQ_SelectPreset(integer $InstanzID, integer $Value)`  
Simuliert einen Tastendruck der Preset-Tasten 1-6 `$Value`.  
`boolean LSQ_Play (integer $InstanzID)`  
Startet die Wiedergabe.  
`boolean LSQ_Pause (integer $InstanzID)`  
Pausiert die Wiedergabe.  
`boolean LSQ_Stop (integer $InstanzID)`  
Stoppt die Wiedergabe.  

#### Playlist:

`string LSQ_LoadPlaylist (integer $InstanzID, string $Name)`  
L�dt die unter `$Name`�bergebene Playlist.  
`array LSQ_GetSongInfoOfCurrentPlaylist (integer $InstanzID)`  
Liefert Informationen �ber den aktuellen Song.  
`array LSQ_GetSongInfoByTrackIndex (integer $InstanzID, integer $Index)`  
Liefert Informationen �ber den Song mit dem `$Index` der aktuellen Playlist.  
Wird als `$Index` 0 �bergeben, so wird der aktuelle Song genutzt.  

| Index     | Typ     | Beschreibung                       |
| :-------: | :-----: | :--------------------------------: |
| Duration  | integer | L�nge in Sekunden                  |
| Id        | integer | UID der Datei in der LMS-Datenbank |
| Title     | string  | Titel                              |
| Genre     | string  | Genre                              |
| Album     | string  | Album                              |
| Artist    | string  | Interpret                          |
| Disc      | integer | Aktuelles Medium                   |
| Disccount | integer | Anzahl aller Medien dieses Albums  |
| Bitrate   | string  | Bitrate in Klartext                |

Alle anderen Befehle liefern einen `boolean` als R�ckgabewert.  
`true` wenn der Befehl vom Server best�tigt wurde.  
Wird der Befehl nicht best�tigt, so ist die ein Fehler (Exception wird erzeugt).  

`boolean LSQ_SavePlaylist (integer $InstanzID, string $Name)`  
Speichert eine Playlist unter den mit `$Name` �bergebenen Namen.  
`boolean LSQ_PlayTrack (integer $InstanzID, integer $Index)`  
Springt in der Playlist auf den mit `$Index` �bergebe Position.  
`boolean LSQ_NextTrack (integer $InstanzID)`  
Springt in der Playlist auf den n�chsten Track.  
`boolean LSQ_PreviousTrack (integer $InstanzID)`  
Springt in der Playlist auf den vorherigen Track.  
`boolean LSQ_NextButton (integer $InstanzID)`  
Simuliert einen Tastendruck auf den Vorw�rts-Button des Ger�tes.  
`boolean LSQ_PreviousButton (integer $InstanzID)`  
Simuliert einen Tastendruck auf den R�ckwerts-Button des Ger�tes.  

#### Setzen von Eigenschaften:

Alle LSQ_Set* - Befehle liefern einen `boolean` als R�ckgabewert.
`true` wenn der gleiche Wert vom Server best�tigt wurde.
`false` wenn der best�tigte Wert abweicht.
Wird der Befehl nicht best�tigt, so ist die ein Fehler (Exception wird erzeugt).

`boolean LSQ_SetBass (integer $InstanzID, integer $Value)`  
Setzt den Bass auf `$Value`. (Nur SliMP3 & SqueezeBox1 / SB1 )  
`boolean LSQ_SetMute (integer $InstanzID, boolean $Value)`  
Stummschaltung aktiv `true`oder deaktiv `false`.  
`boolean LSQ_SetName (integer $InstanzID, string $Name)`  
Setzt den Namen des Ger�tes auf `$Name`.  
`boolean LSQ_SetPitch (integer $InstanzID, integer $Value)`  
Setzt den Tonh�he auf `$Value`. (Nur SqueezeBox1 / SB1 )  
`boolean LSQ_SetPosition (integer $InstanzID, integer $Value)`  
Springt im aktuellen Track auf die Zeit in Sekunden von `$Value`.  
`boolean LSQ_SetRepeat (integer $InstanzID, integer $Value)`  
Setzt dem Modus f�r Wiederholungen. `$Value` kann die Werte 0 f�r aus,  
1 f�r den aktuellen Titel, oder 2 f�r das aktuelle Album/Playlist enthalten.  
`boolean LSQ_SetShuffle (integer $InstanzID, integer $Value)`  
Setzt dem Modus f�r die zuf�llige Wiedergabe. `$Value` kann die Werte 0 f�r aus,  
1 f�r den aktuellen ?Titel?, oder 2 f�r das aktuelle Album/Playlist enthalten.  
`boolean LSQ_SetTreble (integer $InstanzID, integer $Value)`  
Setzt die H�hen auf `$Value`. (Nur SliMP3 & SqueezeBox1 / SB1 )  
`boolean LSQ_SetVolume (integer $InstanzID, integer $Value)`  
Setzt die Lautst�rke auf `$Value`.  
`boolean LSQ_SetSleep(integer $InstanzID, integer $Seconds)`  
Aktiviert den (Ein)Schlafmodus mit der unter `$Seconds`angegeben Sekunden.  
0 deaktiviert den zuvor gesetzten Schlafmodus.  

#### Lesen von Eigenschaften:

Alle LSQ_Get* - Befehle liefern einen jeweils beschriebenen R�ckgabewert.  
Antwortet das Ger�t nicht auf die Anfrage, so ist die ein Fehler und eine Exception wird erzeugt.  

`integer LSQ_GetBass (integer $InstanzID)`  
Liefert den aktuellen Wert vom Bass. (Nur SliMP3 & SqueezeBox1 / SB1 )  
`boolean LSQ_GetMute (integer $InstanzID)`  
Liefert `true` wenn Stummschaltung aktiv ist. Sonst `false`.  
`string LSQ_GetName (integer $InstanzID)`  
Liefert den aktuellen Names des Ger�tes.  
`integer LSQ_GetPitch (integer $InstanzID)`  
Liefert den aktuellen Wert der eingestellten Tonh�he. (Nur SqueezeBox1 / SB1 )  
`integer LSQ_GetPosition (integer $InstanzID)`  
Liefert die Zeit in Sekunden welche vom aktuellen Track schon gespielt wurde.  
`integer LSQ_GetRepeat (integer $InstanzID)`  
Liefert den aktuellen Modus f�r Wiederholungen. Es werden die Werte 0 f�r aus,  
1 f�r den aktuellen Titel, oder 2 f�r das aktuelle Album/Playlist gemeldet.  
`integer LSQ_GetShuffle (integer $InstanzID)`  
Liefert den aktuellen Modus f�r sie zuf�llige Wiedergabe. Es werden die Werte 0 f�r aus,  
1 f�r den aktuellen ?Titel?, oder 2 f�r das aktuelle Album/Playlist gemeldet.  
`integer LSQ_GetTreble (integer $InstanzID)`  
Liefert den aktuellen Wert der eingestellten Tonh�he. (Nur SliMP3 & SqueezeBox1 / SB1 )  
`integer LSQ_GetVolume (integer $InstanzID)`  
 Liefert den aktuellen Wert der Lautst�rke.  
`integer LSQ_GetSleep(integer $InstanzID)`  
Liefert die verbleibende Zeit bis zum ausschalten des Ger�tes bei aktivem Schlafmodus.  
Ist der Schlafmodus nicht aktiv, wird 0 gemeldet.  

#### Syncronisieren:

Alle LSQ_Set* - Befehle liefern einen `boolean` als R�ckgabewert.
`true` wenn der gleiche Wert vom Server best�tigt wurde.
`false` wenn der best�tigte Wert abweicht.
Wird der Befehl nicht best�tigt, so ist die ein Fehler (Exception wird erzeugt).

`boolean LSQ_SetSync(integer $InstanzID, integer $SlaveInstanzID)`  
`$SlaveInstanzID` wird als Client der `$InstanzID` zugeordnet.

`boolean LSQ_SetUnSync(integer $InstanzID)`  
L�st `$InstanzID` aus der Syncronisierung von dem Master.

Alle LSQ_Get* - Befehle liefern einen jeweils beschriebenen R�ckgabewert.  
Antwortet das Ger�t nicht auf die Anfrage, so ist die ein Fehler und eine Exception wird erzeugt.  

`mixed (array or boolean) LSQ_GetSync(integer $InstanzID)`  
Liefert alle InstanzIDs der mit `$InstanzID` gesyncten Ger�te als Array.  
`false` wenn kein Sync aktiv ist.  

### Konfiguration:

#### LMSSplitter:

GUID: `{61051B08-5B92-472B-AFB2-6D971D9B99EE}`  

**Datenempfang vom Child:**  
Interface-GUI:`{EDDCCB34-E194-434D-93AD-FFDF1B56EF38}`  
Objekt vom Typ `LSQData`  

| Eigenschaft | Typ     | Standardwert | Funktion                           |
| :---------: | :-----: | :----------: | :--------------------------------: |
| Open        | boolean | true         | Verbindung zum LMS aktiv / deaktiv |
| Host        | string  |              | Adresse des LMS                    |
| Port        | integer | 9090         | CLI-Port des LMS                   |
| Webport     | integer | 9000         | Port des LMS-Webserver             |


#### LSQDevice:  

GUID: `{118189F9-DC7E-4DF4-80E1-9A4DF0882DD7}`  

**Datenempfang vom Splitter:**  
Interface-GUI:`{CB5950B3-593C-4126-9F0F-8655A3944419}`  
Objekt vom Typ `LMSResponse`  

| Eigenschaft | Typ     | Standardwert | Funktion                                                              |
| :---------: | :-----: | :----------: | :-------------------------------------------------------------------: |
| Address     | string  |              | MAC [inkl. : ] bei SqueezeBox-Ger�ten IP-Adresse bei Anderen          |
| CoverSize   | string  | cover        | Gr��e vom Cover:  cover  cover150x150  cover300x300                   |
| Interval    | integer | 2            | Abstand in welchen der LMS aktuelle Daten bei der Wiedergabe liefert. |

