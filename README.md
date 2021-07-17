# Chinook Database
Introduction\
In this project, I queried the Chinook Database. The Chinook Database holds information about a music store. For this project, I will be assisting the Chinook team with understanding the media in their store, their customers and employees, and their invoice information. To assist in the queries ahead, the schema for the Chinook Database is provided below. You can see the columns that link tables together via the arrows.

<img width="652" alt="Project PK and FK" src="https://user-images.githubusercontent.com/87584380/126049432-77b0aa15-c0c3-482a-9d9e-642142133728.png">

My presentation includes:\
Four slides\
One visualization per slide\
A 1-2 sentence explanation of each slide\
The SQL query used to create the data used in the visualization. 

Visualization:
[sql-project-submission-template-1.pptx](https://github.com/Adeleke1/PortfolioWorks/files/6835350/sql-project-submission-template-1.pptx)

# Queries used for my Project:	
1. /*Query 1 - query used to get amount spent by customers per country on any album by U2/
```
SELECT c.Country, SUM(il.Quantity)*il.UnitPrice AS Amount,
FROM Artist ar
JOIN Album a
ON a.ArtistId = ar.ArtistId
JOIN Track t
ON a.AlbumId = t.AlbumId
JOIN InvoiceLine il
ON il.trackId = t.trackId
JOIN Invoice i
ON i.InvoiceId = il.InvoiceId
JOIN Customer c
ON c.CustomerId = i.CustomerId
WHERE ar.name= "U2"
GROUP By c.Country, ar.name
ORDER BY Amount DESC
LIMIT 10
```
2. /*Query 2- query used to obtain top 5 playlists with highest amount of Purchase*/
```
SELECT p.Name, COUNT(i.InvoiceId) AS Purchases\
JOIN PlayListTrack pt\
ON pt.PlaylistId = p.PlaylistId\
JOIN Track t\
ON t.TrackId = pt.TrackId\
JOIN InvoiceLine il\
ON il.TrackId = t.TrackId\
JOIN Invoice i\
ON i.InvoiceId = il. InvoiceId\
JOIN Customer c\
ON i.CustomerId = c.CustomerId\
GROUP BY p.Name\
ORDER BY Purchases DESC\
LIMIT 5
```

3. /*Query 3- query used to know the total amount spent per genre in Berlin, Germany*/
```
SELECT g.name AS Genres, Sum(i.Total) Total_spent, c.city\
FROM Customer c\
JOIN Invoice i\
ON i.CustomerId = c.CustomerId\
JOIN InvoiceLine il\
ON il.InvoiceId = i.InvoiceId\
JOIN Track t\
ON t.TrackId = il.TrackId\
JOIN Genre g\
ON g.GenreId = t.GenreId\
WHERE c.Country = "Germany" AND c.city ="Berlin"\
GROUP BY Genres, c.City\
ORDER BY c.state, Total_spent DESC
```

4. /*Query 4- query used to obtain the no of alternative tracks in playlist/
```
SELECT p.PlaylistId, g.Name, p.Name Playlists, Count(t.Name) AS Tracks\
FROM Playlist p\
JOIN PlaylistTrack pt\
ON pt.PlaylistId = p.PlaylistId\
JOIN Track t\
ON pt.TrackId = t.TrackId\
JOIN Genre g\
ON t.GenreId = g.GenreId\
WHERE g.name = "Alternative"\
GROUP BY Playlists\
ORDER BY Tracks
```
