### Football-Attendance-Predictions
# Emilio Barragán Godoy

The main goal of this project was to create a Machine Learning model that predicts the attendance of football matches all around the world. This included matches from every national league (like Liga MX or Premier League), every continental cup (like the UEFA Champions League or CONMEBOL Libertadores), as well as international tournaments like the World Cup, EURO, etc.

The main reason I started this project was because I am a huge football fan, mainly from the country and city I live in (Monterrey, Mexico), but I also enjoy watching football from other countries like Brazil, England and even some regions like South America and Europe. And recently in june 2025 the Club World Cup took place in the US and it was very exciting to see teams from all around the world playing against each other, I even got the opportunity to go to one of the matches from the team I support (Rayados). However, something that caught my eye, not just from the match I went to see, but from matches I could watch in live TV, was the attendance of these events, mainly the fact that some of them had very low.

<img width="746" height="455" alt="image" src="https://github.com/user-attachments/assets/500aaf58-e7c2-4b2b-bfa9-d0b477792dd5" />


The reason why Club America is in the graph is because the data includes the play-off against LAFC.

Green: avg >40,000, Yellow: avg > 25,000, Red: avg < 25,000

This image represents the average attendance of every team that participated in the Club World Cup 2025, as we can see, there are some clubs that had a low attendance, at least compared to what FIFA expected, and thats why we saw some matches with empty stadiums or only half filled. The main reason could be that a club's fanbase is very different from a national team, this meaning that teams like Real Madrid, Bayern, PSG and so on have huge fanbases because they are recognized all around the world, but other teams like, Pachuca, Mamelodi Sundowns or Ulsan HD are only famous in their country, or worse, their city. Another important aspect is the host country/city, where people from Asia, South America and even Europe might find it difficult to travel to the US considering distance, timing, prices, etc, which is very important considering that clubs have a different fanbase than national teams. 
However, if distance and prices and timing are a the main reason, then the World Cup would also have low average attendance, which is not the case, in Qatar, not a single team averaged less than 40,000, which is great. This confirms that national teams and events including them, are more attractive to not just football fans but also locals and tourists all around the world.

<img width="639" height="455" alt="image (1)" src="https://github.com/user-attachments/assets/55229c06-d56e-423d-a31a-3959ba4afe23" />

And when I noticed this I started questioning myself, if the in 2026 will be the World Cup and the majority of the matches will take place in the US, will the attendances be similar? Will we have some matches with very low filling rate/empty stadiums? What will be the attendance expected for every match?
In a few words, we would probably have a world cup similar to the one in 1994, which had an average of 68,991 spectators per match (the highest one in history), which in this year could be a bit lower considering there will be some smaller stadiums which are in Canada and Mexico. However, that doesn't deny the fact that we still might have some matches where the filling rate might be a bit low. And that's what I wanted to find out.

Using a free API from ESPN data, I was able to extract all the data registered from football events, including professional clubs matches, international tournaments, national leagues, continental cups, and so on. Once extracted over 500,000 matches I started cleaning data, which include removing matches where the attendance is not given, as well as adding missing data if there is enough data given (e.g. if the venue is FNB Stadium and the city and country are null, we can fill them with Johannesburg, South Africa). And using this data, I started calculating the popularity of every variable considered that I considered to be useful in the attendance of a match, which are the average of the two teams playing, city, venue, country, tournament, phase (e.g. "Final", "Group stage"), phase_tournament (e.g."World Cup Final", "Liga MX Semifinal"), day (sunday, friday), hour (1-24), month (1-12) and the maximum capacity of the venue.

Using a random forest generator from scikit-learn I was able to introduce all this data and test it to have a functional machine learning model that has a **MAE: 2823.75** (Absolute Error = abs(attendance-prediction)). Once the model was ready I started testing with previous tournaments to see what I could use to improve the model, as well notice any pattern, like outliers or missing data. During testing I noticed that tournaments where national teams face each other not just are more popular, but also that the model gives a more accurate prediction, which is great for predicting this year's world cup, but not so great since for club tournaments, like Liga MX, UEFA Champions League, Club World Cup, etc, the model does get a higher MAE, but I am still working to improve that number.

For now, I am trying to get the best results for this World Cup, and considering the variables mentioned, the World Cup in 2026 will have an average of **60,448** spectators per match and a total of **6,286,656** spectators throughout all the tournament, which would make this world cup the second with the highest average per match, and the first one with the most spectators of all time. The knockout matches were created assuming that the bracket will be the following:
<img width="1891" height="824" alt="image" src="https://github.com/user-attachments/assets/b2afc9f2-54d7-495f-85a9-e793bb1de2b3" />


