# Mini Music App
## Projektidee

Die Mini Music App ist eine Webanwendung zur Verwaltung von Musik-Playlists. Benutzer können Artists und Songs zur Datenbank hinzufügen, neue Playlists erstellen und Songs zu diesen Playlists hinzufügen. Die App zeigt alle Songs, Artists und Playlists übersichtlich an und ermöglicht es, Playlists mit ihren enthaltenen Songs und Artists zu durchsuchen. Das Projekt nutzt eine PostgreSQL-Datenbank und Streamlit als Frontend.

## ER Modell

### Entitätstypen:
1. artists – Musikkünstler (Name, Land, Genre)
2. songs – Musikstücke (Titel, Dauer, Erscheinungsjahr)
3. playlists – Wiedergabelisten (Name, Ersteller, Erstellungsdatum)

### Beziehungstypen:
1. artists -> songs (1:n) – Ein Artist kann mehrere Songs haben, ein Song gehört zu einem Artist
2. playlists -> songs (n:m) – Eine Playlist kann mehrere Songs enthalten, ein Song kann in mehreren Playlists sein. Diese Beziehung wird durch die Tabelle `playlist_songs` umgesetzt.

### Kardinalitäten:
- Artist zu Song: 1:n (ein Artist, viele Songs)
- Playlist zu Song: n:m (viele Playlists, viele Songs)

[ER-Design Mini Projekt](er-design.png "ER-Design Mini Projekt")

## Beschreibung der Streamlit-App

### 1. Eingabeformular (was wird erfasst?)

Die App bietet mehrere Formulare zur Dateneingabe:

- Artist hinzufügen: Name, Land, Genre des Künstlers
- Song hinzufügen: Titel, Artist (Dropdown), Dauer in Sekunden, Erscheinungsjahr
- Playlist erstellen: Playlist-Name, Ersteller
- Song zu Playlist hinzufügen: Auswahl einer Playlist (Dropdown), Auswahl eines Songs (Dropdown), Position in der Playlist

### 2. Datenanzeige (welche Abfrage wird angezeigt?)

Die App zeigt folgende Daten an:

- Tab 1 – Songs & Artists:
  - Alle Songs mit ID, Titel, Dauer, Jahr und Artist-ID
  - Alle Artists mit ID, Name, Land und Genre

- Tab 3 – Playlists:
  - Alle Playlists mit ihren Songs (JOIN über `playlists`, `playlist_songs`, `songs` und `artists`)
  - Anzeige in erweiterbaren Boxen mit Song-Titel, Artist-Name und Position
  - Filter: Gruppierung nach Playlist-Name

Die Hauptabfrage nutzt LEFT JOINs um Playlists auch anzuzeigen, wenn sie noch keine Songs enthalten:


## Ausführen der App

1. `pip install -r requirements.txt`
2. `python setup_db.py`
3. `python -m streamlit run streamlit_app.py`



# **Mini Music App**

## **Project Idea**

The Mini Music App is a web application for managing music playlists. Users can add artists and songs to the database, create new playlists, and add songs to these playlists. The app displays all songs, artists, and playlists in an organized way and allows users to browse playlists along with their songs and artists. The project uses a PostgreSQL database and Streamlit as the frontend.

## **ER Model**

### **Entity Types**

1. **artists** – music artists (name, country, genre)
2. **songs** – music tracks (title, duration, release year)
3. **playlists** – playlists (name, creator, creation date)

### **Relationship Types**

1. **artists → songs (1:n)** – one artist can have multiple songs, each song belongs to one artist
2. **playlists → songs (n:m)** – a playlist can contain multiple songs, and a song can be part of multiple playlists. This relationship is implemented through the `playlist_songs` table.

### **Cardinalities**

* Artist to Song: **1:n** (one artist, many songs)
* Playlist to Song: **n:m** (many playlists, many songs)


## **Description of the Streamlit App**

### **1. Input Forms (what is being collected?)**

The app provides several forms for data entry:

* **Add Artist:** name, country, genre
* **Add Song:** title, artist (dropdown), duration in seconds, release year
* **Create Playlist:** playlist name, creator
* **Add Song to Playlist:** choose playlist (dropdown), choose song (dropdown), position in playlist

### **2. Data Display (what queries are shown?)**

The app displays the following data:

* **Tab 1 – Songs & Artists:**

  * All songs with ID, title, duration, year, and artist ID
  * All artists with ID, name, country, and genre

* **Tab 3 – Playlists:**

  * All playlists with their songs (JOIN across `playlists`, `playlist_songs`, `songs`, and `artists`)
  * Shown in expandable boxes with song title, artist name, and position
  * Filter: grouping by playlist name

The main query uses **LEFT JOINs** to ensure playlists are shown even if they don’t contain any songs.

## **Running the App**

1. `pip install -r requirements.txt`
2. `python setup_db.py`
3. `python -m streamlit run streamlit_app.py`

