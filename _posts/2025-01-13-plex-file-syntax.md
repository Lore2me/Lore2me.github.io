---
layout: post
title: Plex - File Administration
date: 2025-01-13 14:48 +0100
categories: [Plex]
tags: [plex]
description: How to name and store the files for Plex to recognize them.
---
# Plex - File Administration
This guide explains how to name and store the files for Plex to recognize them.

## Directory structure
Plex uses a directory structure to organize the media files. The basic structure is:
```
Media/
├── Movies/
├── TV Shows/
├── Music/
```

Where `Media` is the root directory, and `Movies`, `TV Shows`, and `Music` are the subdirectories.
TV Shows is the directory for series, and each series has its own subdirectory.

## Naming conventions
Plex uses a series of regular expressions to match the files to the metadata in its database. The following are the most common naming conventions:

### Movies
The basic format for movies is:
```
Movie Title (Year).ext
```
Where `ext` is the file extension (e.g., `mp4`, `mkv`, `avi`, etc.).

#### IMDB ID
If you have the IMDB ID of the movie, you can also use it in the file name:
```
Movie Title (Year) {imdb-XXX}.ext
```
Where `XXX` is the IMDB ID of the movie, it can be found in the url of the movie page on IMDB.

Example:
```
Movies/
├── The Shawshank Redemption (1994)
│   ├── The Shawshank Redemption (1994).mkv
│   ├── The Shawshank Redemption (1994) {imdb-tt0111161}.mkv
```

#### Quality
If you have multiple versions of the same movie, you can also include the quality in the file name:
```
Movie Title (Year) {Quality}.ext
```
Where `Quality` is the quality of the movie (e.g., `1080p`, `720p`, `480p`, etc.).

Example:
```
Movies/
├── The Shawshank Redemption (1994)
│   ├── The Shawshank Redemption (1994) {1080p}.mkv
│   ├── The Shawshank Redemption (1994) {720p}.mkv
```

#### Version (Premium feature)
If you have multiple versions of the same movie, you can also include the version in the file name:
```
Movie Title (Year) {edition-VERSION}.ext
```
Where `VERSION` is the version of the movie (e.g., `Director's Cut`, `Extended Edition`, `Theatrical Cut`, etc.).

Example:
```
Movies/
├── The Shawshank Redemption (1994) {edition-Director's Cut}
│   ├── The Shawshank Redemption (1994) {edition-Director's Cut}.mkv
│   ├── The Shawshank Redemption (1994) {edition-Extended Edition}.mkv
```

*The ability to specify different editions for a movie requires a Plex Pass subscription for Plex Media Server admin account.*

#### Movies Split Across Multiple Files
If a movie is split across multiple files, you can use the following format:
```
Movie Title (Year) - Part XX.ext
```
Where `XX` is the part number.

Example:
```
Movies/
├── The Shawshank Redemption (1994) - Part 1.mkv
├── The Shawshank Redemption (1994) - Part 2.mkv
```

### TV Shows / Series
The basic format for TV shows is:
```
TV Show Name/
    Season XX/
        TV Show Name - SXXEXX - Episode Title.ext
```
Where `XX` is the season number, `XX` is the episode number, and `ext` is the file extension.

Example (if you would somehow have the TV show Breaking Bad, I'dont have it):
```
TV Shows/
├── Breaking Bad/
│   ├── Season 01/
│   │   ├── Breaking Bad - S01E01 - Pilot.mkv
│   │   ├── Breaking Bad - S01E02 - Cat's in the Bag.mkv
│   │   ├── ...
│   ├── Season 02/
│   │   ├── Breaking Bad - S02E01 - Seven Thirty-Seven.mk
│   │   ├── Breaking Bad - S02E02 - Grilled.mkv
│   │   ├── ...
```

But if you don't know the episode title, you don't need to wrote it. Plex will still recognize the file.

### Music
The basic format for music is:
```
Music/
├── Artist/
│   ├── Album/
│   │   ├── Track Number - Track Title.ext
```
Where `Track Number` is the number of the track, `Track Title` is the title of the track, and `ext` is the file extension.

Example:
```
Music/
├── Pink Floyd/
│   ├── The Dark Side of the Moon/
│   │   ├── 01 - Speak to Me.mp3
│   │   ├── 02 - Breathe.mp3
│   │   ├── ...
```

If you don't have a full album, you can also put the tracks directly in the `Artist` directory.
Example:
```
Music/
├── Pink Floyd/
│   ├── 01 - Speak to Me.mp3
│   ├── 02 - Breathe.mp3
│   ├── ...
```

## Conclusion
By following these naming conventions,
Plex will be able to recognize your media files and match them to the metadata in its database.
This will ensure that your media library is organized and easy to navigate.
If you don't follow these conventions, Plex may not be able to match your files correctly.