Since I tested the model with past world cups, and it got an average MAE lower than 2,000, we can say that it is very safe and reliable to predict the World Cup attendance in 2026 with this model. For now you can find the data in the file results_wc2026.csv, which is a file with every match (the teams in the knockout stage can change), but here is some data from the predictions:

## Average per match: 60,448

## Total: 6,286,656

# Top 5 matches with the most spectators according to the model
| homeTeamName   | awayTeamName   | city            |   modpred |
|:---------------|:---------------|:----------------|----------:|
| Germany        | England        | Arlington       |     77776 |
| Ecuador        | Germany        | East Rutherford |     79338 |
| Brazil         | Morocco        | East Rutherford |     79793 |
| France         | Sweden         | East Rutherford |     81251 |
| Germany        | Portugal       | East Rutherford |     84385 |

# Top 5 matches with the least spectators according to the model
| homeTeamName   | awayTeamName           | city    |   modpred |
|:---------------|:-----------------------|:--------|----------:|
| Senegal        | Iraq                   | Toronto |     35330 |
| Ghana          | Panama                 | Toronto |     38587 |
| Panama         | Croatia                | Toronto |     39269 |
| Germany        | Ivory Coast            | Toronto |     40067 |
| Canada         | Bosnia and Herzegovina | Toronto |     40174 |

# Average spectators in every city
<img width="663" height="455" alt="image (2)" src="https://github.com/user-attachments/assets/2c7b43a6-f497-4ca8-b0b3-007728fd6aad" />

# All the data
| homeTeamName           | awayTeamName           | city            |   modpred |
|:-----------------------|:-----------------------|:----------------|----------:|
| South Korea            | Czechia                | Guadalajara     |     41783 |
| Mexico                 | South Africa           | Mexico City     |     73508 |
| Canada                 | Bosnia and Herzegovina | Toronto         |     40174 |
| United States          | Paraguay               | Inglewood       |     70378 |
| Haiti                  | Scotland               | Foxborough      |     47968 |
| Brazil                 | Morocco                | East Rutherford |     79793 |
| Qatar                  | Switzerland            | Santa Clara     |     60043 |
| Australia              | Türkiye                | Vancouver       |     47525 |
| Germany                | Curacao                | Houston         |     65298 |
| Ivory Coast            | Ecuador                | Philadelphia    |     56684 |
| Sweden                 | Tunisia                | Guadalupe       |     51605 |
| Netherlands            | Japan                  | Arlington       |     74824 |
| Belgium                | Egypt                  | Seattle         |     56948 |
| Iran                   | New Zealand            | Inglewood       |     63374 |
| Spain                  | Cape Verde             | Atlanta         |     57258 |
| Saudi Arabia           | Uruguay                | Miami Gardens   |     58140 |
| Iraq                   | Norway                 | Foxborough      |     41798 |
| Austria                | Jordan                 | Santa Clara     |     60252 |
| France                 | Senegal                | East Rutherford |     75528 |
| Argentina              | Algeria                | Kansas City     |     67467 |
| Ghana                  | Panama                 | Toronto         |     38587 |
| Portugal               | Congo DR               | Houston         |     64633 |
| Uzbekistan             | Colombia               | Mexico City     |     65359 |
| England                | Croatia                | Arlington       |     76741 |
| Czechia                | South Africa           | Atlanta         |     56916 |
| Switzerland            | Bosnia and Herzegovina | Inglewood       |     65041 |
| Canada                 | Qatar                  | Vancouver       |     47239 |
| Mexico                 | South Korea            | Guadalajara     |     45249 |
| United States          | Australia              | Seattle         |     62077 |
| Türkiye                | Paraguay               | Santa Clara     |     61795 |
| Brazil                 | Haiti                  | Philadelphia    |     57666 |
| Scotland               | Morocco                | Foxborough      |     53947 |
| Ecuador                | Curacao                | Kansas City     |     63099 |
| Netherlands            | Sweden                 | Houston         |     66918 |
| Germany                | Ivory Coast            | Toronto         |     40067 |
| Tunisia                | Japan                  | Guadalupe       |     51607 |
| Uruguay                | Cape Verde             | Miami Gardens   |     56223 |
| Belgium                | Iran                   | Inglewood       |     65450 |
| New Zealand            | Egypt                  | Vancouver       |     42471 |
| Spain                  | Saudi Arabia           | Atlanta         |     61009 |
| Norway                 | Senegal                | East Rutherford |     70748 |
| Jordan                 | Algeria                | Santa Clara     |     60622 |
| Argentina              | Austria                | Arlington       |     73404 |
| France                 | Iraq                   | Philadelphia    |     57666 |
| England                | Ghana                  | Foxborough      |     56457 |
| Colombia               | Congo DR               | Guadalajara     |     42806 |
| Panama                 | Croatia                | Toronto         |     39269 |
| Portugal               | Uzbekistan             | Houston         |     63758 |
| Bosnia and Herzegovina | Qatar                  | Seattle         |     52236 |
| Switzerland            | Canada                 | Vancouver       |     50573 |
| Morocco                | Haiti                  | Atlanta         |     57665 |
| Scotland               | Brazil                 | Miami Gardens   |     60916 |
| South Africa           | South Korea            | Guadalupe       |     50996 |
| Czechia                | Mexico                 | Mexico City     |     70152 |
| Ecuador                | Germany                | East Rutherford |     79338 |
| Paraguay               | Australia              | Santa Clara     |     62012 |
| Türkiye                | United States          | Inglewood       |     70214 |
| Japan                  | Sweden                 | Arlington       |     73524 |
| Tunisia                | Netherlands            | Kansas City     |     67299 |
| Curacao                | Ivory Coast            | Philadelphia    |     52650 |
| Senegal                | Iraq                   | Toronto         |     35330 |
| Norway                 | France                 | Foxborough      |     52334 |
| Egypt                  | Iran                   | Seattle         |     54862 |
| New Zealand            | Belgium                | Vancouver       |     44444 |
| Cape Verde             | Saudi Arabia           | Houston         |     58141 |
| Uruguay                | Spain                  | Guadalajara     |     44888 |
| Croatia                | Ghana                  | Philadelphia    |     58551 |
| Colombia               | Portugal               | Miami Gardens   |     61648 |
| Congo DR               | Uzbekistan             | Atlanta         |     54971 |
| Jordan                 | Argentina              | Arlington       |     72822 |
| Algeria                | Austria                | Kansas City     |     64981 |
| Panama                 | England                | East Rutherford |     76743 |
| Czechia                | Bosnia and Herzegovina | Inglewood       |     63460 |
| Morocco                | Japan                  | Houston         |     65337 |
| Netherlands            | Brazil                 | Guadalupe       |     53030 |
| Germany                | Scotland               | Foxborough      |     55578 |
| Ivory Coast            | Senegal                | Arlington       |     68929 |
| Mexico                 | Saudi Arabia           | Mexico City     |     70825 |
| France                 | Sweden                 | East Rutherford |     81251 |
| Belgium                | South Africa           | Seattle         |     55666 |
| United States          | Qatar                  | Santa Clara     |     63804 |
| Croatia                | Norway                 | Atlanta         |     57381 |
| Colombia               | England                | Toronto         |     43812 |
| Spain                  | Algeria                | Inglewood       |     67663 |
| Switzerland            | Ecuador                | Vancouver       |     46480 |
| Türkiye                | Egypt                  | Arlington       |     70570 |
| Argentina              | Uruguay                | Miami Gardens   |     62140 |
| Portugal               | Australia              | Kansas City     |     67796 |
| Czechia                | Brazil                 | Houston         |     66378 |
| Germany                | France                 | Philadelphia    |     61758 |
| Morocco                | Senegal                | East Rutherford |     77182 |
| Mexico                 | Croatia                | Mexico City     |     72916 |
| England                | Spain                  | Arlington       |     77507 |
| United States          | Belgium                | Seattle         |     62074 |
| Ecuador                | Portugal               | Vancouver       |     49226 |
| Argentina              | Türkiye                | Atlanta         |     61146 |
| Germany                | Brazil                 | Foxborough      |     57146 |
| England                | Belgium                | Inglewood       |     68026 |
| Senegal                | Croatia                | Miami Gardens   |     57038 |
| Argentina              | Portugal               | Kansas City     |     69749 |
| Germany                | England                | Arlington       |     77776 |
| Croatia                | Portugal               | Atlanta         |     65469 |
| Croatia                | England                | Miami Gardens   |     60696 |
| Germany                | Portugal               | East Rutherford |     84385 |

# NOTE: THE WHOLE DATA COULDN'T BE ADDED BECAUSE GITHUB DOESN'T ALLOW FILES OVER 100 MB
